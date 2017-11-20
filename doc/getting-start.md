# 快速开始使用

## 1.指定测试文件

```
$ npm install mocha
$ mkdir test
$ $EDITOR test/test.js # or open with your favorite editor
```

## 2.编写测试用例

在编辑器中输入:

```js
var assert = require('assert');

describe('Array', function() {
  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      assert.equal(-1, [1,2,3].indexOf(4));
    });
  });
});
```
## 3. 在终端运行测试

然后再终端中：

```
$ ./node_modules/mocha/bin/mocha

  Array
    #indexOf()
      ✓ should return -1 when the value is not present


  1 passing (9ms)
```

### 可以在`package.json`中编写测试脚本

```json
//...
"scripts": {
    "test": "mocha"
},

//...
```

## 4.输出测试结果

```
$ npm test
```
