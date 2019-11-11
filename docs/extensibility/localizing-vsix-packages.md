---
title: 本地化 VSIX 包 |Microsoft Docs
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- localize package
- localize extension
- localized deployment
ms.assetid: 10e80b13-b39e-466c-a7c8-774a862355af
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 171c8635c2d6db2c346fb836701e630812ecbb28
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186451"
---
# <a name="localizing-vsix-packages"></a>本地化 VSIX 包

可以通过为每个目标语言创建*vsixlangpack*文件，然后将其放在正确的文件夹中，来本地化 VSIX 包。 当安装本地化的包时，将显示该扩展的本地化名称以及本地化说明。 如果提供本地化的许可证文件或指向本地化信息的 URL，则它们也会显示。

如果内容你的 VSIX 包包含添加菜单命令或其他 UI 的 VSPackage，请参阅[本地化菜单命令](../extensibility/localizing-menu-commands.md)以获取有关本地化新 UI 元素的信息。

## <a name="directory-structure"></a>目录结构

 当用户安装扩展时，**扩展和更新**将检查其名称与目标计算机的 Visual Studio 区域设置匹配的文件夹的 VSIX 包顶级。 如果**扩展和更新**在文件夹中找到*vsixlangpack*文件，则会将该文件中的本地化值替换为*source.extension.vsixmanifest*文件中的相应值。 安装扩展时，将显示这些值。 下面的示例演示了本地化为西班牙语（es）和法语（fr-fr）的 VSIX 包的目录结构。

```text
.
├── MyExtension.dll
├── Extension.vsixmanifest
├── [Content_Types].xml
├── es-ES
│   └── Extension.vsixlangpack
└── fr-FR
    └── Extension.vsixlangpack
```

> [!NOTE]
> [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] 中支持 VSIX 的项目模板生成 VSIX 清单并将其命名为*source.extension.vsixmanifest*。 当 Visual Studio 生成项目时，它会将该文件的内容复制到 VSIX 包的 Source.extension.vsixmanifest 中。

## <a name="the-extensionvsixlangpack-file"></a>Vsixlangpack 文件

*Vsixlangpack*文件遵循[VSIX 语言包架构 2.0](../extensibility/vsix-language-pack-schema-2-0-reference.md)。 此架构具有一个 `PackageLanguagePackManifest`，其后紧跟 `Metadata` 子元素。 Metadata 元素最多可以包含6个子元素： `DisplayName`、`Description`、`MoreInfo`、`License`、`ReleaseNotes`和 `Icon`。 这些子元素对应于*source.extension.vsixmanifest*文件的 `ReleaseNotes`元素的 `DisplayName`、`Description`、`MoreInfo`、`License`、`Icon` 和 `Metadata` 子元素。

创建 vsixlangpack 文件时，必须将 `Include in Vsix` 属性设置为 `true`。 否则，将忽略本地化安装文本。

### <a name="to-set-the-include-in-vsix-property"></a>设置 Include in Vsix 属性

1. 在**解决方案资源管理器**中，右键单击 vsixlangpack 文件，然后单击 "**属性**"。

2. 在 "**属性" 网格**中，单击 "**包括在 Vsix 中**"，并将其值设置为 `true`。

## <a name="example"></a>示例

### <a name="description"></a>描述

下面的示例显示*source.extension.vsixmanifest*文件的相关部分。 该文件还包含适用于西班牙语的*vsixlangpack*文件。 如果目标计算机的 Visual Studio 区域设置为西班牙语，则语言包中的值将替换清单中的值。

### <a name="code"></a>代码

- [*Source.extension.vsixmanifest*]

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageManifest ...>
  <Metadata ...>
    <DisplayName>Family Tree</DisplayName>
    <Description>This extension places a custom treeview control in the toolbox that is optimized for handling family tree information.</Description>
    <MoreInfo>http://www.contoso.com/products/FamilyTree.htm</MoreInfo>
    <License>Eula.rtf</License>
    <ReleaseNotes>ReleaseNotes.rtf</ReleaseNotes>
    <Icon>Icon.png</Icon>
  </Metadata>
  <Installation .../>
  <Dependencies .../>
  <Prerequisites .../>
  <Assets .../>
</PackageManifest>
```

- [*Vsixlangpack*]

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

## <a name="see-also"></a>请参阅

|Title|描述|
|-----------|-----------------|
|[VSIX 语言包架构2.0 引用](vsix-language-pack-schema-2-0-reference.md)|VSIX 语言包描述 .vsix 部署文件的本地化信息。|
|[VSIX 包的解析](../extensibility/anatomy-of-a-vsix-package.md)|描述 vsix 包的结构和内容。|
|["本地化" 菜单命令](../extensibility/localizing-menu-commands.md)|演示如何本地化扩展中的其他文本资源。|