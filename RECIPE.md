# regex 正则引擎配方（提取中）

```toml
format = "recipkg/1"

[package]
name = "regex"
version = "0.1.2"
kind = "software"
description = "可复用的有限自动机正则匹配引擎重建配方，当前仍在提取。"
entry = "BUILD_PROMPT.md"

[dependencies.quality]
git = "https://github.com/recipkg/recipkg.git"
rev = "41e5b55c6612a9a5a10e499b5ace6a1a3fed0f2b"
subdir = "recipes/software-quality"
```

来源：[rust-lang/regex](https://github.com/rust-lang/regex/tree/926af2e68eca3ce089815790541cf50759ba2c59)，上游 `1.13.0` 标签对应提交 `926af2e68eca3ce089815790541cf50759ba2c59`，根包声明 MIT 或 Apache-2.0；Unicode 数据和依赖需单独核对。此配方仍不完整，证据、许可和未验证内容见 `COVERAGE.md`。
