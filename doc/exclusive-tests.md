# EXCLUSIVE TESTS
# 互斥测试?

The exclusivity feature allows you to run only the specified suite or test-case by appending .only() to the function. Here’s an example of executing only a particular suite:

专有特性允许你运行一个指定的suite或者测试用例，方式是在函数后添加一个`.only()`。下面的例子中就执行了一个这样特殊suite：

```js
describe('Array', function() {
  describe.only('#indexOf()', function() {
    // ...
  });
});
```

Note: All nested suites will still be executed.

注意：所有嵌套的suite仍然会被执行。

Here’s an example of executing an individual test case:
举一个执行独立测试用例的例子：

```js
describe('Array', function() {
  describe('#indexOf()', function() {
    it.only('should return -1 unless present', function() {
      // ...
    });

    it('should return the index when present', function() {
      // ...
    });
  });
});
```

Previous to v3.0.0, .only() used string matching to decide which tests to execute. As of v3.0.0, this is no longer the case. In v3.0.0 or newer, .only() can be used multiple times to define a subset of tests to run:

在`v3.0.0`之前，`.only()`使用字符串匹配决定哪个测试会被执行。到了`v3.0.0`，机制发生了改变。`.only()`可以作为测试的子集而被多次调用:

```js
describe('Array', function() {
  describe('#indexOf()', function() {
    it.only('should return -1 unless present', function() {
      // this test will be run
      //测试会被运行
    });

    it.only('should return the index when present', function() {
      // this test will also be run
      //测试同样会被运行
    });

    it('should return -1 if called with a non-Array context', function() {
      // this test will not be run
      //这个测试不会被运行
    });
  });
});
```

You may also choose multiple suites:

你还可以选择多种suite：

```js
describe('Array', function() {
  describe.only('#indexOf()', function() {
    it('should return -1 unless present', function() {
      // this test will be run
      // 测试会被运行
    });

    it('should return the index when present', function() {
      // this test will also be run
      // 这个测试也会被执行
    });
  });

  describe.only('#concat()', function () {
    it('should return a new Array', function () {
      // this test will also be run
      // 这个测试也会被执行
    });
  });

  describe('#slice()', function () {
    it('should return a new Array', function () {
      // this test will not be run
      // 这个测试不会被执行
    });
  });
});
```

But tests will have precedence:

但，测试也需要区分优先级：

```js
describe('Array', function() {
  describe.only('#indexOf()', function() {
    it.only('should return -1 unless present', function() {
      // this test will be run
    });

    it('should return the index when present', function() {
      // this test will not be run
    });
  });
});
```
Note: Hooks, if present, will still be executed.

注意：如果存在钩子，他们还是会被执行的。

>Be mindful not to commit usages of .only() to version control, unless you really mean it!
>尽量不要提交`.only()`的部分到版本控制中，除非你真的需要他们！（？？？）





