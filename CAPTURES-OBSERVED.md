# 捕获组与替换观察

本文记录固定 `rust-lang/regex` 提交 `926af2e68eca3ce089815790541cf50759ba2c59` 的字符串 API 文档，并区分源代码合同与参考程序运行样本。对应实现说明位于 `src/regex/string.rs` 的 [`captures` 与 `captures_iter`](https://github.com/rust-lang/regex/blob/926af2e68eca3ce089815790541cf50759ba2c59/src/regex/string.rs#L359-L416)、[`replace` 与替换语法](https://github.com/rust-lang/regex/blob/926af2e68eca3ce089815790541cf50759ba2c59/src/regex/string.rs#L685-L811)。

## 固定源码中的行为说明

- 捕获组 `0` 始终表示完整匹配；其他编号按左括号出现次序分配。命名组也可按数字编号读取；名称列表按捕获组次序给出。
- `captures` 返回首个匹配的捕获信息；`captures_iter` 连续产生非重叠匹配。每条捕获记录包含完整匹配和所有捕获组；未参与匹配的组没有匹配值。
- `replace` 只处理第一个匹配；`replace_all` 处理所有非重叠匹配。没有匹配时返回与输入等价的文本。
- 文本替换项支持 `$N`、`$name` 和 `${name}`。编号 `0` 指完整匹配；不存在的组引用替换为空；遇到多个可能名字时优先读取最长名称；`$$` 表示字面美元符号。
- 源码还提供接收捕获记录的替换闭包。它可计算动态替换内容，但闭包错误、中途失败和字节 API 替换未在本轮运行样本覆盖。

## 参考运行样本

2026-10-29，使用 Linux x86-64、Rust/Cargo 1.99.0 和 `fixtures/regex-reference/Cargo.lock` 锁定的 `regex 1.13.0` 参考适配器运行 `standard-library-verification/tests/test_regex.py`，11 项测试全部通过。样本包括：

- 两个命名捕获组及两条非重叠匹配，返回组名和完整匹配/子组的 UTF-8 字节区间；
- 可选组在某条匹配中缺失时返回空值；
- 匹配 `éx` 时，捕获区间为字节 `[0,3)`，而不是字符索引 `[0,2)`；
- 只替换首个数字匹配与替换全部数字匹配；
- `$0`、`${first}`、`$second`、缺失组和 `$$` 的展开，以及没有匹配时保留原文本。

这些测试通过调用固定 crates.io 版本的上游 crate 完成。它们用于核对配方中的有限行为，不是独立引擎重建；参考 crate 归档与固定 Git 提交的逐文件等价尚未核验，其他平台、闭包替换、完整 API 与错误边界也未覆盖。
