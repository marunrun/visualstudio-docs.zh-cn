---
title: 本地化 VSIX 软件包 |微软文档
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- localize package
- localize extension
- localized deployment
ms.assetid: 10e80b13-b39e-466c-a7c8-774a862355af
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7d2d4222e45d56447951e86d558af9983a0d1cc9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702903"
---
# <a name="localizing-vsix-packages"></a>本地化 VSIX 包

您可以通过为每个目标语言创建*扩展.vsixlangpack*文件，然后将它们放在正确的文件夹中来本地化 VSIX 包。 安装本地化包时，扩展的本地化名称将与本地化说明一起显示。 如果提供本地化许可证文件或指向本地化信息的 URL，也会显示这些文件。

如果 VSIX 包的内容包含添加菜单命令或其他 UI 的 VSPackage，请参阅[本地化菜单命令](../extensibility/localizing-menu-commands.md)，了解有关本地化新 UI 元素的信息。

## <a name="directory-structure"></a>目录结构

 当用户安装扩展时，**扩展和更新**会检查其名称与目标计算机的 Visual Studio 区域设置匹配的文件夹的 VSIX 包的顶层。 如果**扩展和更新**在文件夹中找到 *.vsixlangpack*文件，它将该文件中的本地化值替换为 *.vsixmanifest*文件中的相应值。 安装扩展时将显示这些值。 下面的示例显示了本地化为西班牙语 （es-ES） 和法语 （fr-FR） 的 VSIX 包的目录结构。

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
> 中支持 VSIX 的项目模板[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]生成 VSIX 清单并将其命名为*source.扩展.vsixmanifest*。 当 Visual Studio 生成项目时，它会将该文件的内容复制到 VSIX 包中的扩展.VsixManifest 中。

## <a name="the-extensionvsixlangpack-file"></a>扩展.vsixlangpack 文件

*扩展.vsixlangpack*文件遵循[VSIX 语言包架构 2.0](../extensibility/vsix-language-pack-schema-2-0-reference.md)。 此架构具有`PackageLanguagePackManifest`， 它紧接子`Metadata`元素。 元数据元素最多可以包含 6 个子元素`DisplayName`、、、、、、、、、、、、`Description``MoreInfo``License``ReleaseNotes`和`Icon`。 这些子`DisplayName`元素`Description`对应于`MoreInfo``License``ReleaseNotes`*扩展.vsixmanifest*文件元素`Icon`的`Metadata`子元素。

创建 vsixlangpack 文件时，必须将`Include in Vsix`属性设置为`true`。 否则，将忽略本地化的安装文本。

### <a name="to-set-the-include-in-vsix-property"></a>在 Vsix 属性中设置"包括"

1. 在**解决方案资源管理器**中，右键单击扩展.vsixlangpack 文件，然后单击**属性**。

2. 在**属性网格**中，单击**Vsix 中的"包括**"，并将其`true`值设置为 。

## <a name="example"></a>示例

### <a name="description"></a>描述

下面的示例显示*扩展.vsixmanifest*文件的相关部分。 该文件还包括西班牙语的相应*扩展.vsixlangpack*文件。 如果目标计算机的 Visual Studio 区域设置设置为西班牙语，则语言包中的值将替换清单中的值。

### <a name="code"></a>代码

- [*扩展.vsixmanifest]*

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

- [*扩展.vsixlangpack*]

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
|[VSIX 语言包架构 2.0 参考](vsix-language-pack-schema-2-0-reference.md)|VSIX 语言包描述 .v6 部署文件的本地化信息。|
|[VSIX 软件包的剖析](../extensibility/anatomy-of-a-vsix-package.md)|描述 vsix 包的结构和内容。|
|[本地化菜单命令](../extensibility/localizing-menu-commands.md)|演示如何本地化扩展中的其他文本资源。|
