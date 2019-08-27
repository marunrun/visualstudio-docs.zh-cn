---
title: 支持多个版本的 Visual Studio 2015 |Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8f4393a88a689e2a923291ada37a9b6d85718db5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431359"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>支持多个版本的 Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

术语 *-并行*意味着您可以安装和维护多个版本的同一台计算机上的产品。 对 Vspackage，这意味着用户可以有多个 Visual Studio 版本安装在同一台计算机上。 但是，不能具有你的 Vspackage 加载到单个版本的 Visual Studio 的并行的版本。

 使你的 VSPackage 可以被加载到 Visual Studio 的并行版本之前，请考虑以下方面：

- 您必须确定你想要遵循哪个-同时实施策略。

     有关详细信息，请参阅[之间共享选择和版本控制的 Vspackage](../extensibility/choosing-between-shared-and-versioned-vspackages.md)。

- 您的解决方案和项目文件格式必须符合实施策略。

     有关详细信息，请参阅[升级自定义项目](../misc/upgrading-custom-projects.md)并[注册的文件扩展名的并行部署](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)。

- 您的安装程序必须处理实施策略，以便版本化的组件，以及所有版本之间共享的组件正确安装和注册。

     有关详细信息，请参阅[使用 Windows Installer 安装 Vspackage](../extensibility/internals/installing-vspackages-with-windows-installer.md)以及[组件管理](../extensibility/internals/component-management.md)。

    > [!NOTE]
    > 安装版本的 Visual Studio 还会安装相应版本的[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]。 例如，在同一台计算机上安装 Visual Studio 2010 和 Visual Studio 2012 还会安装版本 4.0 和 4.5 的[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]分别。

## <a name="in-this-section"></a>本节内容
 [选择之间共享和版本控制的 Vspackage](../extensibility/choosing-between-shared-and-versioned-vspackages.md)说明了如何解决你的 VSPackage 中的并行问题。

 [通过并行部署注册文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)描述你的 VSPackage 如何通过并行方案中注册文件关联。

## <a name="related-sections"></a>相关章节
 [安装 Vspackage](../misc/installing-vspackages.md)讨论了如何生成和安装 Vspackage 以及如何支持同时运行多个版本的 Visual Studio 的用户。
