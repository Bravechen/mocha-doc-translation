# 专有测试(`exclusive tests`)

专有测试特性允许你运行一个指定的单元测试套件或者测试用例，方式是在函数后添加一个`.only()`。下面的例子中就执行了一个这样特殊单元测试套件：

```js
describe('Array', function() {
  describe.only('#indexOf()', function() {
    // ...
  });
});
```

注意：所有嵌套的单元测试套件仍然会被执行。

举一个执行专有测试用例的例子：

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

>译注：上面的代码只会有一个test complete， 只有only的会被执行，另一个会被忽略掉。**每个it 回调函数里只能有一个only**

在`v3.0.0`之前，`.only()`使用字符串匹配决定哪个测试会被执行。到了`v3.0.0`，机制发生了改变。`.only()`可以作为测试的子集而被多次调用:

```js
describe('Array', function() {
  describe('#indexOf()', function() {
    it.only('should return -1 unless present', function() {
      //测试会被运行
    });

    it.only('should return the index when present', function() {
      //测试同样会被运行
    });

    it('should return -1 if called with a non-Array context', function() {
      //这个测试不会被运行
    });
  });
});
```

>译注：每个it 回调函数里只能有一个only。上面的代码中，两个有`.only()`的`it`会被执行，而另一个将会被忽略掉

你还可以使用在多个单元测试套件中：

```js
describe('Array', function() {
  describe.only('#indexOf()', function() {
    it('should return -1 unless present', function() {
      // 测试会被运行
    });

    it('should return the index when present', function() {
      // 这个测试也会被执行
    });
  });

  describe.only('#concat()', function () {
    it('should return a new Array', function () {
      // 这个测试也会被执行
    });
  });

  describe('#slice()', function () {
    it('should return a new Array', function () {
      // 这个测试不会被执行
    });
  });
});
```

>译注：对于使用了`only`的测试会被专门执行，没有调用`.only()`将会被忽略

但，专有测试会优先执行：

```js
describe('Array', function() {
  describe.only('#indexOf()', function() {
    it.only('should return -1 unless present', function() {
      // 这个测试会被执行
    });

    it('should return the index when present', function() {
      // 这个测试不会被执行
    });
  });
});
```

注意：如果存在钩子，他们还是会被执行的。

>Be mindful not to commit usages of .only() to version control, unless you really mean it!
>尽量不要提交`.only()`的部分到版本控制中，除非你真的需要他们！（？？？）





