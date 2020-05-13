---
title: 可视化工作室模板清单架构参考 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: bc7d0a81-0df5-41a9-a912-1b30e5da1d13
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dbe46851d9df85569be796b4147217bd7db450ed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697986"
---
# <a name="visual-studio-template-manifest-schema-reference"></a>可视化工作室模板清单架构参考
此架构描述为 Visual Studio 项目或项目模板生成的可视化工作室模板清单 *（.vstman*） 文件的格式。 架构还描述了该模板的位置和其他相关信息。

 ：因为有单独的项目和项目模板目录，因此清单不应混合使用物料和项目模板。

> [!IMPORTANT]
> 此清单可从 Visual Studio 2017 开始使用。

## <a name="vstemplatemanifest-element"></a>VSTemplate清单元素
 清单的根元素。

### <a name="attributes"></a>特性

- **版本**：表示模板清单版本的字符串。 必需。

- **区域设置**：表示模板清单区域设置或区域设置的字符串。 区域设置值适用于所有模板。 您必须为每个区域设置使用单独的清单。 可选。

### <a name="child-elements"></a>子元素

- **VSTemplate 容器**选。

- **VSTemplateDir**选。

### <a name="parent-element"></a>父元素
 无。

## <a name="vstemplatecontainer"></a>VSTemplate 容器
 模板清单元素的容器。 清单为其定义的每个模板有一个模板容器。

### <a name="attributes"></a>特性
 **VSTemplate 类型**：指定模板类型 （`"Project"`或`"Item"``"ProjectGroup"`的字符串值）。 必选

### <a name="child-elements"></a>子元素

- **相对路径磁盘**：磁盘上模板文件的相对路径。 此位置还定义模板在"**新项目**"或"**新项目**"对话框中显示的模板树中的位置。 对于作为目录和单个文件部署的模板，此路径引用包含模板文件的目录。 对于作为 *.zip*文件部署的模板，此路径应该是 *.zip*文件的路径。

- *VSTemplate 标题：描述标头的[模板数据](../extensibility/templatedata-element-visual-studio-templates.md)元素。

### <a name="parent-element"></a>父元素
 **VSTemplate清单**

## <a name="vstemplatedir"></a>VSTemplateDir
 描述模板所在的目录。 清单可以包含多个**VSTemplateDir**条目，以提供本地化的名称和排序，以便目录控制其在模板类别树中的外观。

 由于其设计 **，VSTemplateDir**条目应只出现在非区域设置指定的清单中。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

- **相对路径**：模板的路径。 每个路径只能有一个条目，因此第一个条目将赢得所有清单。

- **本地化名称**：指定本地化名称**的名称描述元素**。 可选。

- **排序顺序**：指定排序顺序的字符串。 可选。

- **父文件夹覆盖名称**：父文件夹的重写名称。 可选。 此元素具有**Name**属性，该属性是指定名称的字符串值。

### <a name="parent-element"></a>父元素
 **VSTemplate清单**

## <a name="namedescriptionicon"></a>名称描述图标
 指定名称和说明，可能用于本地化模板。 请参阅上面**的本地化名称**。

### <a name="attributes"></a>特性

- **包**：指定包的字符串值。 可选。

- **ID**：指定 ID 的字符串值。 可选。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-element"></a>父元素
 **本地化名称**

## <a name="examples"></a>示例
 以下代码是项目模板 *.vstman*文件的示例。

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

 以下代码是项模板 *.vstman*文件的示例。

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
