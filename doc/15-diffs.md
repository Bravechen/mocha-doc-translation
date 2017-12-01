# DIFFS

Mocha提供了`err.expected`和`err.actual`属性，包含了从第三方断言库中抛出的任何`AssertionError`类型错误信息。`Mocha`将会尝试用不同的显示方式展示期望的结果，以及断言实际产生的结果。下面的例子展示了一个"string"对比：

![image](https://raw.githubusercontent.com/Bravechen/blog-dir/master/assets/reporter-string-diffs.png);

