---
title: 使用罗斯林分析器入门 |微软文档
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a712697bafefcf115ce10d110c0ef3a4270c6acd
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444959"
---
# <a name="getting-started-with-roslyn-analyzers"></a>Roslyn 分析器入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

借助 Visual Studio 中基于项目的实时代码分析器，API 作者可以将特定于域的代码分析作为 NuGet 包的一部分。  由于这些分析器由 .NET 编译器平台（代号为"Roslyn"）提供支持，因此，在您键入之前，甚至在您完成行之前，它们就可以在代码中生成警告（无需再等待构建代码以发现问题）。  分析仪还可以通过 Visual Studio 灯泡提示器显示自动代码修复，以便您立即清理代码

## <a name="getting-started"></a>入门
[罗斯林实时代码分析仪简介和演练](https://msdn.microsoft.com/magazine/dn879356.aspx)

[添加代码修复演练：为分析器问题为用户提供修复](https://msdn.microsoft.com/magazine/dn904670.aspx)

[真实世界分析仪讲座的介绍与演练](https://channel9.msdn.com/events/Build/2015/3-725)

[现实世界罗斯林分析器](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md)，您也可以观看作为[谈话](https://channel9.msdn.com/events/Build/2015/3-725)

[GitHub 的几个示例，分为三种分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

[几个分析器谈话的介绍和旅游](https://channel9.msdn.com/Events/dotnetConf/2015/NET-Compiler-Platform-Roslyn-Analyzers-and-the-Rise-of-Code-Aware-Libraries)

## <a name="other-resources"></a>其他资源
[GitHub OSS 网站上的更多文档](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)

[在 GitHub 上使用 Roslyn 分析器实现的 FxCop 规则](https://github.com/dotnet/roslyn/tree/master/src/Features/Core/Portable/Diagnostics/Analyzers)
