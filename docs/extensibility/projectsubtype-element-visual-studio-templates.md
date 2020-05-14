---
title: 项目子类型元素（可视化工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectSubType
helpviewer_keywords:
- ProjectSubType element [Visual Studio Templates]
- <ProjectSubType> element [Visual Studio Templates]
ms.assetid: f6895cd4-3e95-4f0e-aa9e-8c7750f46ed4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 27396ad1bcc4e181b2b8cecd6ca863db2412630d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701835"
---
# <a name="projectsubtype-element-visual-studio-templates"></a>项目子类型元素（可视化工作室模板）
将模板分类为`ProjectType`元素中指定值的子类别。

 \<VStemplate>\<模板数据>\<项目子类型>

## <a name="syntax"></a>语法

```xml
<ProjectSubType> SubType </ProjectSubType>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 此值指定模板的子类别。

## <a name="remarks"></a>备注
 `ProjectSubType` 是 `TemplateData` 的可选子元素。

 该`ProjectSubType`元素为[ProjectType](../extensibility/projecttype-element-visual-studio-templates.md)元素提供子类别。 此值可以包括：

- `SmartDevice-NETCFv1`：指定模板以[!INCLUDE[Compact](../extensibility/includes/compact_md.md)]版本 1.0 为目标。

- `SmartDevice-NETCFv2`：指定模板以[!INCLUDE[Compact](../extensibility/includes/compact_md.md)]版本 2.0 为目标。

  如果模板包含`ProjectType`的值的元素`Web`，则`ProjectSubType`元素指定模板的编程语言。 此元素可以具有以下值：

- `CSharp`：指定模板创建[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]Web 项目或项。

- `VisualBasic`：指定模板创建[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]Web 项目或项。

## <a name="example"></a>示例
 下面的示例显示了面向版本 2.0[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]的设备应用程序的项目模板的[!INCLUDE[Compact](../extensibility/includes/compact_md.md)]元数据。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic device template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ProjectSubType>SmartDevice-NETCFv2</ProjectSubType>
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
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [项目类型元素（可视化工作室模板）](../extensibility/projecttype-element-visual-studio-templates.md)
