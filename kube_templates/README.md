# Kubernetes YAML Templates with Detailed Comments

This repository contains comprehensive Kubernetes YAML templates for **33+ major resource types**, with detailed inline comments explaining every field and flag. This covers the vast majority of Kubernetes resources you'll encounter in production.

## 📋 Table of Contents

### Core Workload Resources
1. [Deployment](01-deployment.yaml) - Manages ReplicaSets and Pods for applications
2. [Service](02-service.yaml) - Exposes pods as network services
3. [Pod](03-pod.yaml) - Basic unit that runs containers
4. [ReplicaSet](07-replicaset.yaml) - Ensures a specified number of pod replicas
5. [StatefulSet](08-statefulset.yaml) - Manages stateful applications with stable identities
6. [DaemonSet](09-daemonset.yaml) - Ensures pods run on all (or specific) nodes
7. [Job](10-job.yaml) - Runs a task to completion
8. [CronJob](11-cronjob.yaml) - Runs jobs on a schedule

### Configuration & Secrets
9. [ConfigMap](04-configmap.yaml) - Stores configuration data as key-value pairs
10. [Secret](05-secret.yaml) - Stores sensitive data (passwords, tokens, keys)

### Cluster Management
11. [Namespace](06-namespace.yaml) - Creates logical partitions in a cluster

### Storage Resources
12. [PersistentVolume](12-persistentvolume.yaml) - Cluster-wide storage resource
13. [PersistentVolumeClaim](13-persistentvolumeclaim.yaml) - Request for storage by a user
14. [StorageClass](24-storageclass.yaml) - Defines storage classes for dynamic provisioning
15. [VolumeSnapshot](25-volumesnapshot.yaml) - Snapshot of a volume

### Networking
16. [Ingress](14-ingress.yaml) - Manages external HTTP/HTTPS access to services
17. [NetworkPolicy](19-networkpolicy.yaml) - Defines network access rules for pods
18. [Endpoints](27-endpoints-endpointslice.yaml) - Tracks IP addresses of pods backing a service
19. [EndpointSlice](27-endpoints-endpointslice.yaml) - Scalable alternative to Endpoints

### Autoscaling
20. [HorizontalPodAutoscaler](15-horizontalpodautoscaler.yaml) - Automatically scales pods based on metrics
21. [VerticalPodAutoscaler](26-verticalpodautoscaler.yaml) - Automatically adjusts pod resource requests/limits

### Security & RBAC
22. [ServiceAccount](16-serviceaccount.yaml) - Provides identity for pods
23. [Role](17-role-rolebinding.yaml) - Defines permissions within a namespace
24. [RoleBinding](17-role-rolebinding.yaml) - Grants Role permissions to subjects
25. [ClusterRole](18-clusterrole-clusterrolebinding.yaml) - Defines permissions cluster-wide
26. [ClusterRoleBinding](18-clusterrole-clusterrolebinding.yaml) - Grants ClusterRole permissions to subjects

### Resource Management
27. [ResourceQuota](20-resourcequota.yaml) - Limits resource consumption per namespace
28. [LimitRange](21-limitrange.yaml) - Sets default and max/min limits for resources
29. [PriorityClass](22-priorityclass.yaml) - Sets priority for pods (affects scheduling)
30. [PodDisruptionBudget](23-poddisruptionbudget.yaml) - Limits voluntary disruptions to pods

### Extensibility
31. [CustomResourceDefinition](28-customresourcedefinition.yaml) - Defines custom resources
32. [ValidatingWebhookConfiguration](29-validatingwebhookconfiguration.yaml) - Defines validating admission webhooks
33. [MutatingWebhookConfiguration](30-mutatingwebhookconfiguration.yaml) - Defines mutating admission webhooks

### Advanced
34. [CertificateSigningRequest](31-certificatesigningrequest.yaml) - Requests a certificate from the cluster
35. [RuntimeClass](32-runtimeclass.yaml) - Defines container runtime configurations
36. [Lease](33-lease.yaml) - Provides distributed lock/leader election mechanism

## 🚀 Usage

Each YAML file contains:
- **Complete field definitions** - All available fields and flags
- **Detailed inline comments** - Explanation of each field right next to it
- **Multiple examples** - Different use cases and configurations
- **Best practices** - Security settings, resource limits, and more

### Example Usage

```bash
# Apply a Deployment
kubectl apply -f 01-deployment.yaml

# Apply a Service
kubectl apply -f 02-service.yaml

# Apply with custom namespace
kubectl apply -f 01-deployment.yaml -n production
```

## 📝 Notes

- All templates include comprehensive comments explaining every field
- Examples show various configurations and use cases
- Security best practices are included (non-root users, capabilities, etc.)
- Resource requests and limits are specified
- Health checks (liveness, readiness, startup probes) are configured
- Volume mounts and storage examples are included where applicable

## 🔧 Customization

