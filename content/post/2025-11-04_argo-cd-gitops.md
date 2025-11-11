---
author: "davidalvarezp"
title: "Despliegues continuos con Argo CD y GitOps"
slug: "argo-cd-gitops"
description: "Aprende a implementar CI/CD basado en GitOps con Argo CD para despliegues automáticos y consistentes en Kubernetes."
tags: ["Argo CD", "GitOps", "Kubernetes", "DevOps"]
categories: ["Dev"]
date: "2025-11-04"
keywords: ["argo cd", "gitops", "kubernetes", "ci/cd", "despliegue automatizado"]
draft: false
---

# Despliegues continuos con Argo CD y GitOps

GitOps permite que la **infraestructura y aplicaciones** se gestionen declarativamente desde repositorios Git. Argo CD sincroniza automáticamente los cambios con Kubernetes, asegurando que el estado del clúster coincida con el estado deseado definido en Git.

## Instalación de Argo CD

Crear namespace para Argo CD:
```bash
kubectl create namespace argocd
```

Instalar Argo CD:
```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Exponer servidor API de Argo CD:
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

## Configuración de aplicación GitOps

Definir una Application que apunte a tu repositorio Git con manifiestos Kubernetes:
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: mi-app
  namespace: argocd
spec:
  project: default
  source:
    repoURL: 'https://github.com/usuario/mi-app'
    targetRevision: HEAD
    path: k8s
  destination:
    server: 'https://kubernetes.default.svc'
    namespace: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

## Buenas prácticas

- Versionar todos los manifiestos en Git
- Revisar logs de sincronización de Argo CD
- Definir políticas de rollback y alertas
- Separar entornos dev, staging y prod con namespaces

## Conclusión

Argo CD junto con GitOps permite **despliegues automáticos y consistentes**, mejorando la fiabilidad y trazabilidad de aplicaciones en Kubernetes.
