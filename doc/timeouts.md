# TIMEOUTS
# 超时设定

## SUITE-LEVEL

Suite-level timeouts may be applied to entire test “suites”, or disabled via this.timeout(0). This will be inherited by all nested suites and test-cases that do not override the value.

suite级别的超时设定将会在整个测试suite中起作用，可以通过使用`this.timeout(0)`来禁用。全局的设定会被所有的嵌套suite和测试用例继承，并且不能改变全局的设定值。

```js
describe('a suite of tests', function() {
  this.timeout(500);

  it('should take less than 500ms', function(done){
    setTimeout(done, 300);
  });

  it('should take less than 500ms as well', function(done){
    setTimeout(done, 250);
  });
})
```

## TEST-LEVEL

Test-specific timeouts may also be applied, or the use of this.timeout(0) to disable timeouts all together:
超时设定也可以在某一项测试中使用，也能用`this.timeout(0)`进行禁用。

```js
it('should take less than 500ms', function(done){
  this.timeout(500);
  setTimeout(done, 300);
});

```

## HOOK-LEVEL

Hook-level timeouts may also be applied:

在钩子函数中也可以使用超时设定:

```js
describe('a suite of tests', function() {
  beforeEach(function(done) {
    this.timeout(3000); // A very long environment setup.
    setTimeout(done, 2500);
  });
});
```
Again, use this.timeout(0) to disable the timeout for a hook.
别忘了，可以使用`this.timeout(0)`在钩子函数禁用`timeout`

>In v3.0.0 or newer, a parameter passed to this.timeout() greater than the maximum delay value will cause the timeout to be disabled.
>在v3.0.0之后的版本中，如果`this.timeout()`的参数大于[最大延迟时间](https://developer.mozilla.org/docs/Web/API/WindowTimers/setTimeout#Maximum_delay_value)(`the maximum delay`)将会造成禁用`timeout`的结果。


