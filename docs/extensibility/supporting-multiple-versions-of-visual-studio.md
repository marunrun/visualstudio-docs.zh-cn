---
title: 支持多个版本的视觉工作室 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699479"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>支持多个版本的 Visual Studio
并排术语*意味着*您可以在同一台计算机上安装和维护产品的多个版本。 对于 VSPackages，这意味着用户可以在同一台计算机上安装多个 Visual Studio 版本。 但是，您不能将 VS 包的并行版本加载到 Visual Studio 的单个版本中。

 在使 VSPackage 能够加载到并行版本的 Visual Studio 之前，请考虑以下事项：

- 您必须确定要遵循的并行实现策略。

   有关详细信息，请参阅[在共享和版本化 VS 包之间进行选择](../extensibility/choosing-between-shared-and-versioned-vspackages.md)。

- 您的解决方案和项目文件格式必须适合您的实施策略。

   有关详细信息，请参阅[升级自定义项目和](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)[注册并行部署的文件名称扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)。

- 安装程序必须处理实现策略，以便正确安装和注册版本控制组件以及跨所有版本共享的组件。

   有关详细信息，请参阅[安装带有 Windows 安装程序的 VS 包](../extensibility/internals/installing-vspackages-with-windows-installer.md)以及[组件管理](../extensibility/internals/component-management.md)。

  > [!NOTE]
  > 安装 Visual Studio 版本还会安装相应的 .NET 框架版本。 例如，在同一台计算机上安装 Visual Studio 2010 和 Visual Studio 2012 也分别安装 .NET Framework 的 4.0 和 4.5 版本。

## <a name="in-this-section"></a>本节内容
- [在共享和版本化 VS 包之间进行选择](../extensibility/choosing-between-shared-and-versioned-vspackages.md)说明如何解决 VS 包中的并排问题。

- [注册并行部署的文件名扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)描述 VSPackage 如何在并行方案中注册文件关联。

## <a name="related-sections"></a>相关章节
- [使用 Windows Installer 安装 VSPackage](../extensibility/internals/installing-vspackages-with-windows-installer.md)
