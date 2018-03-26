### TS特性解析及转译

#### @decorator
> 1. decorator（装饰器）是 ES2016（即ES7）引入的新特性，
```js
var __decorate = (this && this.__decorate) || function (decorators, target, key, desc) {
    if (typeof Reflect === 'object' && typeof Reflect.decorate === 'function') {
        r = Reflect.decorate(decorators, target, key, desc);
    } else {
        var c = arguments.length;
        // r 用于存储适用多个装饰器时候的 中间值
        // c < 3时，进行类装饰器操作， r存储中间 target 对象；
        // c >= 3时， desc传入null时执行 方法装饰器 操作 r为 属性的 描述符对象
        // c >=3时， desc不为null， 执行 属性装饰器 操作 r 为 undefined 或者 属性的描述符对象
        var r = c < 3 ? target : desc === null ? desc = Object.getOwnPropertyDescriptor(target, key) : desc;
        var d;

        for (var i = decorators.length - 1; i >= 0; i--) {
            if (d = decorators[i]) {
                r = (c < 3 ?  d(r) : c > 3 ? d(target, key, r) : d(target, key)) || r;
            }
        }
    }
    return c > 3 && r && Object.defineProperty(target, key, r), r;
}
```