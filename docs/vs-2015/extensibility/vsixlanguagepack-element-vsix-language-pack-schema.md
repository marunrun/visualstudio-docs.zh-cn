---
title: VSIXLanguagePack 元素 （VSIX 语言包架构） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
ms.assetid: 767f5c22-8b87-49ca-92aa-a7a3f026469f
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9a429a97c25f9c0215f17b024d34fece20d1d8f0
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65690705"
---
# <a name="vsixlanguagepack-element-vsix-language-pack-schema"></a>VSIXLanguagePack 元素 （VSIX 语言包架构）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

必需。 VSIX 语言包中提供的根元素。 VSIX 语言包提供本地化的安装 VSIX 包的信息。  
  
## <a name="syntax"></a>语法  
  
```  
<VSIXLanguagePack>  
  <LocalizedName>...</LocalizedName>  
  <LocalizedDescription>...</LocalizedDescription>  
  <MoreInfoURL>...</MoreInfoURL>  
  <License>...</License>  
</VSIXLanguagePack>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`xmlns`|在其中定义 VSIX 语言包架构的 XML 命名空间。|  
  
## <a name="xmlns-attribute"></a>xmlns 特性  
  
|值|描述|  
|-----------|-----------------|  
|`http://schemas.microsoft.com/developer/vsx-schema-lp/2010`|必需。 定义对语言包架构文件的位置。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[LocalizedName 元素](../extensibility/localizedname-element-vsix-language-pack-schema.md)|必需。 要安装的扩展插件的本地化的名称。|  
|[LocalizedDescription 元素](../extensibility/localizeddescription-element-vsix-language-pack-schema.md)|必需。 要安装的扩展插件的本地化的说明。|  
|[MoreInfoURL 元素](../extensibility/moreinfourl-element-vsix-language-pack-schema.md)|可选。 有关扩展的本地化信息的链接。|  
|[License 元素](../extensibility/license-element-vsix-language-pack-schema.md)|可选。 该扩展的许可证文件的本地化版本的路径。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|None||  
  
## <a name="element-information"></a>元素信息  
  
|                 |                                                           |
|-----------------|-----------------------------------------------------------|
|    命名空间    | http://schemas.microsoft.com/developer/vsx-schema-lp/2010 |
|   架构名称   |                 VSIX 语言包架构                 |
| 验证文件 |                VSIXLanguagePackSchema.xsd                 |
|  可以为空   |                            否                             |
  
## <a name="see-also"></a>请参阅  
 [VSX 语言包架构参考](../extensibility/vsx-language-pack-schema-reference.md)   
 [本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)   
 [VSIX 扩展架构 1.0 参考](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)
