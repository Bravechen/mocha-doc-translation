# RETRY TESTS

You can choose to retry failed tests up to a certain number of times. This feature is designed to handle end-to-end tests (functional tests/Selenium…) where resources cannot be easily mocked/stubbed. It’s not recommended to use this feature for unit tests.

对于已经失败的测试，也可以选择对他们进行重试，并且设定重试次数。这项特性是用来解决在端对端测试（functional tests/Selenium…）中，某些资源难以模拟或者存档(mocked/stubbed)的情况下出现的问题。在单元测试中，是不推荐使用这个的。

This feature does re-run beforeEach/afterEach hooks but not before/after hooks.

这项特性可以在`beforeEach/afterEach`钩子中使用，但是不能在`before/after`钩子中使用。

NOTE: Example below was written using Selenium webdriver (which overwrites global Mocha hooks for Promise chain).
注意：下面的例子中，我们用到了`Selenium webdriver`（在内部，它使用Promise链重写了Mocha的全局钩子函数）。

```js
describe('retries', function() {
  // Retry all tests in this suite up to 4 times
  this.retries(4);

  beforeEach(function () {
    browser.get('http://www.yahoo.com');
  });

  it('should succeed on the 3rd try', function () {
    // Specify this test to only retry up to 2 times
    this.retries(2);
    expect($('.foo').isDisplayed()).to.eventually.be.true;
  });
});
```