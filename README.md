# regex · Recipkg

**把正则引擎的匹配语义、字节边界和可重复验收整理成可复用配方。**

[标准库](https://github.com/recipkg/standard-library) · [配方清单](RECIPE.md) · [构建要求](BUILD_PROMPT.md) · [验收条件](ACCEPTANCE.md) · [捕获与替换观察](CAPTURES-OBSERVED.md) · [来源](SOURCES.md) · [来源与覆盖](COVERAGE.md)

![从软件与依赖整理配方，再交给 Agent 重建](https://raw.githubusercontent.com/recipkg/recipkg/main/assets/recipkg-cover.png)

本仓库保存重建配方，不是上游源码或官方发行版。配方仍在提取，语法、字节 API 和性能等均未完整验证；见 [覆盖状态](COVERAGE.md)。

```sh
recipe_dir="$(mktemp -d)"
recipkg pack . -o "$recipe_dir/regex.recipe.tar.gz"
recipkg check "$recipe_dir/regex.recipe.tar.gz"
recipkg build "$recipe_dir/regex.recipe.tar.gz" --lang zh-CN --output "$recipe_dir/build.md"
printf '提示词：%s\n' "$recipe_dir/build.md"
```
