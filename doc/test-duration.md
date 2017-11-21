# TEST DURATION
# 测试耗时计算

Many reporters will display test duration, as well as flagging tests that are slow, as shown here with the “spec” reporter:
许多报告都会显示测试的时长。如果有测试被标记为缓慢耗时的，那么会使用特定的显示方式来表明：

![image]()

To tweak what’s considered “slow”, you can use the slow() method:

```js
describe('something slow', function() {
  this.slow(10000);

  it('should take long enough for me to go make a sandwich', function() {
    // ...
  });
});
```