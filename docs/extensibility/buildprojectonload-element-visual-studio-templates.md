---
title: BuildProjectOnload 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: b07d3074-0fc9-45e1-baf5-da6bd4f3f1c0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c9a9d4536c9ae7205a98ef0c79906ccbb002b5f7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66321245"
---
# <a name="buildprojectonload-element-visual-studio-templates"></a>BuildProjectOnload 元素 （Visual Studio 模板）
生成新的项目如下创建并将其添加到解决方案。 不生成整个解决方案。

元素层次结构：

```xml
<VSTemplate>
  <TemplateData>
    <BuildProjectOnLoad>
```

## <a name="syntax"></a>语法

```vb
<BuildProjectOnLoad> true/false </BuildProjectOnLoad>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|`TemplateData`|将此模板分类并定义显示在这种方式**新的项目**并**添加新项**对话框。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是`true`或`false`以指示是否从模板创建时生成新的项目。

## <a name="remarks"></a>备注
 `BuildProjectOnLoad` 是可选元素。 默认值为 `false`。

## <a name="example"></a>示例
 下面的示例说明了 Visual C# 模板的元数据。

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <BuildProjectOnload>true</BuildProjectOnLoad>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅

- [BuildOnLoad 属性和元素](buildonload-visual-studio-templates.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)