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
ms.openlocfilehash: 3e0ef2cc0c2404a2148f471d12f313b158f3bd64
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344563"
---
# <a name="localizing-vsix-packages"></a>本地化 VSIX 包

可以通过创建本地化 VSIX 包*Extension.vsixlangpack*文件为每种目标语言，然后将它们放在正确的文件夹。 安装本地化的包时，扩展插件的本地化的名称显示以及的本地化说明。 如果你提供本地化的许可证文件或指向的本地化信息的 URL，则它们也会显示。

如果内容 VSIX 包中包含 VSPackage 添加的菜单命令或其他 UI，请参阅[本地化菜单命令](../extensibility/localizing-menu-commands.md)有关本地化的新 UI 元素的信息。

## <a name="directory-structure"></a>目录结构

 当用户安装扩展**扩展和更新**检查其名称与目标计算机的 Visual Studio 区域设置相匹配的文件夹的 VSIX 包的最高级别。 如果**扩展和更新**查找 *.vsixlangpack*文件在文件夹中，都将替换该文件中的相应值中的本地化的值 *.vsixmanifest*文件。 在安装该扩展时，会显示这些值。 下面的示例显示了已本地化为西班牙语 (ES-ES) 和法语 (FR-FR) 的 VSIX 包的目录结构。

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
> 中的 VSIX 支持的项目模板[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]生成的 VSIX 清单并将其命名*source.extension.vsixmanifest*。 当 Visual Studio 生成项目时，它将复制该文件的内容到 Extension.VsixManifest VSIX 包中。

## <a name="the-extensionvsixlangpack-file"></a>Extension.vsixlangpack 文件

*Extension.vsixlangpack*文件如下所示[VSIX 语言包架构 2.0](../extensibility/vsix-language-pack-schema-2-0-reference.md)。 此架构具有`PackageLanguagePackManifest`，其中后紧跟着`Metadata`子元素。 元数据元素可以包含最多 6 个子元素， `DisplayName`， `Description`， `MoreInfo`， `License`， `ReleaseNotes`，并`Icon`。 这些子元素对应于`DisplayName`， `Description`， `MoreInfo`， `License`， `ReleaseNotes`，并且`Icon`的子元素`Metadata`元素*Extension.vsixmanifest*文件。

在创建 vsixlangpack 文件时，必须设置`Include in Vsix`属性设置为`true`。 否则，将忽略的本地化的安装文本。

### <a name="to-set-the-include-in-vsix-property"></a>若要设置包括在 Vsix 属性

1. 在中**解决方案资源管理器**，右键单击 Extension.vsixlangpack 文件，然后单击**属性**。

2. 在中**属性网格**，单击**包含在 Vsix**，并将其值设置为`true`。

## <a name="example"></a>示例

### <a name="description"></a>描述

下面的示例演示的相关部分*Extension.vsixmanifest*文件。 该文件还包括相应*Extension.vsixlangpack*西班牙语的文件。 如果目标计算机的 Visual Studio 区域设置设置为西班牙语，语言包中的值替换在清单中的值。

### <a name="code"></a>代码

- [*Extension.vsixmanifest*]

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

- [*Extension.vsixlangpack*]

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

|标题|描述|
|-----------|-----------------|
|[VSIX 语言包架构 2.0 参考](/visualstudio/extensibility/vsix-language-pack-schema-2-0-reference)|VSIX 语言包描述一个.vsix 部署文件的本地化信息。|
|[VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)|描述的结构和 vsix 包的内容。|
|[本地化菜单命令](../extensibility/localizing-menu-commands.md)|演示如何将扩展在其他文本资源本地化。|