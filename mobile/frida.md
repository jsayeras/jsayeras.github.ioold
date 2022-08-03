---
layout: default
---

## Frida 

Enumerate loaded classes

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

Hook shared library before init_array. Adapted from [Giovanni Roca](http://www.giovanni-rocca.com/giving-yourself-a-window-to-debug-a-shared-library-before-dt_init-with-frida-on-android/)

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