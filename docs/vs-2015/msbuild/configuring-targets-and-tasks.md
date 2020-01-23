---
title: 配置目标和任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
ms.assetid: 9aabe67a-1720-4bbf-80d3-822b3ccf75c0
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 892e9615599a8881e219c00f748a0cc1567d996d
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850036"
---
# <a name="configuring-targets-and-tasks"></a>配置目标和任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过 MSBuild 可以配置要在进程外运行的 MSBuild 目标和任务，以便面向当前运行所在的上下文之外的上下文。 例如，当开发计算机运行 64 位的 .NET Framework 4.5 操作系统时，可面向 32 位 NET Framework 2.0 应用程序。 还可以面向运行 .NET Framework 4 或更早版本的计算机。 32 或 64 位与特定 .NET Framework 版本的组合称为“目标上下文”。  
  
## <a name="installation"></a>安装  
 .NET Framework 4.5 和 4.5.1 替换了 .NET Framework 4 的公共语言运行时 (CLR)、目标、任务和工具，而没有进行重命名。 .NET Framework 4.5.1 作为 [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] 的一部分安装。  
  
 如果要单独安装 MSBuild 与 Visual Studio，可以从 [MSBuild 下载](https://www.microsoft.com/download/details.aspx?id=40760)下载安装软件包。 还必须安装所要使用的 .NET Framework 版本。  
  
## <a name="targets-and-tasks"></a>目标和任务  
 MSBuild 在进程外运行特定的生成任务，以面向更大的上下文集合。  例如，32 位 MSBuild 可在 64 位进程中运行生成任务，以面向 64 位计算机。 这是由 `UsingTask` 实参和 `Task` 形参控制的。 .NET Framework 4.5 安装的目标将设置这些自变量和参数，无需进行任何更改即可生成适用于各种目标上下文的应用程序。  
  
 如果要创建自己的目标上下文，必须正确设置这些实参和形参。 有关示例，请参阅 .NET Framework 4.5 Microsoft.Common.targets 文件和 Microsoft.Common.Tasks 文件。  有关如何创建可用于多个目标上下文的自定义任务或如何修改现有任务的信息，请参阅[如何；配置目标和任务](../msbuild/how-to-configure-targets-and-tasks.md)。  
  
## <a name="see-also"></a>请参阅  
 [多定向](../msbuild/msbuild-multitargeting-overview.md)
