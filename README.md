# k8s-specifications-argo-cd

Este repositorio contiene los manifiestos necesarios para desplegar aplicaciones en Kubernetes utilizando ArgoCD.

## Requisitos previos

1. Tener instalado y configurado ArgoCD en tu clúster de Kubernetes.
2. Acceso al repositorio de este proyecto: [k8s-specifications-argo-cd](https://github.com/daniel2688/k8s-specifications-argo-cd.git).

## Configuración de la aplicación en ArgoCD

Sigue los pasos a continuación para levantar los manifiestos utilizando el archivo `app.yaml`.

### Contenido del archivo `app.yaml`

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
    name: practica-kcna
    namespace: argocd
spec:
    project: default
    source:
        repoURL: https://github.com/daniel2688/k8s-specifications-argo-cd.git
        path: .
        targetRevision: HEAD
    destination:
        server: https://kubernetes.default.svc
        namespace: practica-kcna
    syncPolicy:
        automated:
            prune: true
            selfHeal: true
```

### Pasos para aplicar el manifiesto

1. Clona este repositorio en tu máquina local:
     ```bash
     git clone https://github.com/daniel2688/k8s-specifications-argo-cd.git
     cd k8s-specifications-argo-cd
     ```

2. Aplica el archivo `app.yaml` en ArgoCD:
     ```bash
     kubectl apply -f app.yaml
     ```

3. Verifica que la aplicación se haya creado correctamente:
     ```bash
     argocd app list
     ```

4. Sincroniza la aplicación si no se sincroniza automáticamente:
     ```bash
     argocd app sync practica-kcna
     ```

## Notas

- La política de sincronización automática (`syncPolicy.automated`) asegura que los recursos se actualicen automáticamente y se eliminen los recursos obsoletos.
- Asegúrate de que el namespace `practica-kcna` exista en tu clúster antes de aplicar el manifiesto.

## Recursos adicionales

- [Documentación oficial de ArgoCD](https://argo-cd.readthedocs.io/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
