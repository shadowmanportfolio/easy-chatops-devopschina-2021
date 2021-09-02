---
name: 创建一个新版本
about: A template to use for releasing
title: v1.0.0
labels: ''
assignees: ''

---

## 🤖 请用您喜欢的版本命名规则来命名 issue 。比如： “v1.0.0”

使用斜线命令可以在issue评论栏进行交互操作：

| 命令 | 描述 | 参数 |
|---|---|---|
| `/release` | 基于当前的`develop`分支创建一个新的标记版本 (如 v1.0.0), 分支 (v1.0.0-branch), 以及镜像标签 (也是 v1.0.0) | N/A |
| `/promote` | 晋级新的镜像库标签 (如 demo), 更新版本标签 ('promoted to demo'), 并且在分支上更新引用 | N/A |
| `/deploy` | 基于Issue 标题部署晋级版本到 k8s 集群 | `cluster=<ci 或 prod>`</br>可选参数: `namespace=<namespace>` 注意： 这个名称也决定了以下的值文件会被使用 `charts/new-app/values-*.yaml` |
| `/tekton` | 运行 tekton task 或 pipeline | `cluster=<ci 或 prod>`</br>`run=<task 或 pipeline>`</br>`name=<task/pipeline的名字>`</br>`namespace=<k8s 命名空间>`</br>`(可选) branch=<分支名和issue-title-branch名是不同的>` |
| `/cancel` | 取消当前的版本 (即关闭本 issue) | N/A |
