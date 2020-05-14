---
title: 使用罗斯林分析器入门 |微软文档
ms.date: 04/02/2018
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bc975ff4f142b85297c20f16ac399fce588c093b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711272"
---
# <a name="get-started-with-roslyn-analyzers"></a>使用罗斯林分析仪入门

借助 Visual Studio 中基于项目的实时代码分析器，API 作者可以将特定于域的代码分析作为 NuGet 包的一部分。 由于这些分析器由 .NET 编译器平台（代号为"Roslyn"）提供支持，因此，在您键入之前，甚至在您完成行之前，它们就可以在代码中生成警告（无需再等待构建代码以发现问题）。 分析器还可以通过 Visual Studio 灯泡提示器显示自动代码修复，以便您立即清理代码。

## <a name="get-started"></a>入门

[罗斯林分析仪概述](../code-quality/roslyn-analyzers-overview.md)

[教程：编写第一个分析器和代码修补程序](/dotnet/csharp/roslyn-sdk/tutorials/how-to-write-csharp-analyzer-code-fix)

[添加代码修复演练：为用户提供分析器问题的修复](https://msdn.microsoft.com/magazine/dn904670.aspx)

[现实世界罗斯林分析器](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md)，您也可以观看作为[谈话](https://channel9.msdn.com/events/Build/2015/3-725)

[GitHub 的几个示例，分为三种分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

## <a name="see-also"></a>请参阅

- [.NET 编译器平台包版本引用](roslyn-version-support.md)
- [GitHub OSS 网站上的更多文档](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
- [使用罗斯林分析仪实现的FxCop规则](../code-quality/fxcop-rule-port-status.md)
