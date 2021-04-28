---
title: '[Kubernetes] 명령어들'
categories:
  - IT
  - Kubernetes
tags:
  - Kubernetes
date: 2021-03-04 11:17:05
thumbnail: /images/thumbnail/kubernetes.png
---

## 명령어들

```bash
# 생성
kubectl create -f test.pod.yaml

# 중지 및 삭제
kubectl delete pod test --grace-period=0 --force
kubectl delete service test

# node 정보 확인
kubectl get nodes

# pod 확인
kubectl get pods --all-namespaces

# 서비스 확인
kubectl get svc

# 배포 확인
kubectl get deployments

# 상세 정보 확인
kubectl describe pods

# 개별 상세 정보 확인
kubectl describe pod <name>

```
