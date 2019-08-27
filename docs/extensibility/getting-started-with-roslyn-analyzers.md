---
title: 入门与 Roslyn 分析器 |Microsoft Docs
ms.date: 04/02/2018
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 21b2d77d8c038988fa77293280c9ff7ad38cc82e
ms.sourcegitcommit: 90c3187d804ad7544367829d07ed4b47d3f8a72d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68822340"
---
# <a name="get-started-with-roslyn-analyzers"></a>Roslyn 分析器入门

通过在 Visual Studio 中运行基于项目的代码分析器, API 作者可将特定于域的代码分析作为其 NuGet 包的一部分进行传送。 由于这些分析器由 .NET Compiler Platform (代码名为 "Roslyn") 提供支持, 因此, 即使在完成行之前键入, 它们也可能在代码中产生警告 (不再等待生成代码来发现问题)。 分析器还可以通过 Visual Studio 灯泡提示符来显示自动代码修补程序, 使您可以立即清理您的代码。

## <a name="get-started"></a>入门

[Roslyn 分析器概述](../code-quality/roslyn-analyzers-overview.md)

[教程：编写您的第一个分析器和代码修补程序](/dotnet/csharp/roslyn-sdk/tutorials/how-to-write-csharp-analyzer-code-fix)

[添加代码修复演练:为分析器问题提供用户修补程序](https://msdn.microsoft.com/magazine/dn904670.aspx)

[真实的 Roslyn 分析器](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md), 还可以观看[对话](https://channel9.msdn.com/events/Build/2015/3-725)

[GitHub 上的几个示例, 分为三类分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

## <a name="see-also"></a>请参阅

- [.NET 编译器平台包版本引用](roslyn-version-support.md)
- [GitHub OSS 站点上的更多文档](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
- [通过 Roslyn 分析器实现的 FxCop 规则](../code-quality/fxcop-rule-port-status.md)
