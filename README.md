# ModuleLoaders

TLDR

Are you making a simple nodejs app?  Use CommonJS.  

Are you making anything else (TS/ES6). Use new ES6, but will have to configure SystemJS/Webpack/TypeScript Compiler (tsc) to transpile them back down to commonJS/SystemJs.


**CommonJS**

Spec for module loading.
NodeJS implements this spec

    // salute.js
    var MySalute = "Hello";
    module.exports = MySalute;
    // world.js
    var MySalute = require("./salute");
    var Result = MySalute + "world!";
    module.exports = Result;

**AMD**

CommonJS but for web browsers.  
Async (commonJS is synchronous loading)

    //Explicitly defines the "foo/title" module:
    define("foo/title",
        ["my/cart", "my/inventory"],
        function(cart, inventory) {
            //Define foo/title object in here.
       }
    );

    require(['foo'], function(foo) {
    
    });


**SystemJS**

Universal module loader.  Works with ES6, AMD, CommonJS, global scripts.  Works in the browser and NodeJS.

**ES6 - Replaces ComonJS/AMD.**

Not supported by anything yet, have to use SystemJS on top, or transpile code first using webpack

      //------ lib.js ------
    export const sqrt = Math.sqrt;
    export function square(x) {
        return x * x;
    }
    export function diag(x, y) {
        return sqrt(square(x) + square(y));
    }
    
    //------ main.js ------
    import { square, diag } from 'lib';
    console.log(square(11)); // 121
    console.log(diag(4, 3)); // 5


    //------ main.js ------
    import * as lib from 'lib';
    console.log(lib.square(11)); // 121
    console.log(lib.diag(4, 3)); // 5
