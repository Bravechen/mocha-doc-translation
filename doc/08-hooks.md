# 钩子函数

在默认的BDD风格接口中，Mocha提供了一些钩子函数:`before()`、`after()`、`beforeEach()`和`afterEach()`。这些函数将会在测试的预处理阶段被调用，并在测试后被销毁。

```js
describe('hooks', function() {

  before(function() {
    //在所有测试之前运行
  });

  after(function() {
    //在所有测试之后运行
  });

  beforeEach(function() {
    //在每个测试运行前执行
  });

  afterEach(function() {
    //在每个测试运行后执行
  });

  //测试用例
});
```

>钩子函数会在测试之前或测试之后执行，也会在每个测试之间执行。总之会按照被定义的方式在合适时间被执行。所有的`before()`钩子会在一开始执行一次，紧接着是执行每个测试的`beforeEach()`钩子，然后执行测试，再接着执行每个`afterEach()`钩子，最后执行一次`after()`钩子。

## 描述钩子函数

每个钩子函数都可以有一个可选的描述文字，以便在测试中快速的定位错误。如果提供的钩子是一个具名函数，那么在没有设置描述的情况下，函数名字将会被作为该钩子的描述。

```js
beforeEach(function() {
  // beforeEach hook
});

beforeEach(function namedFun() {
  // beforeEach:namedFun
});

beforeEach('some description', function() {
  // beforeEach:some description
});
```

## 异步钩子函数

所有的钩子函数(`before(), after(), beforeEach(), afterEach()`)既可以是同步的也可以是异步的，和普通的测试用例差不多。举例来说，你可能想要在每个测试之前为数据库填充入一些假数据：

```js
describe('Connection', function() {
  var db = new Connection,
    tobi = new User('tobi'),
    loki = new User('loki'),
    jane = new User('jane');

  beforeEach(function(done) {
    db.clear(function(err) {
      if (err) return done(err);
      db.save([tobi, loki, jane], done);
    });
  });

  describe('#find()', function() {
    it('respond with matching records', function(done) {
      db.find({type: 'User'}, function(err, res) {
        if (err) return done(err);
        res.should.have.length(3);
        done();
      });
    });
  });
});
```

## 根级钩子

你可以在任何文件中加入“根级”钩子函数。例如，在所有的`describe()`代码块之外添加`beforeEach()`。这会造成在每个测试进行之前都调用一次`beforeEach()`函数的回调函数，而无论这段代码在哪个文件之中（如此现象是因为在内部Mocha提供了一段隐式的`describe()`代码，可以被称作“根级单元测试套件”(`root suite`)）。

```js
beforeEach(function() {
  console.log('before every test in every file');
});
```
## 推迟 root suite

如果你需要在单元测试套件运行之前执行一些异步操作，也可以推迟`root suite`的运行。在启动Mocha时加上`--delay`参数，就可以在全局上下文对象中获得一个附加的回调函数`run()`。

```js
setTimeout(function() {
  // do some setup

  describe('my suite', function() {
    // ...
  });

  run();
}, 5000);
``` 

>译注:
>- beforeEach会对当前describe下的所有子case生效。
>- before和after的代码没有特殊顺序要求。
>- 同一个describe下可以有多个before，执行顺序与代码顺序相同。
>- 同一个describe下的执行顺序为before, beforeEach, afterEach, after
>- 当一个it有多个before的时候，执行顺序从最外围的describe的before开始，其余同理。



