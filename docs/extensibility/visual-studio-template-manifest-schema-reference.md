---
title: Visual Studio 模板清单架构参考 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: bc7d0a81-0df5-41a9-a912-1b30e5da1d13
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dbe46851d9df85569be796b4147217bd7db450ed
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80697986"
---
# <a name="visual-studio-template-manifest-schema-reference"></a>Visual Studio 模板清单架构参考
此架构描述为 Visual Studio 项目或项模板 *生成) 文件* (visual studio 模板清单的格式。 该架构还介绍了该模板的位置和其他相关信息。

 ：由于存在单独的项和项目模板目录，因此清单决不应混合使用项和项目模板。

> [!IMPORTANT]
> 此清单可从 Visual Studio 2017 开始使用。

## <a name="vstemplatemanifest-element"></a>VSTemplateManifest 元素
 清单的根元素。

### <a name="attributes"></a>属性

- **版本**：一个字符串，表示模板清单的版本。 必需。

- **Locale**：表示模板清单的区域设置或区域设置的字符串。 区域设置值适用于所有模板。 必须为每个区域设置使用单独的清单。 可选。

### <a name="child-elements"></a>子元素

- **VSTemplateContainer** 可有可无.

- **VSTemplateDir** 可有可无.

### <a name="parent-element"></a>父元素
 无。

## <a name="vstemplatecontainer"></a>VSTemplateContainer
 模板清单元素的容器。 清单为其定义的每个模板都有一个模板容器。

### <a name="attributes"></a>属性
 **VSTemplateType**：一个字符串值，指定模板 (`"Project"` 、或) 的类型 `"Item"` `"ProjectGroup"` 。 必需

### <a name="child-elements"></a>子元素

- **RelativePathOnDisk**：磁盘上模板文件的相对路径。 此位置还定义模板在 " **新建项目** " 或 " **新建项** " 对话框中显示的模板树中的位置。 对于部署为目录和单个文件的模板，此路径引用包含模板文件的目录。 对于部署为 *.zip* 文件的模板，此路径应为 *.zip* 文件的路径。

- * * VSTemplateHeader：描述标头的 [TemplateData](../extensibility/templatedata-element-visual-studio-templates.md) 元素。

### <a name="parent-element"></a>父元素
 **VSTemplateManifest**

## <a name="vstemplatedir"></a>VSTemplateDir
 描述模板所在的目录。 清单可以包含多个 **VSTemplateDir** 条目，以提供目录的本地化名称和排序顺序，以控制它们在模板类别树中的外观。

 由于其设计， **VSTemplateDir** 条目应仅出现在非区域设置指定的清单中。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

- **RelativePath**：模板的路径。 每个路径只能有一个条目，因此，第一个条目对于所有清单都入选。

- **LocalizedName**：指定本地化名称的 **NameDescriptionIcon** 元素。 可选。

- **SortOrder**：指定排序顺序的字符串。 可选。

- **ParentFolderOverrideName**：父文件夹的重写名称。 可选。 此元素具有 **name** 属性，该属性是一个指定名称的字符串值。

### <a name="parent-element"></a>父元素
 **VSTemplateManifest**

## <a name="namedescriptionicon"></a>NameDescriptionIcon
 指定可能用于本地化模板的名称和说明。 请参阅上面的 **LocalizedName** 。

### <a name="attributes"></a>属性

- **Package**：一个指定包的字符串值。 可选。

- **Id**：一个指定 ID 的字符串值。 可选。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-element"></a>父元素
 **LocalizedName**

## <a name="examples"></a>示例
 下面的代码是项目 *vstman* 文件的一个示例。

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

 下面的代码是项 *vstman* 文件的一个示例。

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
