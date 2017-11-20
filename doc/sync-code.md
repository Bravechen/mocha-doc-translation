# 同步代码测试

When testing synchronous code, omit the callback and Mocha will automatically continue on to the next test.

测试同步代码，不需要回调函数，Mocha会自动执行每个测试。

```js
describe('Array', function() {
  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      [1,2,3].indexOf(5).should.equal(-1);
      [1,2,3].indexOf(0).should.equal(-1);
    });
  });
});
```