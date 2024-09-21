# newHugo

- 配置 hugo (exe, path)

```bash
# 在當前目錄建議 hugo project
hugo new site . --format yaml 

# 以 submodule 方式導入主題
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod

# needed when you reclone your repo
git submodule update --init --recursive

# 更新 submodule
git submodule update --remote --merge
```

## theme
- [hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod)
- [hugo-paperMod Example](https://github.com/adityatelange/hugo-PaperMod/tree/exampleSite)
