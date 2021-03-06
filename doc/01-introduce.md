# 介绍

Mocha是一个具有多种功能的JavaScript测试框架，可以运行在Node.js和浏览器中。它可以简化异步测试，并且使用便捷。使用Mocha进行测试，可以持续、弹性和精确的报告未捕获的错误，并不断的促进开发者修正测试用例。[项目GiHub地址](https://github.com/mochajs/mocha)

## 特性
|特性|特性|
|--|--|
|支持浏览器中测试|全局污染侦测|
|简便的异步支持，支持`Promise`|可选的正则表达式测试|
|测试覆盖率报告|死循环自动退出机制|
|字符串对比支持|便捷的` meta-generate`套件和测试用例|
|使用JS API运行测试|支持配置文件`mocha.opts`|
|为持续集成(`CI`)提供恰当的接口|单击测试条件标题可以过滤测试用例|
|auto-detects and disables coloring for non-ttys|支持node调试器|
|罗列异常修正测试用例|detects multiple calls to `done()`|
|支持异步测试计时|支持第三方断言测试库|
|支持测试重试|extensible reporting, bundled with 9+ reporters|
|test-specific timeouts|extensible test DSLs or “interfaces”|
|支持警告异常通知|`before`, `after`, `before each`, `after each` 四种钩子函数|
|测试用时报告|支持第三方语言转译器|
|高亮耗时测试|编辑器绑定|
|文件变化监控|还有更多！|

## 目录

- 安装
- 快速开始
- 断言
- 异步代码测试
- 同步代码测试
- 箭头函数
- 钩子函数
- 待定测试 Pending Tests
- 专有测试 Exclusive Tests
- 包容性测试 Inclusive Tests
- 测试重试 Retry Tests
- 动态生成测试用例
- TIMEOUTS
- Diffs
- 命令行使用方法
- 接口
- 报告
- 在浏览器中使用Mocha
- `mocha.opts`
- `test`目录
- Editor Plugins
- Examples
- Testing Mocha
- More Information