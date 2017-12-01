# 动态生成测试用例

使用`Function.prototype.call`和函数表达式来定义运行在Mocha中的单元测试套件和测试用例，可以直接动态生成你需要的测试用例。不必使用特殊的语法，仅使用纯js对象就可以建立类似函数式和“参数化”的测试用例。一些其他的框架就利用了这个特性。

>译注:就是将测试用例的参数用一个集合代替，从而生成不同的测试用例。

请看下面的例子:

```js
var assert = require('chai').assert;

function add() {
  return Array.prototype.slice.call(arguments).reduce(function(prev, curr) {
    return prev + curr;
  }, 0);
}

describe('add()', function() {

  //3个测试用例所用的参数，合为一个参数和结果的集合
  var tests = [
    {args: [1, 2],       expected: 3},
    {args: [1, 2, 3],    expected: 6},
    {args: [1, 2, 3, 4], expected: 10}
  ];

  //遍历集合，集合中每个元素生成一个测试用例
  tests.forEach(function(test) {
    it('correctly adds ' + test.args.length + ' args', function() {
      var res = add.apply(null, test.args);
      assert.equal(res, test.expected);
    });
  });
});
```

上面的代码产生了一个单元测试套件，包含了三个测试用例:

```js
$ mocha

  add()
    ✓ correctly adds 2 args
    ✓ correctly adds 3 args
    ✓ correctly adds 4 args
```

