---
layout: default
---

## Frida 

[Frida](https://frida.re/) is a dynamic instrumentation toolkit for developers, reverse-engineers, and security researchers.

[DetectFrida](https://github.com/darvincisec/DetectFrida)
* Detect through named pipes used by Frida
* Detect through frida specific named thread
* Compare text section in memory with text section in disk for both libc and native library

There are different [Frida patches](https://github.com/AAAA-Project/Patchs/tree/master/strongR-frida/frida-core) that can be applied in order to bypass common detection mechanisms.

* frida-core	0001-string_frida_rpc.patch
* frida-core	0002-io_re_frida_server.patch
* frida-core	0003-pipe_linjector.patch
* frida-core	0004-io_frida_agent_so.patch
* frida-core	0005-symbol_frida_agent_main.patch
* frida-core	0006-thread_gum_js_loop.patch
* frida-core	0007-thread_gmain.patch
* frida-core	0008-protocol_unexpected_command.patch

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