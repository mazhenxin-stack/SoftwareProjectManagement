# 冲突练习记录

> 维护人：协作成员 刘瑞祥（liuruixiang）
>
> 目标：按指导书要求，由两名成员在不同分支同时修改本文件中的"当前结论"行，制造一次真实冲突，并在解决后保留过程留痕。

## 1. 演练背景
配置管理文档（`docs/04-config-plan.md`）中已明确"feature → dev → main"的合并流程，但项目经理朱默涵在内部讨论时提出，是否可在小组内部演练阶段直接将冲突分支合并到 main，以缩短验证链路。两种意见均合理，需要通过 Git 实际合并冲突方式进行体验，再由全组讨论得出最终结论。

## 2. 演练参与人
- 朱默涵（zhumohan）：在 `feature-conflict-zhu` 分支上把"当前结论"改成倾向直接合并到 main 的表述。
- 刘瑞祥（liuruixiang）：在 `feature-conflict-liu` 分支上把"当前结论"改成倾向先合并到 dev、再由项目经理合并到 main 的表述。
- 杜航屹（duhangyi）：作为配置管理员复核冲突解决结果，确认最终合并入 dev。

## 3. 当前结论与备注
> 下面这一行是冲突制造的目标行，演练完成后保留最终合并版本。

当前结论：经全组讨论，本组决定遵循配置管理文档约定，所有 feature 分支先合并到 dev，再由项目经理统一合并到 main，禁止 feature 直接合并到 main。
当前备注：此文件专门用于冲突练习，冲突解决后保留在仓库中作为过程记录。

## 4. 建议操作步骤
1. 朱默涵 在 `feature-conflict-zhu` 上将"当前结论"改成 `本组决定直接合并到 main`。
2. 刘瑞祥 在 `feature-conflict-liu` 上将"当前结论"改成 `本组决定先经过 dev 再合并到 main`。
3. 由配置管理员先把 `feature-conflict-zhu` 合并到 `dev`。
4. 再尝试把 `feature-conflict-liu` 合并到 `dev`，此时 Git 报告冲突。
5. 在工作目录中查看 `<<<<<<<` / `=======` / `>>>>>>>` 标记，由两名成员协商最终结论后保存。
6. `git add docs/conflict.md` 并完成合并提交。
7. 在本文件 §5 中追加冲突解决记录。

## 5. 冲突解决记录
> 演练结束后由参与人共同填写。

- 冲突文件：`docs/conflict.md` 第 "当前结论" 行。
- 冲突原因：`feature-conflict-zhu` 与 `feature-conflict-liu` 两条分支基于同一 `dev` 基线对同一行做出了不同修改：朱默涵在 `feature-conflict-zhu` 上倾向直接合并到 main，刘瑞祥在 `feature-conflict-liu` 上倾向走 feature → dev → main 标准流。`feature-conflict-zhu` 先被合并入 `dev` 后，`feature-conflict-liu` 再合并时 Git 检测到同一行的不同变更，无法自动合并并报告 `CONFLICT (content): Merge conflict in docs/conflict.md`。
- 处理方式：
  1. 配置管理员杜航屹通过 `git status` 与 `<<<<<<<` / `=======` / `>>>>>>>` 标记定位冲突；
  2. 朱默涵与刘瑞祥围绕"是否绕过 dev"开展讨论，结合配置管理文档（§2.1 分支模型）已有约定，确认必须保留 dev 作为集成分支；
  3. 在 `docs/conflict.md` 中删除冲突标记并保留经全组讨论后形成的合并表述；
  4. 由配置管理员执行 `git add docs/conflict.md && git commit` 完成合并提交。
- 最终结论：所有 feature 分支必须先合并到 `dev`，由项目经理（朱默涵）按里程碑节奏将 `dev` 合并到 `main`；禁止 feature 直接合并到 main。该规则同步登记到 `docs/04-config-plan.md` §4.1。
- 复核人：杜航屹（duhangyi）。
- 留痕提交：本次合并通过 `git merge --no-ff feature-conflict-liu` 完成，合并提交保留两条父提交，便于事后追溯。
