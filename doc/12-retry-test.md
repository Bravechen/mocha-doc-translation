# 测试重试 RETRY TESTS

对于已经失败的测试，也可以选择对他们进行重试，并且设定重试次数。这项特性是用来解决在端对端测试（functional tests/Selenium…）中，某些资源难以模拟或者存档(mocked/stubbed)的情况下出现的问题。在单元测试中，是不推荐使用这个的。

这项特性可以在`beforeEach/afterEach`钩子中使用，但是不能在`before/after`钩子中使用。

注意：下面的例子中，我们用到了`Selenium webdriver`（在内部，它使用Promise链重写了Mocha的全局钩子函数）。

```js
describe('retries', function() {
  //在这个单元测试中重复所有测试用例4次
  this.retries(4);

  beforeEach(function () {
    browser.get('http://www.yahoo.com');
  });

  it('should succeed on the 3rd try', function () {
    // 指定这项测试单独重复测试2次
    this.retries(2);
    expect($('.foo').isDisplayed()).to.eventually.be.true;
  });
});
```