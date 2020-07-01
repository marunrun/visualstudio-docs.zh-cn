---
title: 项目项元素（Visual Studio 项模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
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
ms.openlocfilehash: 885d0fbb50204f23a30fa43c1ffad45c9d67f829
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770718"
---
# <a name="projectitem-element-visual-studio-item-templates"></a>项目项元素（Visual Studio 项模板）
指定项模板中包含的文件。

> [!NOTE]
> `ProjectItem`元素根据模板是用于项目还是项来接受不同的属性。 本主题介绍 `ProjectItem` item 的元素。 有关 `ProjectItem` 项目模板元素的说明，请参阅项目项[元素（Visual Studio 项目模板）](../extensibility/projectitem-element-visual-studio-project-templates.md)。

 \<VSTemplate> \<TemplateContent>
 \<ProjectItem>

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

### <a name="attributes"></a>属性

| 特性 | 说明 |
|---------------------| - |
| `SubType` | 可选特性。<br /><br /> 指定多文件项模板中的项的子类型。 此值用于确定 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将用于打开项的编辑器。 |
| `CustomTool` | 可选特性。<br /><br /> 为项目文件中的项设置 CustomTool。 |
| `ItemType` | 可选特性。<br /><br /> 为项目文件中的项设置 ItemType。 |
| `ReplaceParameters` | 可选特性。<br /><br /> 一个布尔值，指定在从模板创建项目时，项是否具有必须替换的参数值。 默认值为 `false`。 |
| `TargetFileName` | 可选特性。<br /><br /> 指定从模板创建的项的名称。 此属性可用于使用参数替换创建项名称。 |

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|指定模板的内容。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 `string`，它表示模板 *.zip*文件中的文件的名称。

## <a name="remarks"></a>注解
 `ProjectItem`是的一个可选子级 `TemplateContent` 。

 `TargetFileName`特性可用于重命名具有参数的文件。 例如，如果文件*myfile.txt*位于模板 *.zip*文件的根目录中，但你希望根据用户在 "**添加新项**" 对话框中提供的文件名来命名该文件，则应使用以下 XML：

```xml
<ProjectItem TargetFileName="$fileinputname$.vb">MyFile.vb</ProjectItem>
```

 当从该模板创建项时，文件名称将基于用户在 "**添加新项**" 对话框中输入的名称。 这在创建多文件项模板时非常有用。 有关详细信息，请参阅[如何：创建多文件项模板](../ide/how-to-create-multi-file-item-templates.md)和[模板参数](../ide/template-parameters.md)。

## <a name="example"></a>示例
 下面的示例演示了类的标准项模板的元数据 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 。

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
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [如何：创建多文件项模板](../ide/how-to-create-multi-file-item-templates.md)
- [模板参数](../ide/template-parameters.md)
