---
title: 项目元素（可视化工作室项目模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectItem
helpviewer_keywords:
- <ProjectItem> element [Visual Studio item templates]
- ProjectItem element [Visual Studio item templates]
ms.assetid: 9ed94112-0c38-49df-b728-0dd2d0d1eb47
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6826440ed12e90f1ffced63dfef45bb3d86177ac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701866"
---
# <a name="projectitem-element-visual-studio-item-templates"></a>项目项目元素（可视化工作室项目模板）
指定项目模板中包含的文件。

> [!NOTE]
> 元素`ProjectItem`接受不同的属性，具体取决于模板是针对项目还是项。 本主题介绍项目`ProjectItem`的元素。 有关项目模板`ProjectItem`元素的说明，请参阅[ProjectItem 元素（可视化工作室项目模板）。](../extensibility/projectitem-element-visual-studio-project-templates.md)

 \<>项目项目\<>>\<的"模板">模板内容

## <a name="syntax"></a>语法

```
<ProjectItem
    SubType="Form/Component/CustomControl/UserControl"
    CustomTool="string"
    ItemType="string"
    ReplaceParameters="true/false"
    TargetFileName="TargetFileName.ext">
        FileName.ext
</ProjectItem>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

| 特性 | 描述 |
|---------------------| - |
| `SubType` | 可选特性。<br /><br /> 指定多文件项模板中项的子类型。 此值用于确定[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]将用于打开项的编辑器。 |
| `CustomTool` | 可选特性。<br /><br /> 为项目文件中的项设置自定义工具。 |
| `ItemType` | 可选特性。<br /><br /> 设置项目文件中项的物料类型。 |
| `ReplaceParameters` | 可选特性。<br /><br /> 布尔值，用于指定项是否具有从模板创建项目时必须替换的参数值。 默认值为 `false`。 |
| `TargetFileName` | 可选特性。<br /><br /> 指定从模板创建的项的名称。 此属性可用于使用参数替换创建项名称。 |

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[模板内容](../extensibility/templatecontent-element-visual-studio-templates.md)|指定模板的内容。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 表示`string`模板 *.zip*文件中文件名称的 。

## <a name="remarks"></a>备注
 `ProjectItem`是`TemplateContent`的可选子项。

 该`TargetFileName`属性可用于重命名具有参数的文件。 例如，如果文件*MyFile.vb*存在于模板 *.zip*文件的根目录中，但您希望根据用户在 **"添加新项目"** 对话框中提供的文件名命名该文件，则可以使用以下 XML：

```xml
<ProjectItem TargetFileName="$fileinputname$.vb">MyFile.vb</ProjectItem>
```

 使用此模板创建项目时，文件名将基于用户在"**添加新项目**"对话框中输入的名称。 这在创建多文件项模板时非常有用。 有关详细信息，请参阅[如何：创建多文件项模板](../ide/how-to-create-multi-file-item-templates.md)和[模板参数](../ide/template-parameters.md)。

## <a name="example"></a>示例
 下面的示例演示了[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]类的标准项模板的元数据。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <DefaultName>MyClass.cs</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem ReplaceParameters="true">MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [如何：创建多文件项模板](../ide/how-to-create-multi-file-item-templates.md)
- [模板参数](../ide/template-parameters.md)
