---
title: 项目类型元素（视觉工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectType
helpviewer_keywords:
- ProjectType element [Visual Studio project templates]
ms.assetid: ccf9d83f-c7f3-49c7-a31f-e1f22bec004c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d794bd5e81e77a892b5a3be38ff73ab805582dd7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701809"
---
# <a name="projecttype-element-visual-studio-templates"></a>项目类型元素（可视化工作室模板）
对项目模板进行分类，使其显示在 **"新项目**"或 **"添加新项目"** 对话框中的指定组下。

> [!WARNING]
> 支持在 Visual Studio 2012 中启动C++模板。 在 Visual Studio 2010 和早期版本中，C++不支持它们。

 \<模板>\<模板数据>\<项目类型>

## <a name="syntax"></a>语法

```xml
<ProjectType> CSharp/VisualBasic/VC/Web </ProjectType>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 此值指定模板将创建的项目类型，并且必须包含以下值之一：

- `CSharp`指定模板创建[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]项目或项。

- `VisualBasic`指定模板创建[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]项目或项。

- `Web`：指定模板创建 Web 项目或项。 如果`ProjectType`元素包含此值，则项目或项的语言将定义在[ProjectSubType 元素（可视化工作室模板）中](../extensibility/projectsubtype-element-visual-studio-templates.md)。

## <a name="remarks"></a>备注
 `ProjectType` 是 `TemplateData` 的必需子元素。

 `ProjectType`元素的值指定模板在 **"新项目**"或 **"添加新项目**"对话框中的位置。 例如，在 **"新项目**"对话框`ProjectType`中的`CSharp`**"可视化 C#"** 节点下，将显示值为 的模板。

 可以使用[Project SubType](../extensibility/projectsubtype-element-visual-studio-templates.md)元素指定模板子类型。

## <a name="example"></a>示例
 下面的示例显示了[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]应用程序的项目模板的元数据。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
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
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [项目子类型元素（可视化工作室模板）](../extensibility/projectsubtype-element-visual-studio-templates.md)
