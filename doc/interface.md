# 接口

Mocha’s “interface” system allows developers to choose their style of DSL. Mocha has BDD, TDD, Exports, QUnit and Require-style interfaces.

Mocha的"接口"(`interface`)系统允许开发者选择不同的DSL风格。有`BDD`、`TDD`、`Exports`、`QUnit`和`require`风格的接口供选择。

## BDD

The BDD interface provides describe(), context(), it(), specify(), before(), after(), beforeEach(), and afterEach().

BDD风格提供了`describe(), context(), it(), specify(), before(), after(), beforeEach(),afterEach()`等方法。

context() is just an alias for describe(), and behaves the same way; it just provides a way to keep tests easier to read and organized. Similarly, specify() is an alias for it().

`context()`仅仅是`describe()`的一个别名，行为是相同的。它为测试提供了简单的可读性和组织性。类似的，`specify()`是`it()`的一个别名。

>All of the previous examples were written using the BDD interface.
>本手册之前的例子都是使用BDD风格的测试接口写就的。

```js
 describe('Array', function() {
    before(function() {
      // ...
    });

    describe('#indexOf()', function() {
      context('when not present', function() {
        it('should not throw an error', function() {
          (function() {
            [1,2,3].indexOf(4);
          }).should.not.throw();
        });
        it('should return -1', function() {
          [1,2,3].indexOf(4).should.equal(-1);
        });
      });
      context('when present', function() {
        it('should return the index where the element first appears in the array', function() {
          [1,2,3].indexOf(3).should.equal(2);
        });
      });
    });
  });
```

## TDD

The TDD interface provides suite(), test(), suiteSetup(), suiteTeardown(), setup(), and teardown():

TDD风格的接口提供了`suite(), test(), suiteSetup(), suiteTeardown(), setup(),teardown()`等方法：

```js
suite('Array', function() {
  setup(function() {
    // ...
  });

  suite('#indexOf()', function() {
    test('should return -1 when not present', function() {
      assert.equal(-1, [1,2,3].indexOf(4));
    });
  });
});
```

## EXPORTS

The Exports interface is much like Mocha’s predecessor expresso. The keys before, after, beforeEach, and afterEach are special-cased, object values are suites, and function values are test-cases:

`Exports`风格的接口很像Mocha的前辈[`expresso`](https://github.com/tj/expresso)。键名`before, after, beforeEach, afterEach`是指定的用例，object对象实例相当于suite，而函数类型的键值就是测试用例：

```js
module.exports = {
  before: function() {
    // ...
  },

  'Array': {
    '#indexOf()': {
      'should return -1 when not present': function() {
        [1,2,3].indexOf(4).should.equal(-1);
      }
    }
  }
};
```

## QUNIT

The QUnit-inspired interface matches the “flat” look of QUnit, where the test suite title is simply defined before the test-cases. Like TDD, it uses suite() and test(), but resembling BDD, it also contains before(), after(), beforeEach(), and afterEach().

[QUint](http://qunitjs.com/) 风格的接口中，需要把suite的标题定义在测试用例之前。类似TDD，它有`suite(),test()`方法，并且兼具BDD风格的一些方法:`before(), after(), beforeEach(), afterEach()`。

```js
function ok(expr, msg) {
  if (!expr) throw new Error(msg);
}

suite('Array');

test('#length', function() {
  var arr = [1,2,3];
  ok(arr.length == 3);
});

test('#indexOf()', function() {
  var arr = [1,2,3];
  ok(arr.indexOf(1) == 0);
  ok(arr.indexOf(2) == 1);
  ok(arr.indexOf(3) == 2);
});

suite('String');

test('#length', function() {
  ok('foo'.length == 3);
});
```

## REQUIRE

The require interface allows you to require the describe and friend words directly using require and call them whatever you want. This interface is also useful if you want to avoid global variables in your tests.

`require`风格允许你加载`describe`，并且友好的支持直接在任何你需要地方使用`require`方法。这种风格对于想要在测试中避免设置全局变量的问题很有用。

Note: The require interface cannot be run via the node executable, and must be run via mocha.

注意：`require`接口不能简单的使用node方式使用，一定要通过加载mocha的方式

```js
var testCase = require('mocha').describe;
var pre = require('mocha').before;
var assertions = require('mocha').it;
var assert = require('chai').assert;

testCase('Array', function() {
  pre(function() {
    // ...
  });

  testCase('#indexOf()', function() {
    assertions('should return -1 when not present', function() {
      assert.equal([1,2,3].indexOf(4), -1);
    });
  });
});
```