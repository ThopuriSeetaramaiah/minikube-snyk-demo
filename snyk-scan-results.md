# Snyk Scan Results

## Basic NGINX Deployment (nginx:1.14.2)

### Infrastructure as Code Scan
```
Snyk Infrastructure as Code

- Snyk testing Infrastructure as Code configuration issues.
✔ Test completed.

Issues

Low Severity Issues: 6

  [Low] Container's or Pod's  UID could clash with host's UID
  Info:    `runAsUser` value is set to low UID. UID of the container processes
           could clash with host's UIDs and lead to unintentional authorization
           bypass
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-11
  Path:    [DocId: 0] > input > spec > template > spec > containers[nginx] >
           securityContext > runAsUser
  File:    nginx-deployment.yaml
  Resolve: Set `securityContext.runAsUser` value to greater or equal than
           10'000. SecurityContext can be set on both `pod` and `container`
           level. If both are set, then the container level takes precedence

  [Low] Container is running without memory limit
  Info:    Memory limit is not defined. Containers without memory limits are
           more likely to be terminated when the node runs out of memory
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-4
  Path:    [DocId: 0] > input > spec > template > spec > containers[nginx] >
           resources > limits > memory
  File:    nginx-deployment.yaml
  Resolve: Set `resources.limits.memory` value

  [Low] Container is running without liveness probe
  Info:    Liveness probe is not defined. Kubernetes will not be able to detect
           if application is able to service requests, and will not restart
           unhealthy pods
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-41
  Path:    [DocId: 0] > spec > template > spec > containers[nginx] >
           livenessProbe
  File:    nginx-deployment.yaml
  Resolve: Add `livenessProbe` attribute

  [Low] Container could be running with outdated image
  Info:    The image policy does not prevent image reuse. The container may run
           with outdated or unauthorized image
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-42
  Path:    [DocId: 0] > spec > template > spec > containers[nginx] >
           imagePullPolicy
  File:    nginx-deployment.yaml
  Resolve: Set `imagePullPolicy` attribute to `Always`

  [Low] Container has no CPU limit
  Info:    Container has no CPU limit. CPU limits can prevent containers from
           consuming valuable compute time for no benefit (e.g. inefficient
           code) that might lead to unnecessary costs. It is advisable to also
           configure CPU requests to ensure application stability.
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-5
  Path:    [DocId: 0] > input > spec > template > spec > containers[nginx] >
           resources > limits > cpu
  File:    nginx-deployment.yaml
  Resolve: Add `resources.limits.cpu` field with required CPU limit value

  [Low] Container is running with writable root filesystem
  Info:    `readOnlyRootFilesystem` attribute is not set to `true`. Compromised
           process could abuse writable root filesystem to elevate privileges
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-8
  Path:    [DocId: 0] > spec > template > spec > containers[nginx] >
           securityContext > readOnlyRootFilesystem
  File:    nginx-deployment.yaml
  Resolve: Set `spec.{containers,
           initContainers}.securityContext.readOnlyRootFilesystem` to `true`

Medium Severity Issues: 3

  [Medium] Container or Pod is running without root user control
  Info:    Container or Pod is running without root user control. Container or
           Pod could be running with full administrative privileges
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-10
  Path:    [DocId: 0] > input > spec > template > spec > containers[nginx] >
           securityContext > runAsNonRoot
  File:    nginx-deployment.yaml
  Resolve: Set `securityContext.runAsNonRoot` to `true`

  [Medium] Container does not drop all default capabilities
  Info:    All default capabilities are not explicitly dropped. Containers are
           running with potentially unnecessary privileges
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-6
  Path:    [DocId: 0] > input > spec > template > spec > containers[nginx] >
           securityContext > capabilities > drop
  File:    nginx-deployment.yaml
  Resolve: Add `ALL` to `securityContext.capabilities.drop` list, and add only
           required capabilities in `securityContext.capabilities.add`

  [Medium] Container is running without privilege escalation control
  Info:    `allowPrivilegeEscalation` attribute is not set to `false`. Processes
           could elevate current privileges via known vectors, for example SUID
           binaries
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-9
  Path:    [DocId: 0] > spec > template > spec > containers[nginx] >
           securityContext > allowPrivilegeEscalation
  File:    nginx-deployment.yaml
  Resolve: Set `spec.{containers,
           initContainers}.securityContext.allowPrivilegeEscalation` to `false`
```

### Container Image Scan
```
Testing nginx:1.14.2...

Organization:      sthopuri4332
Package manager:   deb
Project name:      docker-image|nginx
Docker image:      nginx:1.14.2
Platform:          linux/amd64
Base image:        nginx:1.14.2
Licenses:          enabled

Tested 108 dependencies for known issues, found 252 issues.

Base Image    Vulnerabilities  Severity
nginx:1.14.2  252              28 critical, 47 high, 52 medium, 125 low

Recommendations for base image upgrade:

Minor upgrades
Base Image    Vulnerabilities  Severity
nginx:1.28.0  90               1 critical, 3 high, 0 medium, 86 low

Alternative image types
Base Image                    Vulnerabilities  Severity
nginx:1.28.0-alpine3.21-slim  0                0 critical, 0 high, 0 medium, 0 low
nginx:1.27.5-alpine3.21-slim  0                0 critical, 0 high, 0 medium, 0 low
```

