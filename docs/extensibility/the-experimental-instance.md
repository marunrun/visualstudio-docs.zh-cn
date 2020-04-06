---
title: 实验实例 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- VSPackages, experimental builds
- VSIP, experimental builds
ms.assetid: ead0df4e-6f88-4b42-9297-581b7902f050
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e2284767a0aa6be58c0f7e38c912783728914cb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699042"
---
# <a name="the-experimental-instance"></a>实验实例
为了保护您的 Visual Studio 开发环境免受可能更改它的未经测试的应用程序的影响，VSSDK 提供了一个实验空间，可用于实验。 像往常一样使用 Visual Studio 来开发新应用程序，但使用此实验实例运行它们。

 每个具有 VSIX 包的应用程序都会在调试模式下启动 Visual Studio 实验实例。

 如果要在特定解决方案之外启动 Visual Studio 的实验实例，在命令窗口中运行以下命令：

 "*\<视觉工作室安装路径>*[公共7_IDE_devenv.exe] /RootSuffix Exp

> [!NOTE]
> 实验实例写入`<version number>Exp`和`<version number>Exp_Config`节点下的注册表。 例如，Visual Studio 2015 实验注册表区域是
>
> `HKCU\Software\Microsoft\VisualStudio\14.0Exp` 和 `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`

 我们建议您在开发扩展时在实验实例中运行扩展。 部署扩展时，它将在开发实例中运行。 有关注册应用程序的详细信息，请参阅[注册 VS 包](../extensibility/internals/registering-vspackages.md)。
