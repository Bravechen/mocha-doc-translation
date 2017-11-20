# 箭头函数

Passing arrow functions (“lambdas”) to Mocha is discouraged. Due to the lexical binding of this, such functions are unable to access the Mocha context. For example, the following code will fail due to the nature of lambdas:

在Mocha测试中并不建议使用箭头函数("lambdas")。由于它绑定了作用域中的`this`，因此测试函数无法获取到Mocha的上下文对象。举例来说，
以下代码由于lambdas的特性，将会失败:

```js
describe('my suite', () => {
  it('my test', () => {
    // should set the timeout of this test to 1000 ms; instead will fail
    this.timeout(1000);
    assert.ok(true);
  });
});
```

If you do not need to use Mocha’s context, lambdas should work. However, the result will be more difficult to refactor if the need eventually arises.

如果你不需要使用Mocha的上下文对象，lambdas当然能够正常运行。然而，如果最终需求改变，重构将会是非常困难的。