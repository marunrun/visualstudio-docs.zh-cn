---
title: SupportsLanguageDropDown 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsLanguageDropDown
helpviewer_keywords:
- SupportsLanguageDropDown element [Visual Studio Templates]
- <SupportsLanguageDropDown> element [Visual Studio Templates]
ms.assetid: 641197d5-f724-4c06-bc47-2e22dad3fbfb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b6dbc2c5cae40078f033fa0fb85c6fda032e8ec4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316804"
---
# <a name="supportslanguagedropdown-element-visual-studio-templates"></a>SupportsLanguageDropDown 元素（Visual Studio 模板）
指定 Web 项目模板是完全相同的多个语言，以及是否**语言**上启用选项**添加新项**对话框。

 \<VSTemplate > \<TemplateData > \<SupportsLanguageDropDown >

## <a name="syntax"></a>语法

```
<SupportsLanguageDropDown> true/false </SupportsLanguageDropDown>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是`true`或`false`，以指示是否**语言**选项才可用**添加新项**对话框。

## <a name="remarks"></a>备注
 `SupportsLanguageDropDown` 是可选元素。 默认值为 `false`。

 `SupportsLanguageDropDown`元素功能仅适用于 Web 项目模板。

 如果此元素的值设置为`true`，则项模板是完全相同的所有编程语言和**语言**中启用选项**添加新项**对话框。 此选项，可选择你想要从模板创建的新项的编程语言。

## <a name="example"></a>示例
 下面的示例指定要显示**语言**下拉列表选项。

```
<VSTemplate Version="3.0.0" Type="Project"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">>
    <TemplateData>
        <Name>MyWebProjecStarterKit</Name>
        <Description>A simple Web template</Description>
        <Icon>icon.ico</Icon>
        <ProjectType>Web</ProjectType>
        <ProjectSubType>CSharp</ProjectSubType>
        <DefaultName>WebSite</DefaultName>
        <SupportsLanguageDropDown>true</SupportsLanguageDropDown>
    </TemplateData>
    <TemplateContent>
        <Project File="WebApplication.webproj">
            <ProjectItem>icon.ico</ProjectItem>
            <ProjectItem OpenInEditor="true">Default.aspx</ProjectItem>
            <ProjectItem>Default.aspx.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)