Before using these templates:
1. Update image names and tags
2. Adjust resource requests/limits based on your needs
3. Modify labels and selectors to match your application
4. Update storage sizes and access modes
5. Configure ingress rules and TLS certificates
6. Adjust scaling parameters (HPA min/max replicas, metrics)

## 📚 Additional Resources

- [Kubernetes Official Documentation](https://kubernetes.io/docs/)
- [Kubernetes API Reference](https://kubernetes.io/docs/reference/kubernetes-api/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- [Deprecated Fields Reference](DEPRECATED_FIELDS.md) - List of deprecated fields and their replacements

## ⚠️ Important Notes

- These are templates - customize them for your specific use case
- Some fields may require cluster-specific configuration (e.g., storage classes, ingress controllers)
- Security contexts and resource limits should be adjusted based on your security policies
- Always test in a non-production environment first
- **All templates use current, non-deprecated fields** - see [DEPRECATED_FIELDS.md](DEPRECATED_FIELDS.md) for deprecated alternatives

## 🎯 Quick Reference

### Core Workload Resources
| Resource | File | Common Use Case |
|----------|------|----------------|
| Deployment | `01-deployment.yaml` | Stateless applications |
| Service | `02-service.yaml` | Expose pods internally/externally |
| Pod | `03-pod.yaml` | Single container or testing |
| ReplicaSet | `07-replicaset.yaml` | Pod replication (usually via Deployment) |
| StatefulSet | `08-statefulset.yaml` | Databases, stateful applications |
| DaemonSet | `09-daemonset.yaml` | Logging, monitoring, node agents |
| Job | `10-job.yaml` | One-time tasks, batch processing |
| CronJob | `11-cronjob.yaml` | Scheduled tasks, backups |

### Configuration & Secrets
| Resource | File | Common Use Case |
|----------|------|----------------|
| ConfigMap | `04-configmap.yaml` | Application configuration |
| Secret | `05-secret.yaml` | Passwords, API keys, certificates |

### Storage Resources
| Resource | File | Common Use Case |
|----------|------|----------------|
| PersistentVolume | `12-persistentvolume.yaml` | Cluster storage |
| PersistentVolumeClaim | `13-persistentvolumeclaim.yaml` | Storage requests |
| StorageClass | `24-storageclass.yaml` | Dynamic storage provisioning |
| VolumeSnapshot | `25-volumesnapshot.yaml` | Volume snapshots |

### Networking
| Resource | File | Common Use Case |
|----------|------|----------------|
| Ingress | `14-ingress.yaml` | HTTP/HTTPS routing |
| NetworkPolicy | `19-networkpolicy.yaml` | Network access control |
| Endpoints | `27-endpoints-endpointslice.yaml` | Service endpoint tracking |
| EndpointSlice | `27-endpoints-endpointslice.yaml` | Scalable endpoint tracking |

### Autoscaling
| Resource | File | Common Use Case |
|----------|------|----------------|
| HorizontalPodAutoscaler | `15-horizontalpodautoscaler.yaml` | Horizontal scaling |
| VerticalPodAutoscaler | `26-verticalpodautoscaler.yaml` | Vertical scaling (resource adjustment) |

### Security & RBAC
| Resource | File | Common Use Case |
|----------|------|----------------|
| ServiceAccount | `16-serviceaccount.yaml` | Pod identity |
| Role | `17-role-rolebinding.yaml` | Namespace-scoped permissions |
| RoleBinding | `17-role-rolebinding.yaml` | Bind roles to subjects |
| ClusterRole | `18-clusterrole-clusterrolebinding.yaml` | Cluster-scoped permissions |
| ClusterRoleBinding | `18-clusterrole-clusterrolebinding.yaml` | Bind cluster roles to subjects |

### Resource Management
| Resource | File | Common Use Case |
|----------|------|----------------|
| ResourceQuota | `20-resourcequota.yaml` | Resource limits per namespace |
| LimitRange | `21-limitrange.yaml` | Default resource limits |
| PriorityClass | `22-priorityclass.yaml` | Pod priority and preemption |
| PodDisruptionBudget | `23-poddisruptionbudget.yaml` | Pod availability guarantees |

### Extensibility
| Resource | File | Common Use Case |
|----------|------|----------------|
| CustomResourceDefinition | `28-customresourcedefinition.yaml` | Custom resources |
| ValidatingWebhookConfiguration | `29-validatingwebhookconfiguration.yaml` | Admission validation |
| MutatingWebhookConfiguration | `30-mutatingwebhookconfiguration.yaml` | Admission mutation |

### Advanced
| Resource | File | Common Use Case |
|----------|------|----------------|
| CertificateSigningRequest | `31-certificatesigningrequest.yaml` | Certificate requests |
| RuntimeClass | `32-runtimeclass.yaml` | Container runtime selection |
| Lease | `33-lease.yaml` | Leader election, distributed locks |
| Namespace | `06-namespace.yaml` | Resource isolation |

---

**Happy Kubernetes Deploying! 🚢**

