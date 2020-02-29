---
title: VSIX 语言包架构2.0 引用 |Microsoft Docs
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- language pack
- localize vsix
- localize package
- localize extension
ms.assetid: 2a2932bc-cdbe-4d32-91fa-a3e0474f9098
ms.author: zorio
author: zoeyr
manager: jillfra
ms.openlocfilehash: f97fd5aee27cdc97cf6eb5731da9fad9cb999e18
ms.sourcegitcommit: 1efb6b219ade7c35068b79fbdc573a8771ac608d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78169334"
---
# <a name="vsix-language-pack-schema-20-reference"></a>VSIX 语言包架构2.0 引用

VSIX 语言包架构为 VSIX 包提供本地化的安装信息。 此架构的版本2.0 支持其他本地化元素。

## <a name="language-pack-schema"></a>语言包架构

语言包文件的根元素为 `<PackageLanguagePackManifest>`，属性为 `Version`，它是语言包格式的版本。 本文介绍语言包格式的版本2.0，该格式是通过将 `Version` 特性设置为值 `Version="2.0.0"`在清单中指定的。 根元素只包含一个子 `<Metadata>` 元素。

### <a name="packagelanguagepackmanifest-element"></a>PackageLanguagePackManifest 元素

在 `<PackageLanguagePackManifest>` 元素中，以下元素必须存在：

|标题|说明|
|-----------|-----------------|
|`<Metadata>`| 所有本地化包元数据的包含元素

### <a name="metadata-element"></a>Metadata 元素

在 `<Metadata>` 元素中，可以包含以下元素：

|标题|说明|
|-----------|-----------------|
|`<DisplayName>`|要安装的扩展的本地化名称|
|`<Description>`|要安装的扩展的本地化说明|
|`<License>`| 扩展的许可证的本地化版本的路径|
|`<MoreInfo>`| 指向有关扩展的本地化信息的链接|
|`<ReleaseNotes>`| 发行说明的本地化版本的路径或链接|
|`<Icon>`| 扩展图标的本地化版本的路径|

### <a name="sample-manifest"></a>示例清单

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageLanguagePackManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <DisplayName>Arbol de Familia</DisplayName>
    <Description> Esta extensión pone control personalizado en la caja de herramientas por manejar información de familia.</Description>
    <MoreInfo> http://www.contoso.com/products/es/ArbolDeFamilia.htm</MoreInfo>
    <License>Eula.rtf</License>
    <ReleaseNotes>ReleaseNotes.rtf</ReleaseNotes>
    <Icon>Icon.png</Icon>
  </Metadata>
</PackageLanguagePackManifest>
```

## <a name="see-also"></a>另请参阅

|标题|说明|
|-----------|-----------------|
|[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)|演示如何为 VSIX 包提供本地化的安装支持。|
|[VSIX 扩展架构2.0 引用](../extensibility/vsix-extension-schema-2-0-reference.md)|VSIX 清单描述了 *.vsix*部署文件的内容。 部署文件使你可以使用 "**扩展和更新**" 对话框安装 Visual Studio 扩展。|
|[查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)|演示如何使用 "**扩展和更新**" 对话框来安装、删除、激活和停用扩展。|
