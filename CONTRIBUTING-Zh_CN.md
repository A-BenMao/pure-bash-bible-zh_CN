# 编写Bible

<!-- vim-markdown-toc GFM -->

* [往Bible增加代码.](#往Bible增加代码)
* [代码块的特殊含义.](#代码块的特殊含义)
* [编写测试脚本](#编写测试脚本)
* [运行测试](#运行测试)

<!-- vim-markdown-toc -->

## 往Bible增加代码.

- 代码必须仅仅使用 `bash` 内建函数或功能.
    - 如果代码执行不能始终正常工作，强烈建议增加失败回调以允许程序正常回退到外部程序.
    - 失败回调距离: `${HOSTNAME:-$(hostname)}`
- 如果可能的话，将代码封装在函数中.
    - 这样做可以方便测试程序的编写.
    - 这将同样方便 `shellcheck` 正确的扫描检测.
    - 另外一个好处是展示一个工作用例.
- 编写一些用例.
    - 显示一些输入和输出.


## 代码块的特殊含义.

在函数上标记 `sh` 表示可以被扫描和单元测试.

    ```sh
    # Shellcheck 将会扫描分析，测试脚本将会获取到这个函数.
    func() {
        # Usage: func "arg"
        :
    }
    ```

在代码上标记 `shell` 表示这段代码将被忽略.

    ```shell
    # Shorter file creation syntax.
    :>file
    ```

## 编写测试脚本

可在此处查看测试文件: https://github.com/A-BenMao/pure-bash-bible-zh_CN/blob/master/test.sh

测试单元举例说明:

```sh
test_upper() {
    result="$(upper "HeLlO")"
    assert_equals "$result" "HELLO"
}
```

步骤:

1. 编写测试脚本.
    - 名字命名为 `test_func_name`
    - 将函数输出存储在变量中 (`$result` or `${result[@]}`).
    - 调用 `assert_equals` 测试变量和预期输出之间的相等性。
2. 测试脚本将自动执行它. :+1:


## 运行测试

运行 `test.sh` 的同时也将在代码上执行`shellcheck`.

```sh
cd pure-bash-bible
./test.sh
```
