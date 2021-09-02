# 基于Tekton、ArgoCD和GitHub Action的简单ChatOps发布自动化

## 先决条件
1. OpenShift集群，并在代码库中命名以下GitHub Repository Secrets 作为集群的登录凭证。
  - `OPENSHIFT_PASSWORD`
  - `OPENSHIFT_SERVER`
2. 在OpenShift中部署ArgoCD，并将本代码库地址加入进来。
3. 在OpenShift中部署Tekton，并把预先准备好的 Tasks 和 Pipelines 部署进来。
4. 配置[Github 个人访问 Token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) ，将 Token 值创建 GitHub Repository Secret 名为: `SLASH_TOKEN`。此 Secret 供 [chatops slash commands](https://github.com/peter-evans/slash-command-dispatch#token) 使用来访问代码库。 

## 说明
这个样例代码库是根据 [基于 trunk 的开发](https://trunkbaseddevelopment.com/) 理念设计的。

## 运行机制

通过 GitHub Action `.github/workflows/tekton-build.yaml` 来监听 `src` 目录的代码修改，驱动集群内就绪的 Tekton 进行构建。 

一但准备好交付，创建一个 Issue (点击此链接 [Release Issue template](https://github.com/shadowmanportfolio/easy-chatops-devopschina-2021/issues/new?assignees=&labels=&template=03_release.md&title=v1.0.0) 查看详细操作说明)

`/release` 命令用于为版本打标签</br>
`/promote` 命令用于切换适用的 ArgoCD 配置来指向新的标签</br>
`/deploy` 命令用过于驱动 ArgoCD `Application` ，详细参见社区[文档](https://argoproj.github.io/argo-cd/getting_started/#6-create-an-application-from-a-git-repository)

## 引用的GitHub Actions 来源：
- https://github.com/peter-evans/slash-command-dispatch
- https://github.com/redhat-actions/openshift-tools-installer
- https://github.com/redhat-actions/oc-login
- https://github.com/mikefarah/yq
- https://github.com/peter-evans/close-issue
- https://github.com/peter-evans/create-or-update-comment
- https://github.com/peterjgrainger/action-create-branch
- https://github.com/stefanzweifel/git-auto-commit-action 

## Tekton Tasks & Pipelines 来源：

- https://hub.tekton.dev/tekton/task/s2i
- https://hub.tekton.dev/tekton/task/git-clone


