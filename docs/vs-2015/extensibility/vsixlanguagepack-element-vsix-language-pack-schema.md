---
title: VSIXLanguagePack 元素（VSIX 语言包架构） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
ms.assetid: 767f5c22-8b87-49ca-92aa-a7a3f026469f
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e2e1df362fddeab5be98ff90460a8a1a7d4b7876
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557999"
---
# <a name="vsixlanguagepack-element-vsix-language-pack-schema"></a>VSIXLanguagePack 元素（VSIX 语言包架构）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

必需。 提供 VSIX 语言包的根元素。 VSIX 语言包为 VSIX 包提供本地化的安装信息。  
  
## <a name="syntax"></a>语法  
  
```  
<VSIXLanguagePack>  
  <LocalizedName>...</LocalizedName>  
  <LocalizedDescription>...</LocalizedDescription>  
  <MoreInfoURL>...</MoreInfoURL>  
  <License>...</License>  
</VSIXLanguagePack>  
```  
  
## <a name="attributes-and-elements"></a>属性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>属性  
  
|Attribute|说明|  
|---------------|-----------------|  
|`xmlns`|在其中定义 VSIX 语言包架构的 XML 命名空间。|  
  
## <a name="xmlns-attribute"></a>xmlns 特性  
  
|值|说明|  
|-----------|-----------------|  
|`http://schemas.microsoft.com/developer/vsx-schema-lp/2010`|必需。 定义语言包架构的文件的位置。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|[LocalizedName 元素](../extensibility/localizedname-element-vsix-language-pack-schema.md)|必需。 要安装的扩展的本地化名称。|  
|[LocalizedDescription 元素](../extensibility/localizeddescription-element-vsix-language-pack-schema.md)|必需。 要安装的扩展的本地化说明。|  
|[MoreInfoURL 元素](../extensibility/moreinfourl-element-vsix-language-pack-schema.md)|可选。 指向有关扩展的本地化信息的链接。|  
|[License 元素](../extensibility/license-element-vsix-language-pack-schema.md)|可选。 扩展的许可证文件的本地化版本的路径。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|无||  
  
## <a name="element-information"></a>元素信息  
  
|                 |                                                           |
|-----------------|-----------------------------------------------------------|
|    命名空间    | `http://schemas.microsoft.com/developer/vsx-schema-lp/2010` |
|   架构名   |                 VSIX 语言包架构                 |
| 验证文件 |                VSIXLanguagePackSchema.xsd                 |
|  可以为空   |                            否                             |
  
## <a name="see-also"></a>另请参阅  
 [VSX 语言包架构引用](../extensibility/vsx-language-pack-schema-reference.md)[本地化 Vsix 包](../extensibility/localizing-vsix-packages.md) [vsix 扩展架构1.0 引用](/previous-versions/dd393700(v=vs.110))
