# 断言

Mocha allows you to use any assertion library you wish. In the above example, we’re using Node.js’ built-in assert module–but generally, if it throws an Error, it will work! This means you can use libraries such as:

Mocha允许你使用自己喜欢的断言库。在上一节的例子中，我们使用了Node.js内置的断言模块。试试运行一下，报错了，那就说明它在工作中！
你也可以使用一下任何一款断言库:


[should.js](https://github.com/shouldjs/should.js) - BDD风格断言库，也是本手册例子中使用的断言库
[expect.js](https://github.com/LearnBoost/expect.js) - 采用`expect()`风格的断言库
[chai](http://chaijs.com/) - 采用`expect()`、`assert()`和`should-style`断言库
[better-assert](https://github.com/visionmedia/better-assert) - C-style self-documenting assert()
[unexpected](http://unexpected.js.org/) - 可扩展的BDD断言工具库