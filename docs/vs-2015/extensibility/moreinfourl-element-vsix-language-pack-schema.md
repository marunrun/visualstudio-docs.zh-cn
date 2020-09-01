---
title: " (VSIX 语言包架构) 的其他元素 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
ms.assetid: 3f07b67b-95c5-4ae8-8b7e-d643cbbb0348
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c583d67e1920080f11158a4001e191e93e234006
ms.sourcegitcommit: 26178b116cbf7353fee6ca989b8d872114f7b405
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284390"
---
# <a name="moreinfourl-element-vsix-language-pack-schema"></a> MoreInfoURL元素（VSIX 语言包架构）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可选。 指向有关扩展的本地化信息的链接。  
  
## <a name="syntax"></a>语法  
  
```  
<MoreInfoURL>URL</MoreInfoURL>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|无||  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|无||  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[VSIX LanguagePack 元素](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md)|必需。 提供 VSIX 语言包的根元素。|  
  
## <a name="text-value"></a>文本值  
 可选。 指向网站的链接。 链接是文本字符串。  
  
## <a name="element-information"></a>元素信息  
  
|                 |                                                           |
|-----------------|-----------------------------------------------------------|
|    命名空间    | `http://schemas.microsoft.com/developer/vsx-schema-lp/2010` |
|   架构名称   |                 VSIX 语言包架构                 |
| 验证文件 |                VSIXLanguagePackSchema                 |
|  可以为空   |                      不适用                       |
  
## <a name="see-also"></a>另请参阅  
 [VSX 语言包架构引用](../extensibility/vsx-language-pack-schema-reference.md)   
 [本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)   
 [VSIX 扩展架构1.0 引用](/previous-versions/dd393700(v=vs.110))
