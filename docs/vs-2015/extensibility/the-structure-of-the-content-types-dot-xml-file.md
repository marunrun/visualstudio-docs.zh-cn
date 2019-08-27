---
title: 结构的 Content_types].xml 文件 |Microsoft Docs
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
ms.openlocfilehash: e94e8cd065908671446486d2ec00e167d8fb4f4e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697099"
---
# <a name="the-structure-of-the-contenttypesxml-file"></a>结构的 Content_types].xml 文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含有关的 VSIX 包中的内容类型的信息。 Visual Studio 使用 [Content_Types].xml 文件来安装包，但它不会安装文件本身。  
  
> [!NOTE]
> 本主题仅适用于 VSIX 包中使用的 [Content_Type].xml 文件，尽管 [Content_Types].xml 文件类型是组成部分*开放式打包约定 (OPC)* 标准。 有关详细信息，请参阅[OPC:新标准的打包数据](http://go.microsoft.com/fwlink/?LinkID=148207)MSDN 网站上。  
  
## <a name="attributes-and-elements"></a>特性和元素  
 以下部分介绍的根元素及其属性和子元素。  
  
### <a name="root-element"></a>根元素  
  
|元素|描述|  
|-------------|-----------------|  
|`Types`|包含枚举 VSIX 包中的文件类型的子元素。|  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`Xmlns`|（必选。）使用此 [Content_Types].xml 文件的架构的位置。|  
  
### <a name="attribute-name-attribute"></a>{属性名称}属性  
  
|                           值                           |                描述                |
|-----------------------------------------------------------|-------------------------------------------|
| http://schemas.openformats.org/package/2006/content-types | 内容类型架构的位置。 |
  
### <a name="child-elements"></a>子元素  
 `Types`元素可以包含任意数量的`Default`元素。  
  
|元素|描述|  
|-------------|-----------------|  
|`Default`|介绍了 VSIX 包中的内容类型。 在包中的每个文件类型必须具有其自己`Default`元素。|  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`Extension`|VSIX 包中的文件文件扩展名。|  
|`ContentType`|说明与文件扩展名相关联的内容类型。|  
  
### <a name="attribute-name-attribute"></a>{属性名称}属性  
 Visual Studio 能够识别以下`ContentType`关联的值`Extension`类型。  
  
|扩展名|ContentType|  
|---------------|-----------------|  
|txt|文本/无格式|  
|pkgdef|文本/无格式|  
|xml|text/xml|  
|vsixmanifest|text/xml|  
|htm 或 html|text/html|  
|rtf|application/rtf|  
|pdf|application/pdf|  
|gif|image/gif|  
|jpg 或 jpeg|image/jpg|  
|Tiff|图像/tiff|  
|vsix|应用程序/zip|  
|zip|应用程序/zip|  
|dll|application/octet-stream|  
|所有其他文件类型|application/octet-stream|  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的 [Content_Types].xml 文件描述了典型的 VSIX 包。  
  
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
 [VSIX 扩展架构 1.0 参考](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)   
 [OPC:数据打包了新标准](http://go.microsoft.com/fwlink/?LinkID=148207)
