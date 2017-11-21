# DYNAMICALLY GENERATING TESTS
# 动态生成测试

Given Mocha’s use of Function.prototype.call and function expressions to define suites and test cases, it’s straightforward to generate your tests dynamically. No special syntax is required — plain ol’ JavaScript can be used to achieve functionality similar to “parameterized” tests, which you may have seen in other frameworks.

使用`Function.prototype.call`和函数表达式来定义运行在Mocha中的suite和测试用例，可以直接生成你需要的动态测试。不必使用特殊的语法，仅使用纯js对象就可以建立类似函数式和“参数化”的测试用例。一些其他的框架就利用了这个特性。

Take the following example:
请看下面的例子:

```js
var assert = require('chai').assert;

function add() {
  return Array.prototype.slice.call(arguments).reduce(function(prev, curr) {
    return prev + curr;
  }, 0);
}

describe('add()', function() {
  var tests = [
    {args: [1, 2],       expected: 3},
    {args: [1, 2, 3],    expected: 6},
    {args: [1, 2, 3, 4], expected: 10}
  ];

  tests.forEach(function(test) {
    it('correctly adds ' + test.args.length + ' args', function() {
      var res = add.apply(null, test.args);
      assert.equal(res, test.expected);
    });
  });
});
```

The above code will produce a suite with three specs:
上面的代码产生了一个suite，包含了三个测试:

```js
$ mocha

  add()
    ✓ correctly adds 2 args
    ✓ correctly adds 3 args
    ✓ correctly adds 4 args
```

