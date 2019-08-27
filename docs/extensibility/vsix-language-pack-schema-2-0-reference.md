---
title: VSIX 语言包架构 2.0 参考 |Microsoft Docs
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- language pack
- localize vsix
- localize package
- localize extension
ms.assetid: 2a2932bc-cdbe-4d32-91fa-a3e0474f9098
ms.author: dagriffe
author: dgriffen
manager: jillfra
ms.workload:
- dagriffe
ms.openlocfilehash: acea36031b98693e1d618986720d9932f76a0a63
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62953096"
---
# <a name="vsix-language-pack-schema-20-reference"></a>VSIX 语言包架构 2.0 参考

VSIX 语言包架构提供了 VSIX 包的本地化的安装信息。 此架构的 2.0 版支持额外的本地化元素。

## <a name="language-pack-schema"></a>语言包架构

语言包文件的根元素是`<PackageLanguagePackManifest>`，使用以下属性`Version`，这是语言包格式的版本。 本指南介绍了 2.0 版的语言包格式，通过设置指定在清单中`Version`属性的值设`Version="2.0.0"`。 根元素包含一个子`<Metadata>`元素。

### <a name="packagelanguagepackmanifest-element"></a>PackageLanguagePackManifest 元素

在`<PackageLanguagePackManifest>`元素必须存在以下元素：

|标题|描述|
|-----------|-----------------|
|`<Metadata>`| 包含所有本地化的包元数据元素

### <a name="metadata-element"></a>元数据元素

在`<Metadata>`元素可以具有以下元素：

|标题|描述|
|-----------|-----------------|
|`<DisplayName>`|要安装的扩展插件的本地化的名称|
|`<Description>`|要安装的扩展插件的本地化的说明|
|`<License>`| 路径扩展的许可证的本地化版本|
|`<MoreInfo>`| 有关扩展的本地化信息的链接|
|`<ReleaseNotes>`| 路径或链接到本地化版本的发行说明|
|`<Icon>`| 到本地化版本的扩展图标路径|

### <a name="sample-manifest"></a>示例清单

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageLanguagePackManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <DisplayName>Arbol de Familia</LocalizedName>
    <Description> Esta extensión pone control personalizado en la caja de herramientas por manejar información de familia.</Description>
    <MoreInfo> http://www.contoso.com/products/es/ArbolDeFamilia.htm</MoreInfo>
    <License>Eula.rtf</License>
    <ReleaseNotes>ReleaseNotes.rtf</ReleaseNotes>
    <Icon>Icon.png</Icon>
  </Metadata>
</PackageLanguagePackManifest>
```

## <a name="see-also"></a>请参阅

|标题|描述|
|-----------|-----------------|
|[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)|演示如何提供本地化的安装支持 VSIX 包。|
|[VSIX 扩展架构 2.0 参考](../extensibility/vsix-extension-schema-2-0-reference.md)|VSIX 清单描述的内容 *.vsix*部署文件。 部署文件，您可以通过安装 Visual Studio 扩展**扩展和更新**对话框。|
|[查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)|演示如何使用**扩展和更新**对话框中，若要安装、 删除、 激活和停用扩展。|