## Secure NGINX Deployment (nginx:1.28.0-alpine)

### Infrastructure as Code Scan
```
Snyk Infrastructure as Code

- Snyk testing Infrastructure as Code configuration issues.
✔ Test completed.

Issues

Low Severity Issues: 2

  [Low] Container's or Pod's  UID could clash with host's UID
  Info:    `runAsUser` value is set to low UID. UID of the container processes
           could clash with host's UIDs and lead to unintentional authorization
           bypass
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-11
  Path:    [DocId: 0] > input > spec > template > spec > containers[nginx] >
           securityContext > runAsUser
  File:    secure-nginx-deployment.yaml
  Resolve: Set `securityContext.runAsUser` value to greater or equal than
           10'000. SecurityContext can be set on both `pod` and `container`
           level. If both are set, then the container level takes precedence

  [Low] Container is running with writable root filesystem
  Info:    `readOnlyRootFilesystem` attribute is not set to `true`. Compromised
           process could abuse writable root filesystem to elevate privileges
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-8
  Path:    [DocId: 0] > spec > template > spec > containers[nginx] >
           securityContext > readOnlyRootFilesystem
  File:    secure-nginx-deployment.yaml
  Resolve: Set `spec.{containers,
           initContainers}.securityContext.readOnlyRootFilesystem` to `true`

Medium Severity Issues: 3

  [Medium] Container or Pod is running without root user control
  Info:    Container or Pod is running without root user control. Container or
           Pod could be running with full administrative privileges
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-10
  Path:    [DocId: 0] > input > spec > template > spec > containers[nginx] >
           securityContext > runAsNonRoot
  File:    secure-nginx-deployment.yaml
  Resolve: Set `securityContext.runAsNonRoot` to `true`

  [Medium] Container does not drop all default capabilities
  Info:    All default capabilities are not explicitly dropped. Containers are
           running with potentially unnecessary privileges
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-6
  Path:    [DocId: 0] > input > spec > template > spec > containers[nginx] >
           securityContext > capabilities > drop
  File:    secure-nginx-deployment.yaml
  Resolve: Add `ALL` to `securityContext.capabilities.drop` list, and add only
           required capabilities in `securityContext.capabilities.add`

  [Medium] Container is running without privilege escalation control
  Info:    `allowPrivilegeEscalation` attribute is not set to `false`. Processes
           could elevate current privileges via known vectors, for example SUID
           binaries
  Rule:    https://security.snyk.io/rules/cloud/SNYK-CC-K8S-9
  Path:    [DocId: 0] > spec > template > spec > containers[nginx] >
           securityContext > allowPrivilegeEscalation
  File:    secure-nginx-deployment.yaml
  Resolve: Set `spec.{containers,
           initContainers}.securityContext.allowPrivilegeEscalation` to `false`
```

### Container Image Scan
```
Testing nginx:1.28.0-alpine...

✗ High severity vulnerability found in libxml2/libxml2
  Description: Unchecked Return Value
  Info: https://security.snyk.io/vuln/SNYK-ALPINE321-LIBXML2-10123178
  Introduced through: libxml2/libxml2@2.13.4-r5, libxslt/libxslt@1.1.42-r2, nginx-module-njs/nginx-module-njs@1.28.0.0.8.10-r1, nginx-module-xslt/nginx-module-xslt@1.28.0-r1
  From: libxml2/libxml2@2.13.4-r5
  From: libxslt/libxslt@1.1.42-r2 > libxml2/libxml2@2.13.4-r5
  From: nginx-module-njs/nginx-module-njs@1.28.0.0.8.10-r1 > libxml2/libxml2@2.13.4-r5
  and 1 more...
  Fixed in: 2.13.4-r6

✗ High severity vulnerability found in libxml2/libxml2
  Description: Out-of-bounds Read
  Info: https://security.snyk.io/vuln/SNYK-ALPINE321-LIBXML2-10123179
  Introduced through: libxml2/libxml2@2.13.4-r5, libxslt/libxslt@1.1.42-r2, nginx-module-njs/nginx-module-njs@1.28.0.0.8.10-r1, nginx-module-xslt/nginx-module-xslt@1.28.0-r1
  From: libxml2/libxml2@2.13.4-r5
  From: libxslt/libxslt@1.1.42-r2 > libxml2/libxml2@2.13.4-r5
  From: nginx-module-njs/nginx-module-njs@1.28.0.0.8.10-r1 > libxml2/libxml2@2.13.4-r5
  and 1 more...
  Fixed in: 2.13.4-r6

Organization:      sthopuri4332
Package manager:   apk
Project name:      docker-image|nginx
Docker image:      nginx:1.28.0-alpine
Platform:          linux/amd64
Licenses:          enabled

Tested 68 dependencies for known issues, found 2 issues.
```
