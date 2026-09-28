# argocd-app-manifests

Argo CD GitOps 예제의 **Kubernetes 매니페스트** 저장소입니다. 애플리케이션 소스는 [argocd-app-source](https://github.com/songtomtom/argocd-app-source) 에 있습니다.

블로그 글: [GitHub를 활용한 GitOps 구현하기](https://songtomtom.github.io/blog/argocd-github-gitops)

## 파일

- `deployment.yaml`: python-server Deployment. `image` 태그는 소스 저장소의 GitHub Actions 가 커밋 SHA 로 갱신한다. 사람이 직접 고치지 않는다.
- `my-gitops-app.yaml`: Argo CD `Application` 리소스. 이 저장소의 루트를 감시해 `default` 네임스페이스에 자동 동기화한다.

## 적용

```bash
kubectl apply -f my-gitops-app.yaml
```

`syncPolicy.automated` 에 `prune` 과 `selfHeal` 이 켜져 있어, 저장소에서 지운 리소스는 클러스터에서도 지워지고 클러스터에서 손으로 바꾼 내용은 저장소 상태로 되돌아간다.
