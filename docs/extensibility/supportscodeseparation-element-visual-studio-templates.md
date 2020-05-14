---
title: 支持代码分离元素（可视化工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsCodeSeparation
helpviewer_keywords:
- SupportsCodeSeparation element [Visual Studio Templates]
- <SupportsCodeSeparation> element [Visual Studio Templates]
ms.assetid: 8112aac8-a269-40e5-b92b-9b9a6ff5a542
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bd52ae47f47f3ca1fce23f7cf8d37260ec86fb0c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699500"
---
# <a name="supportscodeseparation-element-visual-studio-templates"></a>SupportsCodeSeparation 元素（Visual Studio 模板）
在 **"添加新项目**"对话框中指定是否启用**了单独文件中的放置代码**复选框。

 \<模板>\<模板数据>\<支持代码分离>

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需元素。<br /><br /> 对模板进行分类，并定义模板在 **"新项目**"或"**新项目**"对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须为 或`true``false`，指示在 **"添加新项目**"对话框中是否启用**了单独文件复选框中的放置代码**。

## <a name="remarks"></a>备注
 `SupportsCodeSeparation` 是可选元素。 默认值为 `false`。

 该`SupportsCodeSeparation`元素仅适用于 Web 项模板。

 代码分离或代码背后的页面模型允许您将标记保存在一个文件中，而编程代码保存在另一个文件中。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]和其他 .NET 语言使用此模型。

## <a name="example"></a>示例
 下面的示例指定在**单独的文件选项中**显示 Place 代码。

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
- [创建项目和项目模板](../ide/creating-project-and-item-templates.md)
