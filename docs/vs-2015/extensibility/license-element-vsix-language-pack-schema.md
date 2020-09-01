---
title: " (VSIX 语言包架构) 的许可证元素 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
ms.assetid: 57dac3b7-0cdd-405c-9af5-30ed9ca45e53
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f1299d97cbda78049732d3367a9231272397e2ec
ms.sourcegitcommit: 26178b116cbf7353fee6ca989b8d872114f7b405
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284377"
---
# <a name="license-element-vsix-language-pack-schema"></a>License 元素（VSIX 语言包架构）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可选。 扩展的许可证文件的本地化版本的路径。  
  
## <a name="syntax"></a>语法  
  
```  
<License>FilePath\license.txt</License>  
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
 要显示的本地化许可证文件的相对路径。  
  
## <a name="remarks"></a>备注  
 如果定义了该 `License` 元素，则在安装过程中将显示指定许可证文件的文本，并且用户必须接受许可证才能继续。  
  
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
