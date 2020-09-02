---
title: .NET Compiler Platform (&quot; Roslyn &quot;) 扩展性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 564201b3-1e18-4b88-b615-42c2f57f3fe8
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fba277731444a294f276f43cc67b098039f4a64f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204722"
---
# <a name="net-compiler-platform-quotroslynquot-extensibility"></a>.NET 编译器平台 (&quot;Roslyn&quot;) 扩展性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

.NET Compiler Platform ( "Roslyn" ) 的核心任务是打开 c # 和 Visual Basic 编译器，并允许工具和开发人员在丰富的信息编译器中共享程序。 代码分析工具改善了代码质量，并在应用程序构造中提供了代码生成器帮助。 随着工具更智能化，他们需要访问仅有编译器拥有的更深入的代码知识。 Roslyn 编译器提供了 Api，可用于工具和应用程序中与代码相关的任务，而不是在和对象代码 out) 中 (源代码。  
  
 最重要的一点是，Roslyn 编译器、其 Api、示例和演练以及基于这些 Api 构建的实际工具都是 [github.com/dotnet/roslyn](https://github.com/dotnet/Roslyn)的完全开放源代码。 若要了解详细信息并开始 Roslyn，请转到 OSS 站点。 你将找到可获得最新的 c # 和 VB 功能的链接，你可以将其用作最终用户，也可以使用 Roslyn Api 作为工具生成器入门的链接。  
  
## <a name="see-also"></a>另请参阅  
 [Roslyn 分析器入门](../extensibility/getting-started-with-roslyn-analyzers.md)
