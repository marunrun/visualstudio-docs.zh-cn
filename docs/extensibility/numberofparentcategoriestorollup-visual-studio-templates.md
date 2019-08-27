---
title: NumberOfParentCategoriesToRollUp 元素 （模板）
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#NumberOfParentCategoriesToRollUp
helpviewer_keywords:
- NumberOfParentCategoriesToRollUp element [Visual Studio Templates]
- <NumberOfParentCategoriesToRollUp> element [Visual Studio Templates]
ms.assetid: 6f9d36f5-ae23-4a92-8132-b11799e2c21a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65787aef175052eb69c6dedfff2e095f16c81ef1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66336330"
---
# <a name="numberofparentcategoriestorollup-element-visual-studio-templates"></a>NumberOfParentCategoriesToRollUp 元素 （Visual Studio 模板）
指定将显示在此模板的父类别数**新的项目**对话框。

 \<VSTemplate> \<TemplateData> \<NumberOfParentCategoriesToRollUp>

## <a name="syntax"></a>语法

```xml
<NumberOfParentCategoriesToRollUp>
1
</NumberOfParentCategoriesToRollUp>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 `integer`值是必需的。

 此值指定父类别将显示中的模板数**新的项目**对话框。

## <a name="remarks"></a>备注
 `NumberOfParentCategoriesToRollUp` 是可选元素。

## <a name="example"></a>示例
 此示例中演示的元数据[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]Windows 应用程序。 如果与此元数据模板位于两个文件夹级别下的顶级[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]节点，该模板将显示在顶级节点**新建项目**对话框。 如果`NumberOfParentCategoriesToRollUp`未设置，该模板仅的节点中显示它是物理位置。

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <NumberOfParentCategoriesToRollUp>2</NumberOfParentCategoriesToRollUp>
    </TemplateData>
    <TemplateContent>
        <Project File="MyStarterKit.csproj">
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
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
