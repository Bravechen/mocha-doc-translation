# 包容性测试 INCLUSIVE TESTS

包容性测试正好与`.only()`相反。通过添加`.skip()`，我们可以让Mocha简单的忽略这些单元测试套件和测试用例。任何被略过的测试都会被记录为`pending`状态，之后会被写入报告。这里有一个例子，展示了跳过全部测试的结果：

```js
describe('Array', function() {
  describe.skip('#indexOf()', function() {
    // ...
  });
});
```

或者调过一个特定的测试用例：

```js
describe('Array', function() {
  describe('#indexOf()', function() {
    it.skip('should return -1 unless present', function() {
      //测试不会被执行
    });

    it('should return the index when present', function() {
      //测试会被执行
    });
  });
});
```

>最佳实践：使用`.skip()`替代注释掉某个测试的操作。


你还可以在运行时使用`.skip()`跳过测试。如果一项测试所用的环境或者配置没有准备好，那么此时在运行时跳过他是合适的。例如：

```js
it('should only test in the correct environment', function() {
  if (/* check test environment */) {
    // make assertions
  } else {
    this.skip();
  }
});
```

上面的测试将会以`pending`的状态写入报告。还有一项重点关注的是，调用`this.skip()`，实际上是中止这项测试。

>最佳实践：为了避免混乱，注意不要在测试用例和钩子函数中先调用`this.skip()`之后，再去安排执行其他指令。

看看下面的例子，来对比一下：

```js
it('should only test in the correct environment', function() {
  if (/* check test environment */) {
    // make assertions
  } else {
    // do nothing
  }
});
```

因为这项测试没有执行任何有效代码，它将会被报告为通过。

>最佳实践：不要做这种无用功！一项测试至少应该进行一次断言或者直接使用`this.skip()`。

如果需要以这种方式跳过多项测试，可以在一个`"before"`钩子中使用`this.skip()`：

```js
before(function() {
  if (/* check test environment */) {
    // setup code
  } else {
    this.skip();
  }
});
```

>在早于Mocha v3.0.0的版本中，`this.skip()`不能在异步测试和钩子函数中使用。



