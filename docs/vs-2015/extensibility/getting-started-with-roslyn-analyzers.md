---
title: 入门与 Roslyn 分析器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2d45491fe031c01a31812f5ed4944f76d059cd60
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300018"
---
# <a name="getting-started-with-roslyn-analyzers"></a>Roslyn 分析器入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过在 Visual Studio 中运行基于项目的代码分析器，API 作者可将特定于域的代码分析作为其 NuGet 包的一部分进行传送。  由于这些分析器由 .NET Compiler Platform （代码名为 "Roslyn"）提供支持，因此，即使在完成行之前键入，它们也可能在代码中产生警告（不再等待生成代码来发现问题）。  分析器还可以通过 Visual Studio 灯泡提示符来显示自动代码修补程序，使您可以立即清理代码

## <a name="getting-started"></a>入门
[Roslyn 实时代码分析器简介和演练](https://msdn.microsoft.com/magazine/dn879356.aspx)

[添加代码修复演练：为用户提供分析器问题的修补程序](https://msdn.microsoft.com/magazine/dn904670.aspx)

[真实世界分析器对话简介和演练](https://channel9.msdn.com/events/Build/2015/3-725)

[真实的 Roslyn 分析器](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md)，还可以观看[对话](https://channel9.msdn.com/events/Build/2015/3-725)

[GitHub 上的几个示例，分为三类分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

[一些分析器讨论简介和教程](https://channel9.msdn.com/Events/dotnetConf/2015/NET-Compiler-Platform-Roslyn-Analyzers-and-the-Rise-of-Code-Aware-Libraries)

## <a name="other-resources"></a>其他资源
[GitHub OSS 站点上的更多文档](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)

[GitHub 上的 Roslyn 分析器实现的 FxCop 规则](https://github.com/dotnet/roslyn/tree/master/src/Diagnostics/FxCop)
