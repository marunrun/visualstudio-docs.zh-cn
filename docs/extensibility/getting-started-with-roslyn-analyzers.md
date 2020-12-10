---
title: 入门与 Roslyn 分析器 |Microsoft Docs
description: 使用以下资源开始在 Visual Studio 中使用 Roslyn 分析器;包括教程和几个示例。
ms.custom: SEO-VS-2020
ms.date: 04/02/2018
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c63510083f227f617b2a11ddec07510ffd792433
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994350"
---
# <a name="get-started-with-roslyn-analyzers"></a>Roslyn 分析器入门

通过在 Visual Studio 中运行基于项目的代码分析器，API 作者可将特定于域的代码分析作为其 NuGet 包的一部分进行传送。 由于这些分析器由 .NET Compiler Platform 名为 "Roslyn ) " 的 (提供支持，因此，即使在完成该行之前键入，它们也可能在代码中产生警告 (不再需要等待生成代码即可发现问题) 。 分析器还可以通过 Visual Studio 灯泡提示符来显示自动代码修补程序，使您可以立即清理您的代码。

## <a name="get-started"></a>入门

[Roslyn 分析器概述](../code-quality/roslyn-analyzers-overview.md)

[教程：编写第一个分析器和代码修补程序](/dotnet/csharp/roslyn-sdk/tutorials/how-to-write-csharp-analyzer-code-fix)

[添加代码修复演练：为用户提供分析器问题的修补程序](/archive/msdn-magazine/2015/february/csharp-adding-a-code-fix-to-your-roslyn-analyzer)

[真实的 Roslyn 分析器](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md) ，还可以观看 [对话](https://channel9.msdn.com/events/Build/2015/3-725)

[GitHub 上的几个示例，分为三类分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

## <a name="see-also"></a>另请参阅

- [.NET 编译器平台包版本引用](roslyn-version-support.md)
- [GitHub OSS 站点上的更多文档](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
- [通过 Roslyn 分析器实现的 FxCop 规则](../code-quality/fxcop-rule-port-status.md)
