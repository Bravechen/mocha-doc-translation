# 接口

Mocha的"接口"(`interface`)系统允许开发者选择不同的DSL风格。有`BDD`、`TDD`、`Exports`、`QUnit`和`require`风格的接口供选择。

## BDD 行为驱动开发

BDD风格提供了`describe(), context(), it(), specify(), before(), after(), beforeEach(),afterEach()`等方法。

`context()`仅仅是`describe()`的一个别名，行为是相同的。它为测试提供了简单的可读性和组织性。类似的，`specify()`是`it()`的一个别名。

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

## TDD 测试驱动开发

TDD风格的接口提供了`suite(), test(), suiteSetup(), suiteTeardown(), setup(),teardown()`等方法：

>译注: mocha默认的模式是Behavior Driven Develop (BDD)，要想执行TDD的test的时候需要加上参数，如:
>
>`mocha -u tdd test.js `

|TDD|BDD|说明|
|--|--|--|
|`suite`|`describe`|单元测试套件|
|`test`|`it`|测试用例|
|`suiteSetup()`|``|钩子函数|
|`suiteTeardown()`|``|钩子函数|
|`setup`|`before`|钩子函数
|`teardown`|`after`|钩子函数|

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

`Exports`风格的接口很像Mocha的前辈[`expresso`](https://github.com/tj/expresso)。键名`before, after, beforeEach, afterEach`是指定的用例，object对象实例相当于单元测试套件，而函数类型的键值就是测试用例：

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

[QUint](http://qunitjs.com/) 风格的接口中，需要把单元测试套件的标题定义在测试用例之前。类似TDD，它有`suite(),test()`方法，并且兼具BDD风格的一些方法:`before(), after(), beforeEach(), afterEach()`。

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

`require`风格允许你加载`describe`，并且友好的支持直接在任何你需要地方使用`require`方法。这种风格对于想要在测试中避免设置全局变量的问题很有用。

注意：`require`接口不能简单的使用node方式使用，一定要通过加载mocha模块的方式

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