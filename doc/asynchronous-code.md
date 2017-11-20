# 异步代码测试

Testing asynchronous code with Mocha could not be simpler! Simply invoke the callback when your test is complete. By adding a callback (usually named done) to it(), Mocha will know that it should wait for this function to be called to complete the test.

在Mocha中测试异步代码简单的不能再简单！你只用关心在测试完成时的回调函数即可。通过为`it()`添加回调函数(函数的参数通常我们把它命名为`done`)，Mocha将会在此函数调用时，完成本次测试。

```js
describe('User', function() {
  describe('#save()', function() {
    it('should save without error', function(done) {
      var user = new User('Luna');
      user.save(function(err) {
        if (err) done(err);
        else done();
      });
    });
  });
});
```

To make things even easier, the done() callback accepts an error, so we may use this directly:

`done()`回调函数可以接受一个名为`error`的参数，因此更简单的做法，事直接使用它:

```js
describe('User', function() {
  describe('#save()', function() {
    it('should save without error', function(done) {
      var user = new User('Luna');
      user.save(done);
    });
  });
});

```

## 使用Promise

Alternately, instead of using the done() callback, you may return a Promise. This is useful if the APIs you are testing return promises instead of taking callbacks:

换一种方式，你也可以使用Promise。这对于那些能够返回promise的待测试API们非常有用。

```js
beforeEach(function() {
  return db.clear()
    .then(function() {
      return db.save([tobi, loki, jane]);
    });
});

describe('#find()', function() {
  it('respond with matching records', function() {
    return db.find({ type: 'User' }).should.eventually.have.length(3);
  });
});
```
>The latter example uses Chai as Promised for fluent promise assertions.

>后面的例子中也有使用[`chai-as-promised`](https://www.npmjs.com/package/chai-as-promised)实现的promise流式断言测试

In Mocha v3.0.0 and newer, returning a Promise and calling done() will result in an exception, as this is generally a mistake:
在Mocha v3.0.0和更高版本，使用返回的Promise并调用`done()`函数是不允许的，会报一个错误：

```js
const assert = require('assert');

it('should complete this test', function (done) {
  return new Promise(function (resolve) {
    assert.ok(true);
    resolve();
  })
    .then(done);
});
```
The above test will fail with Error: Resolution method is overspecified. Specify a callback *or* return a Promise; not both.. In versions older than v3.0.0, the call to done() is effectively ignored.

上面的测试会失败并产生一个错误`Error: Resolution method is overspecified. Specify a callback *or* return a Promise; not both.`。在低于`v3.0.0`的版本中,例子中调用的`done()`会被忽略。

## 使用`async/await`

If your JS environment supports async / await you can also write asynchronous tests like this:

如果你的js运行环境支持`async/await`，那么你也可以这样使用异步测试：

```js
beforeEach(async function() {
  await db.clear();
  await db.save([tobi, loki, jane]);
});

describe('#find()', function() {
  it('responds with matching records', async function() {
    const users = await db.find({ type: 'User' });
    users.should.have.length(3);
  });
});
```

