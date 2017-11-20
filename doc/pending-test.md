## PENDING TESTS

“Pending”–as in “someone should write these test cases eventually”–test-cases are simply those without a callback:

"Pending"是指那些没有回调的测试用例，意思是“最终会有人来写的测试用例”（？？？）。

```js
describe('Array', function() {
  describe('#indexOf()', function() {
    // pending test below
    it('should return -1 when the value is not present');
  });
});
```
Pending tests will be reported as such.

`pending tests`会按照提供的描述被写入报告。
