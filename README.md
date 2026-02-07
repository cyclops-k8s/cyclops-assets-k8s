# Cyclops Assets for Kubernetes

This repository contains Kubernetes manifests for deploying asset management and container registry mirroring infrastructure for Cyclops.

## Overview

The `cyclops-assets-k8s` repository provides the infrastructure to:

- **Serve Static Assets**: Deploy an nginx-based service to host static assets
- **Mirror Container Registries**: Set up local mirrors for popular container registries to improve performance and reduce external dependencies
- **Sync OS Images**: Automatically download and maintain OS images for cloud environments

## Components

### Asset Server
- **Purpose**: Serves static assets via nginx
- **Manifests**: 
  - `assets-deployment.yaml` - Main deployment
  - `service.yaml` - Service configuration
  - `storage.yaml` - Persistent storage configuration

### Container Registry Mirrors
Provides local mirrors for the following registries:
- **docker.io** - Docker Hub mirror
- **quay.io** - Quay.io mirror
- **registry.k8s.io** - Kubernetes registry mirror

Each mirror includes:
- Deployment configuration
- Service definition
- Persistent storage
- ConfigMap for registry settings

### OS Image Synchronization
- **Purpose**: Automatically downloads and maintains OS cloud images (CentOS Stream, Ubuntu)
- **Schedule**: Daily CronJob to sync images
- **Manifests**:
  - `os-image-sync.yaml` - CronJob definition
  - `os-images-configmap.yaml` - List of OS images to sync

### Registry Mirrors Proxy
- **Purpose**: Nginx-based proxy to route requests to appropriate registry mirrors
- **Manifests**:
  - `registry-mirrors-proxy.yaml` - Proxy deployment
  - `registry-mirrors-proxy-cm.yaml` - Proxy configuration
  - `registry-mirrors-service.yaml` - Service definition

## Deployment

All manifests are located in the `manifests/` directory. To deploy:

```bash
# Apply all manifests
kubectl apply -f manifests/

# Or apply specific components
kubectl apply -f manifests/assets-deployment.yaml
kubectl apply -f manifests/mirror-docker-io-*.yaml
```

## Namespace

All resources are deployed to the `cyclops-assets` namespace.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## About Cyclops

Cyclops is a one-stop shop for Kubernetes, providing tools and infrastructure to simplify Kubernetes operations.
