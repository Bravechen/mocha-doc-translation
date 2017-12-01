## 待定测试 `pending test`

"Pending"是指那些省去测试细节的测试用例，隐含意义是“最终会有人来写的测试用例”。

```js
describe('Array', function() {
  describe('#indexOf()', function() {
    // pending test below
    it('should return -1 when the value is not present');
  });
});
```

`pending tests`会按照提供的描述被写入报告。

一般适用情况比如负责测试框架的写好框架让组员去实现细节，或者测试细节尚未完全正确实现先注释以免影响全局测试情况。这种时候mocha会默认该测试pass。
