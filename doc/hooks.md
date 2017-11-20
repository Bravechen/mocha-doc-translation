# 钩子函数

With its default “BDD”-style interface, Mocha provides the hooks before(), after(), beforeEach(), and afterEach(). These should be used to set up preconditions and clean up after your tests.

在默认的BDD风格接口中，Mocha提供了一些钩子函数:`before()`、`after()`、`beforeEach()`和`afterEach()`。这些函数将会在测试的预处理阶段被调用，并在测试后被销毁。

```js
describe('hooks', function() {

  before(function() {
    // runs before all tests in this block
    //在所有测试之前运行
  });

  after(function() {
    // runs after all tests in this block
    //在所有测试之后运行
  });

  beforeEach(function() {
    // runs before each test in this block
    //在每个测试运行前执行
  });

  afterEach(function() {
    // runs after each test in this block
    //在每个测试运行后执行
  });

  // test cases
  //测试用例
});
```

>Tests can appear before, after, or interspersed with your hooks. Hooks will run in the order they are defined, as appropriate; all before() hooks run (once), then any beforeEach() hooks, tests, any afterEach() hooks, and finally after() hooks (once).

>钩子函数会在测试之前，之后执行，也会在每个测试之间执行。按照被定义的方式在合适时间被执行，所有的`before()`钩子会在一开始执行一次，紧接着是执行每个测试的`beforeEach()`钩子，然后执行测试，再接着执行每个`afterEach()`钩子，最后执行一次`after()`钩子。

## 描述钩子函数

Any hook can be invoked with an optional description, making it easier to pinpoint errors in your tests. If a hook is given a named function, that name will be used if no description is supplied.

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

All hooks (before(), after(), beforeEach(), afterEach()) may be sync or async as well, behaving much like a regular test-case. For example, you may wish to populate database with dummy content before each test:

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

You may also pick any file and add “root”-level hooks. For example, add beforeEach() outside of all describe() blocks. This will cause the callback to beforeEach() to run before any test case, regardless of the file it lives in (this is because Mocha has an implied describe() block, called the “root suite”).

你可以在任何文件中加入“根级”钩子函数。例如，在所有的`describe()`代码块之外添加`beforeEach()`。这会造成在每个测试进行之前都调用一次`beforeEach()`函数的回调函数，而无论这段代码再那个文件之中（如此现象是因为在内部Mocha提供了一段隐式的`describe()`代码，可以被称作“root suite”）。

```js
beforeEach(function() {
  console.log('before every test in every file');
});
```
## 推迟 root suite

If you need to perform asynchronous operations before any of your suites are run, you may delay the root suite. Run mocha with the --delay flag. This will attach a special callback function, run(), to the global context:

如果你需要在测试套件运行之前执行一些异步操作，也可以推迟根级套件的运行。在启动Mocha时加上`--delay`参数，就可以在全局上下文对象中获得一个附加的回调函数`run()`。

```js
setTimeout(function() {
  // do some setup

  describe('my suite', function() {
    // ...
  });

  run();
}, 5000);
``` 



