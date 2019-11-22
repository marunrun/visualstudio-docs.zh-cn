---
title: The Structure of the Content_types].xml File | Microsoft Docs
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
ms.openlocfilehash: 9b1fd98b3812fbeca2597534a7177ba2f81ab138
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301238"
---
# <a name="the-structure-of-the-content_typesxml-file"></a>[Content_types].xml 文件的结构
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Contains information about the kinds of content in a VSIX package. Visual Studio uses the [Content_Types].xml file to install the package, but it does not install the file itself.  
  
> [!NOTE]
> Although this topic applies only to [Content_Type].xml files that are used in VSIX packages, the [Content_Types].xml file type is part of the *Open Packaging Conventions (OPC)* standard. For more information, see [OPC: A New Standard For Packaging Your Data](https://go.microsoft.com/fwlink/?LinkID=148207) on the MSDN Web site.  
  
## <a name="attributes-and-elements"></a>特性和元素  
 The following sections describe the root element and its attributes and child elements.  
  
### <a name="root-element"></a>根元素  
  
|元素|描述|  
|-------------|-----------------|  
|`Types`|Contains child elements that enumerate the file types in the VSIX package.|  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`Xmlns`|(Required.) The location of the schema used for this [Content_Types].xml file.|  
  
### <a name="attribute-name-attribute"></a>{Attribute name} Attribute  
  
|                           “值”                           |                描述                |
|-----------------------------------------------------------|-------------------------------------------|
| http://schemas.openformats.org/package/2006/content-types | The location of the content types schema. |
  
### <a name="child-elements"></a>子元素  
 The `Types` element can contain any number of `Default` elements.  
  
|元素|描述|  
|-------------|-----------------|  
|`Default`|Describes a content type in the VSIX package. Every file type in the package must have its own `Default` element.|  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`Extension`|The file name extension of a file in the VSIX package.|  
|`ContentType`|Describes the kind of content that is associated with the file name extension.|  
  
### <a name="attribute-name-attribute"></a>{Attribute name} Attribute  
 Visual Studio recognizes the following `ContentType` values for the associated `Extension` types.  
  
|扩展名|ContentType|  
|---------------|-----------------|  
|txt|text/plain|  
|pkgdef|text/plain|  
|xml|text/xml|  
|vsixmanifest|text/xml|  
|htm or html|text/html|  
|rtf|application/rtf|  
|pdf|application/pdf|  
|gif|image/gif|  
|jpg or jpeg|image/jpg|  
|tiff|image/tiff|  
|vsix|application/zip|  
|zip|application/zip|  
|dll|application/octet-stream|  
|all other file types|application/octet-stream|  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 The following [Content_Types].xml file describes a typical VSIX package.  
  
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
 [Anatomy of a VSIX Package](../extensibility/anatomy-of-a-vsix-package.md)   
 [VSIX Extension Schema 1.0 Reference](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)   
 [OPC: A New Standard For Packaging Your Data](https://go.microsoft.com/fwlink/?LinkID=148207)
