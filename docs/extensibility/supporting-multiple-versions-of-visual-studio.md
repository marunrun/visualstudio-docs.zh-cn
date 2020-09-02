---
title: 支持多个版本的 Visual Studio |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d571f1be4da45ff5ed6b2538cfb515930bde1de
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699479"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>支持多个版本的 Visual Studio
*术语 "并排"* 表示可以在同一台计算机上安装和维护产品的多个版本。 对于 Vspackage，这意味着用户可以在同一台计算机上安装多个 Visual Studio 版本。 但是，你不能将 Vspackage 的并行版本加载到单个版本的 Visual Studio 中。

 在将 VSPackage 加载到 Visual Studio 的并行版本之前，请考虑以下事项：

- 你必须确定要遵循的并行实现策略。

   有关详细信息，请参阅 [在 Shared 和 Vspackage 之间进行选择](../extensibility/choosing-between-shared-and-versioned-vspackages.md)。

- 解决方案和项目文件格式必须符合实现策略。

   有关详细信息，请参阅 [升级自定义项目](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects) 和 [注册并行部署的文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)。

- 安装程序必须处理实现策略，以便正确安装和注册已进行版本控制的组件以及跨所有版本共享的组件。

   有关详细信息，请参阅将 [Vspackage 与 Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md) 和 [组件管理](../extensibility/internals/component-management.md)一起安装。

  > [!NOTE]
  > 安装 Visual Studio 版本时，还会安装相应版本的 .NET Framework。 例如，在同一台计算机上安装 Visual Studio 2010 和 Visual Studio 2012 还将分别安装 .NET Framework 的4.0 和4.5。

## <a name="in-this-section"></a>本节内容
- [在共享和版本控制之间进行选择 vspackage](../extensibility/choosing-between-shared-and-versioned-vspackages.md) 说明如何在 VSPackage 中解析并行问题。

- [为并行部署注册文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md) 介绍 VSPackage 如何在并行方案中注册文件关联。

## <a name="related-sections"></a>相关章节
- [使用 Windows Installer 安装 VSPackage](../extensibility/internals/installing-vspackages-with-windows-installer.md)
