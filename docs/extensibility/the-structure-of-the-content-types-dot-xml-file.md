---
title: '[Content_types] .xml 文件的结构 |Microsoft Docs'
description: 了解内容类型文件的结构，该结构包含有关 VSIX 包中内容种类的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- content_types
- content types
- opc
- vsix
ms.assetid: 9c399598-b9fa-4da7-84b5-defbf82e9335
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7117845e4756f8b0e09a8fa603e66448e705b903
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715218"
---
# <a name="the-structure-of-the-content_typesxml-file"></a>[Content_types].xml 文件的结构
包含有关 VSIX 包中的内容种类的信息。 Visual Studio 使用 [Content_Types] .xml 文件来安装包，但不会安装文件本身。

> [!NOTE]
> 尽管本主题仅适用于 VSIX 包中使用的 [Content_Type] .xml 文件，但 [Content_Types] .xml 文件类型是 *开放打包约定 (OPC)* 标准的一部分。 有关详细信息，请参阅 MSDN 网站上的 [OPC：用于打包数据的新标准](/archive/msdn-magazine/2007/august/opc-a-new-standard-for-packaging-your-data) 。

## <a name="attributes-and-elements"></a>特性和元素
 以下各节描述了 root 元素及其属性和子元素。

### <a name="root-element"></a>Root 元素

|元素|说明|
|-------------|-----------------|
|`Types`|包含枚举 VSIX 包中的文件类型的子元素。|

### <a name="attributes"></a>属性

|属性|说明|
|---------------|-----------------|
|`Xmlns`| (必需。 ) 用于此 [Content_Types] .xml 文件的架构位置。|

### <a name="attribute-name-attribute"></a>{Attribute name}Attribute

| 值 | 说明 |
| - | - |
| `http://schemas.openformats.org/package/2006/content-types` | 内容类型架构的位置。 |

### <a name="child-elements"></a>子元素
 `Types` 元素可包含任意数量的 `Default` 元素。

|元素|说明|
|-------------|-----------------|
|`Default`|描述 VSIX 包中的内容类型。 包中的每个文件类型都必须有其自身的 `Default` 元素。|

### <a name="attributes"></a>属性

|属性|说明|
|---------------|-----------------|
|`Extension`|VSIX 包中文件的文件扩展名。|
|`ContentType`|描述与文件扩展名关联的内容类型。|

### <a name="attribute-name-attribute"></a>{Attribute name}Attribute
 Visual Studio 可识别 `ContentType` 相关类型的以下值 `Extension` 。

|分机|ContentType|
|---------------|-----------------|
|txt|text/plain|
|.pkgdef|text/plain|
|xml|text/xml|
|source.extension.vsixmanifest|text/xml|
|htm 或 html|text/html|
|rtf|应用程序/rtf|
|pdf|应用程序/pdf|
|GIF|image/gif|
|jpg 或 jpeg|image/jpg|
|tiff|image/tiff|
|vsix|应用程序/zip|
|zip|应用程序/zip|
|dll|application/octet-stream|
|所有其他文件类型|application/octet-stream|

## <a name="example"></a>示例

### <a name="description"></a>说明
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
- [VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)
- [VSIX 扩展架构1.0 引用](/previous-versions/dd393700(v=vs.110))
- [OPC：用于打包数据的新标准](/archive/msdn-magazine/2007/august/opc-a-new-standard-for-packaging-your-data)