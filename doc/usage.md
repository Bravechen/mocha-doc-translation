# USAGE

```
 Usage: mocha [debug] [options] [files]
用法：mocha [debug] [options] [files]

  Options:

    -V, --version                           output the version number
                                            输出版本号
    -A, --async-only                        force all tests to take a callback (async) or return a promise
                                            强制所有测试是使用回调函数(async)还是返回一个promise
    -c, --colors                            force enabling of colors
                                            强制启用颜色着色输出
    -C, --no-colors                         force disabling of colors
                                            强制禁用颜色着色输出
    -G, --growl                             enable growl notification support
                                            启用警告消息
    -O, --reporter-options <k=v,k2=v2,...>  reporter-specific options
                                            指定特定报告设置
    -R, --reporter <name>                   specify the reporter to use
                                            指定使用的报告
    -S, --sort                              sort test files
                                            对测试文件进行排序
    -b, --bail                              bail after first test failure
                                            在第一个测试失败时退出测试
    -d, --debug                             enable node's debugger, synonym for node --debug
                                            启用nodejs的调试器,等同于 node --debug
    -g, --grep <pattern>                    only run tests matching <pattern>
                                            只运行符合正则匹配模式的测试
    -f, --fgrep <string>                    only run tests containing <string>
                                            只执行包含指定字符串的测试
    -gc, --expose-gc                        expose gc extension

    -i, --invert                            inverts --grep and --fgrep matches
                                            反转 --grep 和 --fgrep 的匹配
    -r, --require <name>                    require the given module
                                            加载指定的模块
    -s, --slow <ms>                         "slow" test threshold in milliseconds [75]
                                            设置标记为"slow"测试的毫秒临界值 默认[75]
    -t, --timeout <ms>                      set test-case timeout in milliseconds [2000]
                                            设置测试用例的超时临界值，默认[2000]
    -u, --ui <name>                         specify user-interface (bdd|tdd|qunit|exports)
                                            设置用户界面风格，有(bdd|tdd|qunit|exports)可选
    -w, --watch                             watch files for changes
                                            监控文件变化
    --check-leaks                           check for global variable leaks
                                            检查全局污染
    --full-trace                            display the full stack trace
                                            显示全部输出栈信息
    --compilers <ext>:<module>,...          use the given module(s) to compile files
                                            使用给定的模块或模块数组编译文件
    --debug-brk                             enable node's debugger breaking on the first line

    --globals <names>                       allow the given comma-delimited global [names]
                                            允许使用逗号隔开的给定的全局名称
    --es_staging                            enable all staged features
                                            启用所有的阶段特性
    --harmony<_classes,_generators,...>     all node --harmony* flags are available
                                            启用所有给定的harmony语法标记
    --preserve-symlinks                     Instructs the module loader to preserve symbolic links when resolving and caching modules
                                            
    --icu-data-dir                          include ICU data
    --inline-diffs                          display actual/expected differences inline within each string
    --inspect                               activate devtools in chrome
    --inspect-brk                           activate devtools in chrome and break on the first line
    --interfaces                            display available interfaces
    --no-deprecation                        silence deprecation warnings
    --exit                                  force shutdown of the event loop after test run: mocha will call process.exit
    --no-timeouts                           disables timeouts, given implicitly with --debug
    --no-warnings                           silence all node process warnings
    --opts <path>                           specify opts path
    --perf-basic-prof                       enable perf linux profiler (basic support)
    --napi-modules                          enable experimental NAPI modules
    --prof                                  log statistical profiling information
    --log-timer-events                      Time events including external callbacks
    --recursive                             include sub directories
    --reporters                             display available reporters
    --retries <times>                       set numbers of time to retry a failed test case
    --throw-deprecation                     throw an exception anytime a deprecated function is used
    --trace                                 trace function calls
    --trace-deprecation                     show stack traces on deprecations
    --trace-warnings                        show stack traces on node process warnings
    --use_strict                            enforce strict mode
    --watch-extensions <ext>,...            additional extensions to monitor with --watch
    --delay                                 wait for async suite definition
    --allow-uncaught                        enable uncaught errors to propagate
    --forbid-only                           causes test marked with only to fail the suite
    --forbid-pending                        causes pending tests and test marked with skip to fail the suite
    -h, --help                              output usage information


  Commands:

    init <path>  initialize a client-side mocha setup at <path>
```