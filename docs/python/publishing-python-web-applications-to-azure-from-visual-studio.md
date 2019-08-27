---
title: 将 Python 应用发布到 Azure 应用服务
description: 有关将 Python 应用发布到 Azure 应用服务的选项，包括 Git 部署和用于 Linux 的容器，以及部署到 IIS。
ms.date: 03/13/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: c3c8d6c16f2f7e432b6b5e988bf63521f3dfc8c0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62784110"
---
# <a name="publish-to-azure-app-service"></a>发布到 Azure 应用服务

目前，仅适用于 Linux 的 Azure 应用服务支持 Python，可按照本文所述使用 [Git deploy](#publish-to-app-service-on-linux-using-git-deploy) 和[容器](#publish-to-app-service-on-linux-using-containers)发布应用。

> [!Note]
> 适用于 Windows 的 Azure 应用服务对的 Python 支持已遭正式弃用。 因此，仅 [IIS 目标](#publish-to-iis)正式支持 Visual Studio 中的“发布”命令，Azure 应用服务中的远程调试功能已不再正式受支持。
>
> 不过，[发布到 Windows 上的应用服务](publish-to-app-service-windows.md)功能目前仍有效，因为 Windows 上的应用服务适用的 Python 扩展仍可用，但我们不再会为它提供服务或更新它。

## <a name="publish-to-app-service-on-linux-using-git-deploy"></a>使用 Git 部署流程发布到 Linux 上的应用服务

Git 部署流程可将 Linux 上的应用服务连接到 Git 存储库的特定分支。 向相应分支提交的代码会自动部署到应用服务，并且应用服务会自动安装 requirements.txt 中列出的任何依赖项。 在此示例中，Linux 上的应用服务在使用 Gunicorn Web 服务器的预配置容器映像中运行代码。 目前，此服务处于预览阶段，不支持用于生产。

有关详细信息，请参阅 Azure 文档中的以下文章：

- [快速入门：在应用服务中创建 Python Web 应用](/azure/app-service/containers/quickstart-python?toc=%2Fpython%2Fazure%2FTOC.json)使用简单的 Flask 应用和本地 Git 存储库中的部署，快速演示了 Git 部署流程。
- [如何配置 Python](/azure/app-service/containers/how-to-configure-python) 介绍了 Linux 容器上的应用服务的特征，以及如何自定义应用的 Gunicorn 启动命令。

## <a name="publish-to-app-service-on-linux-using-containers"></a>使用容器发布到 Linux 上的应用服务

可提供你自己的容器，而不用依赖 Linux 上的应用服务随附的预生成容器。 借助此选项，可选择要使用的 Web 服务器，并能自定义容器行为。

生成、管理和推送容器的方法有以下两种：

- 使用 Visual Studio Code 和 Docker 扩展，如[使用 Docker 容器部署 Python 应用](https://code.visualstudio.com/docs/python/tutorial-deploy-containers)中所述。 即使不使用 Visual Studio Code，这篇文章还详细介绍了如何使用生产就绪的 uwsgi 和 nginx Web 服务器，以生成 Flask 和 Django 应用的容器映像。 然后便可以使用 Azure CLI 部署这些相同的容器。

- 使用命令行和 Azure CLI，如 Azure 文档中的[使用自定义 Docker 映像](/azure/app-service/containers/tutorial-custom-docker-image)一文所述。 不过，此为通用指南，不是 Python 专用指南。

## <a name="publish-to-iis"></a>发布到 IIS

在 Visual Studio 中，可以将应用发布到 Windows 虚拟机，或其他运行 IIS 且包含“发布”命令的计算机。 使用 IIS 时，请务必在应用中创建或修改 web.config 文件，以指示 IIS 在哪里能找到 Python 解释器。 有关详细信息，请参阅[为 Web 应用配置 IIS](configure-web-apps-for-iis-windows.md)。
