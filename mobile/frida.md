---
layout: default
---

# Frida 

[Frida](https://frida.re/) is a dynamic instrumentation toolkit for developers, reverse-engineers, and security researchers. There are common techniques used to [detect Frida](https://github.com/darvincisec/DetectFrida)
* Detect through named pipes used by Frida
* Detect through frida specific named thread
* Compare text section in memory with text section in disk for both libc and native library

Nontheless, there are also different [Frida patches](https://github.com/AAAA-Project/Patchs/tree/master/strongR-frida/frida-core) that can be applied in order to bypass common detection mechanisms.

* 0001-string_frida_rpc.patch
* 0002-io_re_frida_server.patch
* 0003-pipe_linjector.patch
* 0004-io_frida_agent_so.patch
* 0005-symbol_frida_agent_main.patch
* 0006-thread_gum_js_loop.patch
* 0007-thread_gmain.patch
* 0008-protocol_unexpected_command.patch

When the above patches are not enough to bypass security checks it is usually a good idea to start using early instrumentation, such as in the following snippet:


### Hook shared library before init_array. Adapted from [Giovanni Roca](http://www.giovanni-rocca.com/giving-yourself-a-window-to-debug-a-shared-library-before-dt_init-with-frida-on-android/)

```js
var found = false;
var library = "libtest.so"
Interceptor.attach(Module.findExportByName("libc.so", "open"), {
    onEnter: function() {
        //read first argument shared library name
        var name = Memory.readUtf8String(this.context.r0);
        if (name.includes(library)) {
            found = true;
        }
    }, 
    onLeave: function(ret) {
        if (found) {
            found = false;
            var symb = Module.enumerateSymbolsSync("linker");
            var pp = 0;
            for (var sym in symb) {
                //hook prelink
                if (symb[sym].name.indexOf("prelink") >= 0) {
                    pp = symb[sym].address
                }
            }
            Interceptor.attach(pp, function() {
                //review
                console.log('leaked base before init array -> ' + this.context.r1.sub(0x34));
            });
            
        }            
    }
});
```
## Snippets

There are many useful [snippets](https://github.com/iddoeldor/frida-snippets) that can be used to perform dynamic analysis, the following are the most relevant ones:

### Enumerate loaded classes

```js
Java.perform(function() {
    Java.enumerateLoadedClasses({
        onMatch: function(className) {
            console.log(className);
        },
        onComplete: function() {}
    });
});
```

### Hook reflection

```js
 Java.use('java.lang.reflect.Method').invoke.overload('java.lang.Object', '[Ljava.lang.Object;', 'boolean').implementation = function(a,b,c) {
      console.log('hooked!', a, b, c);
      return this.invoke(a,b,c);
  };
```

### Reveal native methods

```js
var RevealNativeMethods = function() {
  var pSize = Process.pointerSize;
  var env = Java.vm.getEnv();
  var RegisterNatives = 215, FindClassIndex = 6; // search "215" @ https://docs.oracle.com/javase/8/docs/technotes/guides/jni/spec/functions.html
  var jclassAddress2NameMap = {};
  function getNativeAddress(idx) {
    return env.handle.readPointer().add(idx * pSize).readPointer();
  }
  // intercepting FindClass to populate Map<address, jclass>
  Interceptor.attach(getNativeAddress(FindClassIndex), {
    onEnter: function(args) {
      jclassAddress2NameMap[args[0]] = args[1].readCString();
    }
  });
  // RegisterNative(jClass*, .., JNINativeMethod *methods[nMethods], uint nMethods) // https://android.googlesource.com/platform/libnativehelper/+/master/include_jni/jni.h#977
  Interceptor.attach(getNativeAddress(RegisterNatives), {
    onEnter: function(args) {
      for (var i = 0, nMethods = parseInt(args[3]); i < nMethods; i++) {
        /*
          https://android.googlesource.com/platform/libnativehelper/+/master/include_jni/jni.h#129
          typedef struct {
             const char* name;
             const char* signature;
             void* fnPtr;
          } JNINativeMethod;
        */
        var structSize = pSize * 3; // = sizeof(JNINativeMethod)
        var methodsPtr = ptr(args[2]);
        var signature = methodsPtr.add(i * structSize + pSize).readPointer();
        var fnPtr = methodsPtr.add(i * structSize + (pSize * 2)).readPointer(); // void* fnPtr
        var jClass = jclassAddress2NameMap[args[0]].split('/');
	      var methodName = methodsPtr.add(i * structSize).readPointer().readCString();
        console.log('\x1b[3' + '6;01' + 'm', JSON.stringify({
          module: DebugSymbol.fromAddress(fnPtr)['moduleName'], // https://www.frida.re/docs/javascript-api/#debugsymbol
          package: jClass.slice(0, -1).join('.'),
          class: jClass[jClass.length - 1],
          method: methodName, // methodsPtr.readPointer().readCString(), // char* name
          signature: signature.readCString(), // char* signature TODO Java bytecode signature parser { Z: 'boolean', B: 'byte', C: 'char', S: 'short', I: 'int', J: 'long', F: 'float', D: 'double', L: 'fully-qualified-class;', '[': 'array' } https://github.com/skylot/jadx/blob/master/jadx-core/src/main/java/jadx/core/dex/nodes/parser/SignatureParser.java
          address: fnPtr
        }), '\x1b[39;49;00m');
      }
    }
  });
}
Java.perform(RevealNativeMethods);
```
