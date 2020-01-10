---
title: Content_types] .xml 文件的结构 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- content_types
- content types
- opc
- vsix
ms.assetid: 9c399598-b9fa-4da7-84b5-defbf82e9335
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3185b70f74478a9a55c4fb918c1535c86d154c76
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75846371"
---
# <a name="the-structure-of-the-content_typesxml-file"></a>[Content_types].xml 文件的结构
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含有关 VSIX 包中的内容种类的信息。 Visual Studio 使用 [Content_Types] .xml 文件来安装包，但不会安装文件本身。  
  
> [!NOTE]
> 尽管本主题仅适用于 VSIX 包中使用的 [Content_Type] .xml 文件，但 [Content_Types] .xml 文件类型是*开放打包约定（OPC）* 标准的一部分。 有关详细信息，请参阅 MSDN 网站上的[OPC：用于打包数据的新标准](https://msdn.microsoft.com/magazine/cc163372.aspx)。  
  
## <a name="attributes-and-elements"></a>属性和元素  
 以下各节描述了 root 元素及其属性和子元素。  
  
### <a name="root-element"></a>根元素  
  
|元素|描述|  
|-------------|-----------------|  
|`Types`|包含枚举 VSIX 包中的文件类型的子元素。|  
  
### <a name="attributes"></a>特性  
  
|属性|描述|  
|---------------|-----------------|  
|`Xmlns`|（必需。）用于此 [Content_Types] .xml 文件的架构的位置。|  
  
### <a name="attribute-name-attribute"></a>{Attribute name}Attribute  
  
|                           {2&gt;值&lt;2}                           |                描述                |
|-----------------------------------------------------------|-------------------------------------------|
| http://schemas.openformats.org/package/2006/content-types | 内容类型架构的位置。 |
  
### <a name="child-elements"></a>子元素  
 `Types` 元素可包含任意数量的 `Default` 元素。  
  
|元素|描述|  
|-------------|-----------------|  
|`Default`|描述 VSIX 包中的内容类型。 包中的每个文件类型都必须有自己的 `Default` 元素。|  
  
### <a name="attributes"></a>特性  
  
|属性|描述|  
|---------------|-----------------|  
|`Extension`|VSIX 包中文件的文件扩展名。|  
|`ContentType`|描述与文件扩展名关联的内容类型。|  
  
### <a name="attribute-name-attribute"></a>{Attribute name}Attribute  
 Visual Studio 可识别关联 `Extension` 类型的以下 `ContentType` 值。  
  
|扩展名|ContentType|  
|---------------|-----------------|  
|txt|text/plain|  
|.pkgdef|text/plain|  
|xml|text/xml|  
|vsixmanifest|text/xml|  
|htm 或 html|文本/html|  
|rtf|application/rtf|  
|pdf|application/pdf|  
|gif|image/gif|  
|jpg 或 jpeg|image/jpg|  
|tiff|image/tiff|  
|vsix|应用程序/zip|  
|zip|应用程序/zip|  
|dll|application/octet-stream|  
|所有其他文件类型|application/octet-stream|  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的 [Content_Types] .xml 文件描述了一个典型的 VSIX 包。  
  
### <a name="code"></a>代码  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<Types xmlns="http://schemas.openxmlformats.org/package/2006/content-types">  
    <Default Extension="vsixmanifest" ContentType="text/xml" />   
    <Default Extension="dll" ContentType="application/octet-stream" />   
    <Default Extension="png" ContentType="application/octet-stream" />   
    <Default Extension="txt" ContentType="text/plain" />   
    <Default Extension="pkgdef" ContentType="text/plain" />   
</Types>  
```  
  
## <a name="see-also"></a>请参阅  
 [VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)   
 [VSIX 扩展架构1.0 引用](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)   
 [OPC：用于打包数据的新标准](https://msdn.microsoft.com/magazine/cc163372.aspx)
