---
title: MSBuild 多定向概述 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: eecbcd65-9fbc-4307-a321-46d3c3b79b12
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d54209624a7413bb5d968f212e669a4be8171b43
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595912"
---
# <a name="msbuild-multitargeting-overview"></a>MSBuild 多定向概述
通过 MSBuild，可将应用程序编译为在若干 .NET Framework 版本的任一版本和若干系统平台的任一平台上运行。 例如，可将同一应用程序编译为既能在 32 位平台的 .NET Framework 2.0 上运行，也能在 64 位平台的 .NET Framework 4.5 上运行。

> [!IMPORTANT]
> 尽管名称为“多定向”，一个项目一次只能针对一个框架和一个平台。

 以下是 MSBuild 定向的部分功能：

- 可开发面向 .NET Framework 早期版本（例如，版本 2.0、3.5 或 4）的应用程序。

- 可以面向 .NET Framework 之外的框架，例如 Silverlight Framework。

- 可以一个*框架配置文件*为目标，该文件是目标框架的预定义子集。

- 如果已发布 .NET Framework 当前版本的 Service Pack，则可以将其作为目标。

- MSBuild 多定向功能可保证应用程序仅使用目标框架和平台中的可用功能。

## <a name="target-framework-and-platform"></a>目标框架和平台
 目标框架  是项目生成后要在其上运行的一个 .NET Framework 版本；目标平台  项目生成后要在其上运行的一个系统平台。  例如，你可能希望将 .NET Framework 2.0 应用程序的目标设定为在与 802x86 处理器系列 (x86) 兼容的 32 位平台上运行。 目标框架与目标平台的组合称为“目标上下文”  。 有关详细信息，请参阅[目标框架和目标平台](../msbuild/msbuild-target-framework-and-target-platform.md)。

## <a name="toolset-toolsversion"></a>工具集 (ToolsVersion)
 工具集可收集用于创建应用程序的工具、任务和目标。 工具集包括编译器（如 csc.exe 和 vbc.exe）、常见目标文件 (microsoft.common.targets) 及常见任务文件 (microsoft.common.tasks)     。 工具集 4.5 可用于面向 .NET Framework 版本 2.0、3.0、3.5、4 和 4.5。 但工具集 2.0 仅可用于面向 .NET Framework 版本 2.0。 有关详细信息，请参阅[工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)。

## <a name="reference-assemblies"></a>引用程序集
 工具集中指定的引用程序集有助于应用程序的设计和构建。 这些引用程序集不仅可启用特定的目标生成，还可将 Visual Studio IDE 中的组件和功能限制为与目标兼容的组件和功能。 有关详细信息，请参阅[在设计时解析程序集](../msbuild/resolving-assemblies-at-design-time.md)。

## <a name="configure-targets-and-tasks"></a>配置目标和任务
 通过 MSBuild 可配置要在进程外运行的 MSBuild 目标和任务，这样即可面向与当前运行所在的上下文有很大不同的上下文。  例如，当开发计算机在具有 .NET Framework 4.5 的 64 位平台上运行时，可面向 32 位 NET Framework 2.0 应用程序。 有关详细信息，请参阅[配置目标和任务](../msbuild/configuring-targets-and-tasks.md)。

## <a name="troubleshooting"></a>疑难解答
 如果尝试引用不属于目标上下文的程序集，则可能会遇到错误。 有关这些错误以及如何处理这些错误的详细信息，请参阅 [.NET Framework 目标错误疑难解答](../msbuild/troubleshooting-dotnet-framework-targeting-errors.md)。
