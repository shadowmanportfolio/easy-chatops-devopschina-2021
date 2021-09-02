# 基于Tekton、ArgoCD和GitHub Action的简单ChatOps发布自动化

## 先决条件
1. OpenShift集群，并在代码库中命名以下GitHub Repository Secrets 作为集群的登录凭证
  - `OPENSHIFT_PASSWORD`
  - `OPENSHIFT_SERVER`
2. 在OpenShift中部署ArgoCD，并将本代码库地址加入进来
3. 在OpenShift中部署Tekton，并把预先准备好的 Tasks 和 Pipelines 部署进来
4. 配置[Github 个人访问 Token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) ，将 Token 值创建 GitHub Repository Secret 名为: `SLASH_TOKEN`。此 Secret 供 [chatops slash commands](https://github.com/peter-evans/slash-command-dispatch#token) 使用来访问代码库。 

## 说明
这个样例代码库是根据 [基于 trunk 的开发](https://trunkbaseddevelopment.com/) 理念计划的。

## 运行机制

Tekton is building in the cluster based off of any changes to the `src` directory via GitHub action `.github/workflows/tekton-build.yaml`

Once you are ready to release, create an Issue (use the [Release Issue template](https://github.com/shadowmanportfolio/easy-chatops-devopschina-2021/issues/new?assignees=&labels=&template=03_release.md&title=v1.0.0) for more documentation)

`/release` to create a tagged release based on the name</br>
`/promote` to change the appropriate ArgoCD configs to point the new tag</br>
`/deploy` to deploy via ArgoCD `Application` documentation [here](https://argoproj.github.io/argo-cd/getting_started/#6-create-an-application-from-a-git-repository)

## GitHub Actions are from:
- https://github.com/peter-evans/slash-command-dispatch
- https://github.com/redhat-actions/openshift-tools-installer
- https://github.com/redhat-actions/oc-login
- https://github.com/mikefarah/yq
- https://github.com/peter-evans/close-issue
- https://github.com/peter-evans/create-or-update-comment
- https://github.com/peterjgrainger/action-create-branch
- https://github.com/stefanzweifel/git-auto-commit-action 

## Tekton Tasks & Pipelines are from:

- https://hub.tekton.dev/tekton/task/s2i
- https://hub.tekton.dev/tekton/task/git-clone


