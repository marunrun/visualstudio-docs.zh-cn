---
title: 开始使用 Roslyn 分析器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 104e3a30589f5892c1440266afd7917486d704ec
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546643"
---
# <a name="getting-started-with-roslyn-analyzers"></a>Roslyn 分析器入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过在 Visual Studio 中的实时、 基于项目的代码分析器，API 作者可以提供特定于域的代码分析作为其 NuGet 包的一部分。  这些分析器由.NET 编译器平台 (代号为"Roslyn") 提供支持，因为它们可能会产生警告在代码中的，键入即使之前已完成 （不再等到生成代码以便发现问题） 的行。  分析器，还可能会出现通过 Visual Studio 灯泡图标提示来让您立即清理代码的自动代码修补程序

## <a name="getting-started"></a>入门
[Roslyn 实时代码分析器说明和演练](https://msdn.microsoft.com/magazine/dn879356.aspx)

[添加代码修复演练：分析器问题提供用户的修补程序](https://msdn.microsoft.com/magazine/dn904670.aspx)

[说明和演练的现实世界分析器讨论](http://channel9.msdn.com/events/Build/2015/3-725)

[真实世界 Roslyn 分析器](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md)，还可查看作为[通信](http://channel9.msdn.com/events/Build/2015/3-725)

[GitHub 上的几个示例分为三种类型的分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

[简介和教程的几个分析器通信](http://channel9.msdn.com/Events/dotnetConf/2015/NET-Compiler-Platform-Roslyn-Analyzers-and-the-Rise-of-Code-Aware-Libraries)

## <a name="other-resources"></a>其他资源
[GitHub OSS 站点上的多个文档](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)

[FxCop 规则实现通过 GitHub 上的 Roslyn 分析器](https://github.com/dotnet/roslyn/tree/master/src/Diagnostics/FxCop)
