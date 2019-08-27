---
title: .NET 编译器平台 (&quot;Roslyn&quot;) 可扩展性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 564201b3-1e18-4b88-b615-42c2f57f3fe8
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fba277731444a294f276f43cc67b098039f4a64f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204722"
---
# <a name="net-compiler-platform-quotroslynquot-extensibility"></a>.NET 编译器平台 (&quot;Roslyn&quot;) 扩展性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

.NET 编译器平台 ("Roslyn") 的核心任务是打开的 C# 和 Visual Basic 编译器，并允许工具和开发人员能够在丰富的信息的编译器中共享具有有关程序。 代码分析工具提高代码质量和代码生成器的帮助，在应用程序的构造。 随着工具更智能，他们需要访问越来越多的仅由编译器拥有极深代码知识。 而不是作为不透明转换器 （中的源代码和对象代码），Roslyn 编译器提供的 Api 可用于与代码相关工具和应用程序中的任务。  
  
 最妙的是 Roslyn 编译器、 其 Api、 示例和演练和基于这些 Api 构建的真正工具是在所有完全开放源代码[github.com/dotnet/roslyn](https://github.com/dotnet/Roslyn)。 请转到要了解详细信息并开始使用 Roslyn 的 OSS 站点。 将查找链接以获取最新的 C# 和 VB 功能，可以使用作为最终用户，以及链接，开始为利用 Roslyn Api 的工具生成器。  
  
## <a name="see-also"></a>请参阅  
 [Roslyn 分析器入门](../extensibility/getting-started-with-roslyn-analyzers.md)
