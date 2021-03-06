# DeepInto_ECMAScript_and_TypeScript
1. 深入 ES 规范，通过对规范的解析来解释 JS 代码的执行过程；2. TS 新特性的讲解及新特性到 JS 的转译

该系列主要包括两个部分：[ECMAScript 规范解析](https://shadowkimi520.github.io/DeepInto_ECMAScript_and_TypeScript/DeepInto_ECMAScript/) 和 [TypeScript 特性转译](https://shadowkimi520.github.io/DeepInto_ECMAScript_and_TypeScript/TypeScript_Transpiling/)

* 第一部分尝试通过对 ECMAScript 规范的解析来理解 JS 代码的执行过程，计划涉及：
> 1. JS中的变量/值/类型：首先从语言的层面讲解 JS 的基本数据类型（原始类型和对象类型），然后深入规范讨论下这些类型在底层是如何表示的；JS中操作数的隐式类型转换（针对各元算符，涉及ToPrimitive/ToNumber/ToString/ToObject/ToBoolean等抽象操作，ToPrimitive操作的meta programming）；String/Number/Boolean的显示类型转换及对应的包装类型对象；call-by-value/call-by-reference/call-by-share；
> 2. 对象和原型链（ordinary object /  standard exotic object）
> 3. 函数/this/作用域链（箭头函数/方法/构造函数/生成器函数/异步函数）
> 4. 对象的继承方式/ES6 class
> 5. 异步编程（发布-订阅/Promise/Promise + Generator/Async + await

* 第二部分主要是解释 TS 中的新特性。作为一门转译语言，TS 自身并没有运行时特性，最终都需要转译为JS，从而在宿主环境中运行（浏览器/NodeJS等）。ES规范中的某些最新功能可能旧版本的TS并不包含，但 TS 官方承诺会持续兼容最新的 ES 规范，因此 ES 规范中添加的新特性最终都会被包含进新版本的TS，所以TS可以认为是ES6+的超集，ES6/ES2016/ES2017/ES2018...中的新特性最终都会被那个时期最新版本的TS支持（即使浏览器还未支持最新版本的ES标准，只要TS已经支持了，就可以为这些新特性转译出当前浏览器支持的代码，通过模拟的代码在只支持旧版本ES的宿主环境中来支持新特性。TS的好处有两点：1.没有被纳入当前版本ES规范的特性TS可能会支持，我们可以提前在代码中使用该特性（比如ES5时代我们就可以使用class；可以直接使用不被ES6规范支持的装饰器特性）；2. 支持强类型及类型检查，这在大型项目开发过程中可以规避很多很难发现的BUG
当然ES规范也会从TS吸收经验，将TS中比较好的特性直接加入到ES规范中，由JS原生支持，这样在支持这些功能特新的宿主环境中可以直接不进行转译；相反，不支持这些新特性的宿主环境可以通过TS转译后的代码支持新特性。比如ES5不支持的class特性，ES6开始从语言层面内生支持，这样用TS语言写的class特性在支持ES6的宿主环境中不需要转译就可以直接运行，不支持ES6的环境中，我们可以通过TS的配置选项转译出模拟class特性的ES5代码。
归纳起来：
> 1. ES 规范中不大可能加入的 TS 独有特性，比如 类型声明 / 接口。 这部分在TS中变化不大，无论转译目标是什么版本的ES，这部分代码都要进行转译。
> 2. 目前版本的ES中没有，但后续版本极有可能添加的新特性。这一部分如果转译目标为原生支持该特性的环境则转译过程中不对其进行任何修改；如果转译目标为不支持该特性的环境，可以根据当前环境支持的特性来生成模拟代码，从而在不支持该特性的环境中使用该新特性。
> 3. 最新版本的ES中已经存在，但是浏览器还没有广泛实现的特性。这就是第二点中所说的：转译目标不支持该特性的情况，此时生成模拟代码即可；后续随着宿主环境都开始支持该特性，改变转译目标选项就可以保留原有代码，不需要转译成模拟代码。



<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/styles/monokai.min.css">

<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/highlight.min.js"></script>


<script>
hljs.configure({
  languages: ['cs']
})
hljs.initHighlightingOnLoad();
</script>