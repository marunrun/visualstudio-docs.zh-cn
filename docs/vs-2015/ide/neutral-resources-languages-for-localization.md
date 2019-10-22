---
title: 用于本地化的非特定资源语言 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- localization [Visual Studio], resources
- NeutralResourcesLanguageAttribute class
- globalization [Visual Studio], resources
- resources [Visual Studio], fallback system
- culture, locating resources
- neutral resources
ms.assetid: ef064995-3b84-4698-a708-9689b7723533
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 85e0be0172f27732f8efeb882cbcde5b9c6aef3d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670387"
---
# <a name="neutral-resources-languages-for-localization"></a>用于本地化的非特定资源语言
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:System.Resources.NeutralResourcesLanguageAttribute> 类指定包含在主程序集中的资源的区域性。 此属性作为增强性能使用，以便 <xref:System.Resources.ResourceManager> 对象不会搜索包含在主程序集中的资源。

 以下代码演示如何设置非特定资源语言。 可以将代码放置在生成脚本或 AssemblyInfo.vb 或 AssemblyInfo.cs 文件中。

```vb
' Set neutral resources language for assembly.
<Assembly: NeutralResourcesLanguageAttribute("en")>

```

```csharp
// Set neutral resources language for assembly.
[assembly: NeutralResourcesLanguageAttribute("en")]
```

## <a name="see-also"></a>另请参阅
 <xref:System.Resources.ResourceManager> 基于资源的 .NET Framework[分层组织](../ide/hierarchical-organization-of-resources-for-localization.md)的[国际化应用程序简介](../ide/introduction-to-international-applications-based-on-the-dotnet-framework.md)本地化[应用程序](../ide/localizing-applications.md)[全球化和本地化应用程序](../ide/globalizing-and-localizing-applications.md)
