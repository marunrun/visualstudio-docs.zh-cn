---
title: .NET 编译器平台&quot;（&quot;罗斯林 ） 可扩展性 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 564201b3-1e18-4b88-b615-42c2f57f3fe8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 62ceac6e2be8a0a84d82f6b86b685c7c8b20a182
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712078"
---
# <a name="net-compiler-platform-quotroslynquot-extensibility"></a>.NET 编译器平台&quot;（&quot;罗斯林 ） 可扩展性
.NET 编译器平台 （"Roslyn"） 的核心任务是打开 C# 和 Visual Basic 编译器，并允许工具和开发人员共享编译器对程序的丰富信息。 代码分析工具提高了代码质量，代码生成器有助于应用程序构建。 随着工具变得越来越智能，他们需要访问越来越多的只有编译器才具备的深层代码知识。 Roslyn 编译器不是不透明的转换器（源代码和对象代码出），而是提供 API，可用于工具和应用程序中的代码相关任务。

 最好的部分是，Roslyn 编译器、它们的 API、示例和演练，以及基于这些 API 构建的实际工具都是[github.com/dotnet/roslyn](https://github.com/dotnet/Roslyn)完全开源的。 请访问 OSS 网站了解更多信息，并开始使用罗斯林。 您将找到链接来获取最新的 C# 和 Visual Basic 功能，这些功能可用于最终用户，以及利用 Roslyn API 开始作为工具生成器的链接。

## <a name="see-also"></a>请参阅
- [使用罗斯林分析仪入门](../extensibility/getting-started-with-roslyn-analyzers.md)
