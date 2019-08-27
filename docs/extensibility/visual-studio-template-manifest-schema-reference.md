---
title: Visual Studio 模板清单架构参考 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: bc7d0a81-0df5-41a9-a912-1b30e5da1d13
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 52a421986e076d2badc6dc7eb76247d243da155b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323028"
---
# <a name="visual-studio-template-manifest-schema-reference"></a>Visual Studio 模板清单架构参考
此架构描述了 Visual Studio 模板清单的格式 ( *.vstman*) 生成的 Visual Studio 项目或项模板的文件。 位置和有关模板的其他相关信息，还介绍了架构。

 :由于没有单独的项目和项目模板目录，清单应该永远不会同时有的项和项目模板。

> [!IMPORTANT]
> 此清单是从 Visual Studio 2017 开始，提供。

## <a name="vstemplatemanifest-element"></a>VSTemplateManifest 元素
 清单的根元素。

### <a name="attributes"></a>特性

- **版本**：一个表示模板清单的版本字符串。 必需。

- **区域设置**:表示区域设置或区域设置的模板清单的字符串。 区域设置值适用于所有模板。 必须将每个区域使用单独的清单。 可选。

### <a name="child-elements"></a>子元素

- **VSTemplateContainer**可选。

- **VSTemplateDir**可选。

### <a name="parent-element"></a>父元素
 无。

## <a name="vstemplatecontainer"></a>VSTemplateContainer
 模板容器的清单元素。 清单都有针对它定义了每个模板的一个模板容器。

### <a name="attributes"></a>特性
 **VSTemplateType**:一个字符串值，指定模板类型 (`"Project"`， `"Item"`，或`"ProjectGroup"`)。 必需

### <a name="child-elements"></a>子元素

- **RelativePathOnDisk**:磁盘上的模板文件的相对路径。 此位置还定义模板的放置在模板树中所示**新的项目**或**新项**对话框。 有关模板部署为一个目录和单个文件，此路径是指包含模板文件的目录。 有关模板部署为 *.zip*文件，此路径应为路径 *.zip*文件。

- **VSTemplateHeader:一个[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)描述该标头的元素。

### <a name="parent-element"></a>父元素
 **VSTemplateManifest**

## <a name="vstemplatedir"></a>VSTemplateDir
 介绍模板所在的目录。 清单可以包含多个**VSTemplateDir**条目提供本地化的名称和排序顺序的目录，以控制它们在模板类别树中的外观。

 由于其设计**VSTemplateDir**条目应仅在非区域设置指定的清单中出现。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

- **RelativePath**:模板的路径。 可能每个路径，只有一个条目，因此第一个获胜的所有清单。

- **LocalizedName**:一个**NameDescriptionIcon**元素，它指定本地化的名称。 可选。

- **SortOrder**:一个字符串，指定排序顺序。 可选。

- **ParentFolderOverrideName**:重写的父文件夹的名称。 可选。 此元素具有**名称**特性，它是一个字符串值，指定的名称。

### <a name="parent-element"></a>父元素
 **VSTemplateManifest**

## <a name="namedescriptionicon"></a>NameDescriptionIcon
 指定的名称和描述，可能是已本地化的模板。 请参阅**LocalizedName**上面。

### <a name="attributes"></a>特性

- **包**:一个字符串值，该值指定的包。 可选。

- **ID**:一个字符串值，指定该 id。 可选。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-element"></a>父元素
 **LocalizedName**

## <a name="examples"></a>示例
 下面的代码是项目模板的示例 *.vstman*文件。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Project">
    <RelativePathOnDisk>CSharp\1033\TestProjectTemplate</RelativePathOnDisk>
    <TemplateFileName>TestProjectTemplate.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>TestProjectTemplate</Name>
        <Description>TestProjectTemplate</Description>
        <Icon>TestProjectTemplate.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <SortOrder>1000</SortOrder>
        <TemplateID>aac0aeea-7883-4003-992f-937d53d70ab1</TemplateID>
        <CreateNewFolder>true</CreateNewFolder>
        <DefaultName>TestProjectTemplate</DefaultName>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

 下面的代码是项模板的示例 *.vstman*文件。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Item">
    <RelativePathOnDisk>CSharp\1033\ItemTemplate1</RelativePathOnDisk>
    <TemplateFileName>ItemTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ItemTemplate1</Name>
        <Description>ItemTemplate1</Description>
        <Icon>ItemTemplate1.ico</Icon>
        <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
        <DefaultName>Class.cs</DefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```
