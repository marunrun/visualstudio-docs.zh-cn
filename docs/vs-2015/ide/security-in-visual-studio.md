---
title: 安全
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code access security, coding errors
- security [.NET Framework], about security
ms.assetid: 318c34ce-f643-468c-83a1-843196f5d845
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8d967bd1f7a425ccd9dda5a938535788d961352f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672879"
---
# <a name="security-in-visual-studio"></a>Visual Studio 中的安全性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你应该考虑应用程序开发的所有环节（从设计到部署）的安全性。 从尽可能安全地运行 Visual Studio 开始。 请参阅[用户权限](../ide/user-permissions-and-visual-studio.md)。

 若要高效地开发安全的应用程序，应对安全概念和开发所针对的平台的安全特性有基本的了解。 你还应对安全编码技术有所了解。

## <a name="understanding-security"></a>了解安全性
 [安全性](https://msdn.microsoft.com/library/9a9621d7-8883-4a4f-a874-65e8e09e20a6)描述 .NET Framework 代码访问安全性、基于角色的安全性、安全策略和安全工具。

## <a name="coding-for-security"></a>安全编码
 导致安全漏洞的大多数编码错误都是由于开发人员在处理用户输入时所做的假定错误，或者是由于他们对开发平台了解不够充分。

 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)提供对组件进行分类以解决安全性问题的准则。

 [安全性最佳做法](https://msdn.microsoft.com/library/86acaccf-cdb4-4517-bd58-553618e3ec42)讨论缓冲区溢出并提供 Microsoft Visual C++ 安全检查功能（由 /GS 编译时标志提供）的全面介绍。
