# 协作约定（CONTRIBUTING）

> 维护人：协作成员 刘瑞祥（liuruixiang）
>
> 本文件作为 README 协作约定的扩展，给出本组成员日常提交、分支、评审与冲突处理的具体操作规范。

## 1. 本地配置约定

### 1.1 用户名与邮箱
每位成员在本仓库本地 clone 后执行：
```bash
git config user.name <本人姓名拼音>
git config user.email <本人邮箱>
```
对应表：
| 姓名 | user.name | user.email |
|---|---|---|
| 朱默涵 | zhumohan | 478306673@qq.com |
| 马振鑫 | mazhenxin | Mazhenxin1833@163.com |
| 杜航屹 | duhangyi | 3307303811@qq.com |
| 刘瑞祥 | liuruixiang | 1366326417@qq.com |

> 全局 `~/.gitconfig` 中可保留默认账户，仓库级配置必须为本人拼音，方便事后核查个人贡献。

### 1.2 行尾约定
统一使用 LF 行尾。Windows 成员可执行：
```bash
git config core.autocrlf input
```

## 2. 分支与提交流程

1. 从 `dev` 拉取最新代码：`git fetch origin && git checkout dev && git pull --ff-only`。
2. 切到本人 feature 分支：`git checkout -b feature-<主题>` 或 `git switch feature-<主题>`。
3. 完成单一交付物的修改后再提交，保持提交粒度可单独说明。
4. 推送：`git push -u origin feature-<主题>`，并在群内或 PR 中知会评审人。
5. 评审通过后，由配置管理员（杜航屹）执行 `git merge --no-ff feature-<主题>` 合并到 `dev`。

## 3. 评审清单

每次合并到 `dev` 前，提交人需自检：

- [ ] 本次提交聚焦单一交付物或主题，没有夹带不相关改动。
- [ ] 提交说明遵循 `init/docs/fix/merge/chore` 前缀 + 中文动宾结构。
- [ ] 已在本分支拉取最新 `dev` 验证无冲突，或冲突已自行处理并复核。
- [ ] 所涉及的 Markdown 文档可正常渲染（无遗留模板提示文字）。

## 4. 冲突处理

1. 在 feature 分支上 `git merge dev`（或 `git rebase dev`）以提前发现冲突。
2. 出现冲突时优先沟通双方意图，再人工修改文件，删除 `<<<<<<<` / `=======` / `>>>>>>>` 标记。
3. 冲突解决后由配置管理员复核，复核通过后再合并到 `dev`。
4. 在 `docs/conflict.md` 中追加一段说明，记录冲突文件、原因、处理方式与最终结论。

## 5. 沟通节奏
- 日常：QQ 群即时沟通；
- 阶段评审：每完成里程碑由项目经理在 GitHub PR 中组织一次评审；
- 异常情况：分支推不上或合并失败时，第一时间在群里 @ 配置管理员，避免长时间挂起。
