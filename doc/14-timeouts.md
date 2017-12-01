# TIMEOUTS

## 单元测试级别 SUITE-LEVEL

单元测试套件级别的超时设定将会在整个单元测试中起作用，可以通过使用`this.timeout(0)`来禁用。全局的设定会被所有的嵌套单元测试套件和测试用例继承，并且不能改变全局的设定值。

```js
describe('a suite of tests', function() {
  this.timeout(500);

  it('should take less than 500ms', function(done){
    setTimeout(done, 300);  //不能设置超过500
  });

  it('should take less than 500ms as well', function(done){
    setTimeout(done, 250);  //不能设置超过500
  });
})
```

## 测试用例级别 TEST-LEVEL

超时设定也可以在某一项测试用例中使用，也能用`this.timeout(0)`进行禁用。

```js
it('should take less than 500ms', function(done){
  this.timeout(500);
  setTimeout(done, 300);  //不能设置超过500
});

```

## 钩子函数级别 HOOK-LEVEL

在钩子函数中也可以使用超时设定:

```js
describe('a suite of tests', function() {
  beforeEach(function(done) {
    this.timeout(3000);     // 假设需要很长一段时间启动环境
    setTimeout(done, 2500);
  });
});
```

别忘了，可以使用`this.timeout(0)`在钩子函数禁用`timeout`。

>在v3.0.0之后的版本中，如果`this.timeout()`的参数大于[最大延迟时间](https://developer.mozilla.org/docs/Web/API/WindowTimers/setTimeout#Maximum_delay_value)(`the maximum delay`)将会造成禁用`timeout`的结果。


