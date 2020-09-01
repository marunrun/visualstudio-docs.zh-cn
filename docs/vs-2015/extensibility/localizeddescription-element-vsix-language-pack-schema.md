---
title: " (VSIX 语言包架构) 的 LocalizedDescription 元素 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
ms.assetid: 766a1732-bbaf-4875-b276-feb42169633a
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 49bf12f3056eb7ddb0e0afb8333a1f1893c7b954
ms.sourcegitcommit: 26178b116cbf7353fee6ca989b8d872114f7b405
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284328"
---
# <a name="localizeddescription-element-vsix-language-pack-schema"></a>LocalizedDescription 元素（VSIX 语言包架构）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

必需。 提供扩展的本地化说明。  
  
## <a name="syntax"></a>语法  
  
```  
<LocalizedDescription>Localized description of the extension</LocalizedDescription>  
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
 必需。 以目标语言扩展的文本说明。  
  
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
