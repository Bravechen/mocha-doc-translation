# 异步代码测试

在Mocha中测试异步代码简单到不能再简单！你只用关心在测试完成时的回调函数即可。通过为`it()`添加回调函数(函数的参数通常我们把它命名为`done`)，Mocha将会在此函数调用时，完成本次测试。

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
>译注：

`done ()`,按照瀑布流编程习惯，取名`done`是表示你回调的最深处，也就是结束写嵌套回调函数。但对于回调链来说`done`实际上意味着告诉mocha从此处开始测试，一层层回调回去。


`done()`回调函数可以接受一个名为`error`的参数，因此更简单的做法是直接使用它:

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
>译注：

假如我有两个异步函数（两条分叉的回调链），那我应该在哪里加done()呢？实际上这个时候就不应该在一个it里面存在两个要测试的函数，事实上**一个it里面只能调用一次done**，当你调用多次done的话mocha会抛出错误。所以应该类似这样：

```js
fs = require('fs');  
describe('File', function(){  
    describe('#readFile()', function(){  
        it('should read test.ls without error', function(done){  
            fs.readFile('test.ls', function(err){  
                if (err) throw err;  
                done();  
            });  
        })  
        it('should read test.js without error', function(done){  
            fs.readFile('test.js', function(err){  
                if (err) throw err;  
                done();  
            });  
        })  
    })  
})  
```

## 使用Promise

换一种方式，你也可以使用Promise。这对于那些能够返回promise的待测试API非常有用。

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
>后面的例子中也有使用[`chai-as-promised`](https://www.npmjs.com/package/chai-as-promised)实现的promise流式断言测试

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

上面的测试会失败并产生一个错误`Error: Resolution method is overspecified. Specify a callback *or* return a Promise; not both.`。在低于`v3.0.0`的版本中,例子中调用的`done()`会被忽略。

## 使用`async/await`

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

