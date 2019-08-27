---
title: SupportsCodeSeparation 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsCodeSeparation
helpviewer_keywords:
- SupportsCodeSeparation element [Visual Studio Templates]
- <SupportsCodeSeparation> element [Visual Studio Templates]
ms.assetid: 8112aac8-a269-40e5-b92b-9b9a6ff5a542
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3a4a9e7ba92b9f48cf22999d53ecf6c7b7d832ab
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316951"
---
# <a name="supportscodeseparation-element-visual-studio-templates"></a>SupportsCodeSeparation 元素（Visual Studio 模板）
指定是否**将代码放在单独的文件**中启用复选框**添加新项**对话框。

 \<VSTemplate> \<TemplateData> \<SupportsCodeSeparation>

## <a name="syntax"></a>语法

```
<SupportsCodeSeparation> true/false </SupportsCodeSeparation>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义中的显示方式**新的项目**或**新项**对话框。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是`true`或`false`，以指示是否**将代码放在单独的文件**中启用复选框**添加新项**对话框。

## <a name="remarks"></a>备注
 `SupportsCodeSeparation` 是可选元素。 默认值为 `false`。

 `SupportsCodeSeparation`元素功能仅适用于 Web 项目模板。

 代码分离或代码隐藏页模型，可将标记保留在一个文件和另一个文件中的编程代码中。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 和其他.NET 语言使用此模型。

## <a name="example"></a>示例
 下面的示例指定要显示**将代码放在单独的文件**选项。

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
        <SupportsCodeSeparation>true</SupportsCodeSeparation>
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