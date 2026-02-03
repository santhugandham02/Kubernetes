# Deprecated Fields and Annotations Reference

This document lists deprecated fields and annotations found in the Kubernetes YAML templates, along with their recommended alternatives.

## ⚠️ Deprecated Fields

### 1. Ingress - `kubernetes.io/ingress.class` annotation
**File:** `14-ingress.yaml`  
**Status:** Deprecated in Kubernetes 1.18+  
**Replacement:** Use `spec.ingressClassName` instead

**Before (Deprecated):**
```yaml
metadata:
  annotations:
    kubernetes.io/ingress.class: "nginx"
```

**After (Current):**
```yaml
spec:
  ingressClassName: nginx
```

---

### 2. PersistentVolumeClaim - `volume.beta.kubernetes.io/storage-class` annotation
**File:** `13-persistentvolumeclaim.yaml`  
**Status:** Deprecated  
**Replacement:** Use `spec.storageClassName` instead

**Before (Deprecated):**
```yaml
metadata:
  annotations:
    volume.beta.kubernetes.io/storage-class: "fast-ssd"
```

**After (Current):**
```yaml
spec:
  storageClassName: fast-ssd
```

---

### 3. PersistentVolume - `Recycle` reclaim policy
**File:** `12-persistentvolume.yaml`  
**Status:** Deprecated and removed in Kubernetes 1.15+  
**Replacement:** Use `Retain` or `Delete` instead

**Before (Deprecated):**
```yaml
spec:
  persistentVolumeReclaimPolicy: Recycle
```

**After (Current):**
```yaml
spec:
  persistentVolumeReclaimPolicy: Retain  # or Delete
```

---

### 4. ResourceQuota - `scopes` field
**File:** `20-resourcequota.yaml`  
**Status:** Deprecated  
**Replacement:** Use `scopeSelector` instead

**Before (Deprecated):**
```yaml
spec:
  scopes:
  - BestEffort
  - NotTerminating
```

**After (Current):**
```yaml
spec:
  scopeSelector:
    matchExpressions:
    - operator: In
      scopeName: PriorityClass
      values:
      - high-priority
```

---

### 5. Service - `loadBalancerIP` field
**File:** `02-service.yaml`  
**Status:** Deprecated in Kubernetes 1.24+  
**Replacement:** Use `loadBalancerClass` (cloud-provider specific)

**Before (Deprecated):**
```yaml
spec:
  type: LoadBalancer
  loadBalancerIP: 192.168.1.100
```

**After (Current - Kubernetes 1.24+):**
```yaml
spec:
  type: LoadBalancer
  loadBalancerClass: "service.k8s.aws/nlb"  # Example for AWS
  # Use cloud-provider specific annotations for IP assignment
```

**Note:** `loadBalancerIP` is still widely used and supported by most cloud providers, but the new approach uses `loadBalancerClass` with provider-specific annotations.

---

## ⚠️ Alpha/Beta Annotations (Not Deprecated, But Use with Caution)

### 1. Namespace - `scheduler.alpha.kubernetes.io/node-selector`
**File:** `06-namespace.yaml`  
**Status:** Alpha-level feature  
**Note:** May not be available in all Kubernetes distributions. Primarily used in OpenShift.

---

### 2. Service - `service.beta.kubernetes.io/*` annotations
**File:** `02-service.yaml`  
**Status:** Beta-level, but still commonly used  
**Note:** These annotations are the standard way to configure cloud provider load balancers. While beta-level, they are stable and widely supported. Some cloud providers are moving to newer annotation formats, so check your provider's documentation.

**Common annotations:**
- `service.beta.kubernetes.io/aws-load-balancer-type`
- `service.beta.kubernetes.io/azure-load-balancer-internal`
- `service.beta.kubernetes.io/gce-load-balancer-type`

---

## ✅ All Templates Use Current Best Practices

All templates in this repository:
1. Use stable API versions (`v1`, `apps/v1`, `networking.k8s.io/v1`, etc.)
2. Prefer spec fields over annotations where possible
3. Include deprecated examples only for reference (clearly marked)
4. Use current recommended approaches as the primary examples

---

## 📚 References

- [Kubernetes API Deprecation Policy](https://kubernetes.io/docs/reference/using-api/deprecation-policy/)
- [Kubernetes API Reference](https://kubernetes.io/docs/reference/kubernetes-api/)
- [Kubernetes Release Notes](https://kubernetes.io/releases/)

---

**Last Updated:** Based on Kubernetes 1.28+ API specifications

