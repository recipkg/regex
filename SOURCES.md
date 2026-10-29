# 来源与选取依据

- 上游：[rust-lang/regex](https://github.com/rust-lang/regex)，目标为 `1.13.0`，固定提交 [`926af2e68eca3ce089815790541cf50759ba2c59`](https://github.com/rust-lang/regex/tree/926af2e68eca3ce089815790541cf50759ba2c59)。
- GitHub API 快照（2026-10-29）：4,047 stars；最近推送日期为 2026-10-28 UTC。星数是发现信号，不证明完整性或质量。
- 固定提交的根 `Cargo.toml` 声明 MIT OR Apache-2.0；Unicode 数据及第三方依赖有各自许可，须按其来源分别核对。
- 按固定提交的 [`src/regex/string.rs` 捕获组 API](https://github.com/rust-lang/regex/blob/926af2e68eca3ce089815790541cf50759ba2c59/src/regex/string.rs#L359-L416) 与 [`replace`/`replace_all` 文档](https://github.com/rust-lang/regex/blob/926af2e68eca3ce089815790541cf50759ba2c59/src/regex/string.rs#L685-L811) 记录组编号、非重叠迭代、替换引用语法和无匹配行为；运行样本见 `CAPTURES-OBSERVED.md`。
- 已读范围、固定依赖和有限上游样本见 [COVERAGE.md](COVERAGE.md)、[ACCEPTANCE.md](ACCEPTANCE.md) 与 [CAPTURES-OBSERVED.md](CAPTURES-OBSERVED.md)。尚未完整提取语法、字节 API、错误与资源限制，也没有独立重建或跨平台验收。
