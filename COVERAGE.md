# 来源、实测与缺口

- [rust-lang/regex 1.13.0 标签](https://github.com/rust-lang/regex/tree/926af2e68eca3ce089815790541cf50759ba2c59)的提交为 `926af2e68eca3ce089815790541cf50759ba2c59`。根 Cargo.toml 声明 MIT OR Apache-2.0；Unicode 数据、第三方依赖和各自许可需单独检查。阅读了根包 `src/lib.rs` 的部分语法、Unicode 与性能说明。
- 固定 [ripgrep Cargo.lock](https://github.com/BurntSushi/ripgrep/blob/e89fff89ac9af12e8d4ce9d5fd07beb408ca730f/Cargo.lock) 包含 `regex 1.13.0`、`regex-automata 0.4.15`、`regex-syntax 0.8.11`、`aho-corasick 1.1.4`、`memchr 2.8.3`。从 crates.io 下载 `regex-1.13.0.crate`，其 SHA-256 为 `2a0e75113e14dc5acb068cd0786884f214f1312650a3d36d269f5c4f3cdee8a2`，与锁文件一致；归档内 `.cargo_vcs_info.json` 声明的 Git 提交与标签一致，但未逐文件核对包与该提交，也未证明系统 ripgrep 的实际构建来源。
- 在 Linux x86-64、Rust/Cargo 1.99.0 的临时目录构建 crates.io 包参考适配器，锁定上述 5 个依赖版本，运行 `test_regex.py` 的 4 组样本通过。上游 crate 的 feature 配置和 ripgrep 实际内部调用路径未逐项比对；该结果是库适配器测试，不是 ripgrep 全部功能测试或独立重建。
- 同一组锁定的 crates.io 包及 Rust/Cargo 版本下，参考适配器新增 `regex::bytes::Regex` 样本：无效 UTF-8、默认 Unicode 和关闭 Unicode、字节序列的空匹配边界。具体输入和结果见 `ACCEPTANCE.md`；仅这些样本得到验证，尚未覆盖任意二进制、其他模式和平台。
- 2026-10-29，在 Rust/Cargo 1.99.0、Linux x86-64 下扩展固定 `regex = 1.13.0` 的参考适配器，加入捕获组编号/名称、未匹配可选组、UTF-8 字节区间、首个/全部替换及 `$` 展开样本。`test_regex.py` 的 11 个方法全部通过；验收代码在 [standard-library-verification `8a79140aaa0585dc975d69c09712321832e84b96`](https://github.com/recipkg/standard-library-verification/tree/8a79140aaa0585dc975d69c09712321832e84b96)，依赖版本由 fixture 的 `Cargo.lock` 固定。参考程序运行的是上游 crate，不是独立重建；crate 归档与固定 Git 提交的逐文件等价仍未核验。
- 尚未完整提取语法、捕获、字节 API、替换、错误细节、性能、Unicode 数据和资源限制；未证明配方可完整生成引擎、未运行独立重建或跨平台验证。`quality` 是固定的共用质量合同，不是引擎实现。
