# gh-rag-indexes

[gh-rag](https://github.com/alex-1263/github-rag) 的索引数据分发仓库:**骨架库**(向量 + 元数据,无正文/评论全文)按周自动构建并发布到 [Releases](../../releases)。

```bash
gh-rag fetch --from <骨架库 URL 或本地路径>   # 装载(指纹校验,不匹配拒绝)
gh-rag sync --all                             # 补全文(内容哈希对齐,向量零重嵌)
```

## 命名与对账

```
gh-rag-index-{repo}-{model}-{dim}-{date}.sqlite.gz
```

文件名对模型,库内 `embedding_fp` 对指纹,`fetch` 装载前强制与本地嵌入配置匹配。

## 数据贡献

**模式 A(最简单)**:开 PR,在 `repos.toml` 加一行 `"owner/repo"` —— merge 后由构建流水线统一产出。

**模式 B(自助构建)**:fork 本仓库 → Settings→Secrets 配自己的 `EMBED_API_KEY` → Actions 跑 `build` workflow(同一份 workflow = 产出规格)→ 产物上传自己 fork 的 Release → 向本仓库提 PR 添加 manifest 条目。

## 版权边界(重要)

issue/PR 正文与讨论的**版权属于各原作者**(GitHub ToS D.5 仅授权通过服务的 use/display/perform/fork)。本仓库分发的骨架库**只含衍生数据**(向量)与**事实元数据**(编号/类型/状态/时间/哈希),**不含任何原文文本**;全文由各用户经 GitHub API 本地获取——流程设计即版权边界。发布者需保证:来源仓库为公开仓库,衍生数据有权分发。

## 许可

数据(骨架库)以 [CC BY 4.0](LICENSE) 分发(署名 = 溯源链接);构建代码同上游 [MIT](https://github.com/alex-1263/github-rag/blob/main/LICENSE)。
