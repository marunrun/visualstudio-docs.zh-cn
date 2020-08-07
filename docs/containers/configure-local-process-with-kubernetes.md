---
title: 将 KubernetesLocalProcessConfig.yaml 用于 Local Process with Kubernetes 的附加配置
services: azure-dev-spaces
ms.date: 07/28/2020
ms.topic: conceptual
description: 介绍将 KubernetesLocalProcessConfig.yaml 用于 Local Process with Kubernetes 的附加配置选项
keywords: Local Process with Kubernetes, Azure Dev Spaces, Dev Spaces, Docker, Kubernetes, Azure, AKS, Azure Kubernetes 服务, 容器
monikerRange: '>=vs-2019'
author: ghogen
ms.author: ghogen
manager: jillfra
ms.openlocfilehash: 234eacedbc08007ede6bb5745a1a289aa838cccb
ms.sourcegitcommit: e359b93c93c6ca316c0d8b86c2b6e566171fd1ea
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2020
ms.locfileid: "87508310"
---
# <a name="configure-local-process-with-kubernetes"></a>配置 Local Process with Kubernetes

使用 `KubernetesLocalProcessConfig.yaml` 文件可以将环境变量和已装载文件复制到 AKS 群集中的 Pod。 可以在 `KubernetesLocalProcessConfig.yaml` 中指定以下操作：

* 下载一个卷，并将该卷的路径设置为环境变量。
* 使集群上运行的服务可供开发计算机上运行的进程使用。
* 创建一个具有常数值的环境变量。

默认的 `KubernetesLocalProcessConfig.yaml` 文件不会自动创建，因此你必须在项目的根目录中手动创建文件。

## <a name="download-a-volume"></a>下载卷

在“env”下，为要下载的每个卷指定“name”和“value”。 “name”是将在开发计算机上使用的环境变量。 “value”是卷的名称和开发计算机上的路径。 “value”的值采用 $(volumeMounts:VOLUME_NAME)/PATH/TO/FILES 的形式。

例如：

```yaml
version: 0.1
env:
  - name: ALLOW_LIST_PATH
    value: $(volumeMounts:allow-list)/allow-list
```

上面的示例从容器下载 allow-list 卷，并设置该位置加上环境变量 ALLOW_LIST_PATH 的路径。 默认行为是将文件下载到你在开发计算机上的临时目录下指定的路径。 在上面的示例中，将 ALLOW_LIST_PATH 设置为 `/TEMPORARY_DIR/allow-list`。 

> [!NOTE]
> 无论你设置的路径是什么，下载卷时都会下载该卷的全部内容。 该路径仅用于设置开发计算机上使用的环境变量。 向令牌末尾添加 /allow-list 或 /path/to/files 实际上并不会影响卷的保留位置。 环境变量只是在应用需要引用该卷内的特定文件时提供方便。

还可以选择指定一个位置来下载要在开发计算机上装载的卷，而不是使用临时目录。 在“volumeMounts”下，为每个特定位置指定“name”和“localPath”。 “name”是要匹配的卷名称，“localPath”是开发计算机上的绝对路径。 例如：

```yaml
version: 0.1
volumeMounts:
  - name: default-token-*
    localPath: /var/run/secrets/kubernetes.io/serviceaccount
env:
  - name: KUBERNETES_IN_CLUSTER_CONFIG_OVERRIDE
    value: $(volumeMounts:default-token-*)
```

上面的示例使用“env”中的条目来下载与 default-token-\* 匹配的卷，如 default-token-1111  或 default-token-1234-5678-90abcdef。 在多个卷匹配的情况下，使用第一个匹配的卷。 使用“volumeMounts”中的条目，将所有文件下载到开发计算机上的 `/var/run/secrets/kubernetes.io/serviceaccount`。 将 KUBERNETES_IN_CLUSTER_CONFIG_OVERRIDE 环境变量设置为 `/var/run/secrets/kubernetes.io/serviceaccount`。

## <a name="make-a-service-available"></a>使服务可用

在“env”下，为你需要在开发计算机上提供的每个服务指定“name”和“value”。 “name”是将在开发计算机上使用的环境变量。 “value”是群集中服务的名称和路径。 “value”的值采用 $(services:SERVICE_NAME)/PATH 的形式。

例如：

```yaml
version: 0.1
env:
  - name: MYAPP1_SERVICE_HOST
    value: $(services:myapp1)/api/v1/
```

上面的示例使 myapp1 服务可用于开发计算机，并将 MYAPP1_SERVICE_HOST 环境变量设置为 myapp1 服务的本地 IP 地址加上 `/api/v1` 路径（即 `127.1.1.4/api/v1`）。 使用环境变量、myapp1 或 myapp1.svc.cluster.local 都可以访问 myapp1 服务 。

> [!NOTE]
> 在你的开发计算机上提供服务时，无论你设置的路径是什么，都会使整个服务可用。 该路径仅用于设置开发计算机上使用的环境变量。
另外，还可以使用 $(services:SERVICE_NAME.NAMESPACE_NAME) 使特定 Kubernetes 命名空间中的服务可用。 例如：

```yaml
version: 0.1
env:
  - name: MYAPP2_SERVICE_HOST
    value: $(services:myapp2.mynamespace)
```

上面的示例使 mynamespace 命名空间中的 myapp2 服务可用于开发计算机，并将 MYAPP2_SERVICE_HOST 环境变量设置为 mynamespace 命名空间中的 myapp2 的本地 IP 地址 。

## <a name="create-an-environment-variable-with-a-constant-value"></a>创建一个具有常数值的环境变量

在“env”下，为你需要在开发计算机上创建的每个环境变量指定“name”和“value”。 “name”是将在开发计算机上使用的环境变量，“value”表示值。 例如：

```yaml
version: 0.1
env:
  - name: DEBUG_MODE
    value: "true"
```

上面的示例创建一个名为 DEBUG_MODE 的环境变量，其值为 true。

## <a name="example-kuberneteslocalprocessconfigyaml"></a>示例 KubernetesLocalProcessConfig.yaml

下面是完整的 `KubernetesLocalProcessConfig.yaml` 文件的示例：

```yaml
version: 0.1
volumeMounts:
  - name: default-token-*
    localPath: /var/run/secrets/kubernetes.io/serviceaccount
env:
  - name: KUBERNETES_IN_CLUSTER_CONFIG_OVERRIDE
    value: $(volumeMounts:default-token-*)
  - name: ALLOW_LIST_PATH
    value: $(volumeMounts:allow-list)/allow-list
  - name: MYAPP1_SERVICE_HOST
    value: $(services:myapp1)/api/v1/
  - name: MYAPP2_SERVICE_HOST
    value: $(services:myapp2.mynamespace)
  - name: DEBUG_MODE 
    value: "true"
```

## <a name="next-steps"></a>后续步骤

若要开始使用 Local Process with Kubernetes 将本地开发计算机连接到群集，请参阅[通过 Visual Studio Code 使用 Local Process with Kubernetes][local-process-kubernetes-vs-code] 和 [通过 Visual Studio 使用 Local Process with Kubernetes][local-process-kubernetes-vs]。

[local-process-kubernetes-vs-code]: https://code.visualstudio.com/docs/containers/local-process-kubernetes
[local-process-kubernetes-vs]: local-process-kubernetes.md
