# 快速开始使用

## 1.指定测试文件

```
$ npm install mocha
$ mkdir test
$ $EDITOR test/test.js # 或者打开你喜欢的编辑器
```

## 2.编写测试代码

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
>译注:

- `describe (moduleName, testDetails) `
由上述代码可看出，`describe`是可以嵌套的，比如上述代码嵌套的两个`describe`就可以理解成测试人员希望测试`Array`模块下的`#indexOf() `子模块。`module_name `是可以随便取的，关键是要让人读明白就好。

- `it (info, function)` 
具体的测试语句会放在it的回调函数里，一般来说`info`字符串会写期望的正确输出的简要一句话文字说明。当该`it`代码块内的测试失败的时候控制台就会把详细信息打印出来。一般是从最外层的`describe`的`module_name`开始输出（可以理解成沿着路径或者递归链或者回调链），最后输出`info`，表示该期望的`info`内容没有被满足。一个`it`对应一个实际的测试用例(`test case`)。


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
