---
title: 安全性和已本地化的附属程序集 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- key pairs for strong-named assemblies
- strong-named assemblies, security considerations
- satellite assemblies, localized
- code signing, assemblies
- security [Visual Studio], assemblies
- strong-named assemblies, localized
- assemblies [Visual Studio], security
- localization, satellite assemblies
ms.assetid: 6d953840-b301-47d5-8d34-30c1b29b5071
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9c810c6c7e0c0c73557e6b38860c1e6d3953b225
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691291"
---
# <a name="security-and-localized-satellite-assemblies"></a>安全性和已本地化的附属程序集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果主程序集使用强命名，则必须使用与主程序集相同的私钥对附属程序集进行签名。 如果主程序集和附属程序集之间的公钥/私钥对不匹配，则不会加载资源。 有关对程序集签名的详细信息，请参阅[如何：使用强名称为程序集签名](https://msdn.microsoft.com/library/2c30799a-a826-46b4-a25d-c584027a6c67)。  
  
 通常，可能需要要求你组织的签名组或外部签名组织使用私钥进行签名。 这是因为私钥具有敏感性：访问通常限制为少数几个人。 可以在开发期间使用延迟签名。 有关详细信息，请参阅[延迟为程序集签名](https://msdn.microsoft.com/library/9d300e17-5bf1-4360-97da-2aa55efd9070)。  
  
## <a name="see-also"></a>请参阅  
 [程序集安全注意事项](https://msdn.microsoft.com/library/1b5439c1-f3d5-4529-bd69-01814703d067)   
 [秘钥安全性概念](https://msdn.microsoft.com/library/3cfced4f-ea02-4e66-ae98-d69286363e98)   
 [基于 .NET Framework 的国际应用程序简介](../ide/introduction-to-international-applications-based-on-the-dotnet-framework.md)   
 [本地化应用程序](../ide/localizing-applications.md)   
 [对应用程序进行全球化和本地化](../ide/globalizing-and-localizing-applications.md)
