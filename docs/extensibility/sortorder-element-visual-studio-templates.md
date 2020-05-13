---
title: 排序元素（可视化工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SortOrder
helpviewer_keywords:
- SortOrder element [Visual Studio Templates]
- <SortOrder> element [Visual Studio Templates]
ms.assetid: 151932c1-f08a-4f78-a8d0-bd2f32211a9c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 935d00335a21d3e129e79ce351e554ea93787447
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699954"
---
# <a name="sortorder-element-visual-studio-templates"></a>SortOrder 元素（Visual Studio 模板）
指定用于排列模板的相同类别中的其他模板的值，因为它显示在 **"新项目**"或 **"添加新项目"** 对话框中。

 \<VStemplate \<>模板数据\<>排序顺序>

## <a name="syntax"></a>语法

```
<SortOrder> ... </SortOrder>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 表示`integer`排序订单值的 。

## <a name="remarks"></a>备注
 `SortOrder` 是可选元素。 默认值为 100，所有值必须为 10 倍。

 对于`SortOrder`用户创建的模板，将忽略该元素。 所有用户创建的模板都按字母顺序排序。

 具有低排序订单值的模板显示在具有高排序订单值的模板之前的"**新项目**"或 **"新建项目"** 对话框中。

## <a name="example"></a>示例
 下面的示例说明了标准[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]类模板的元数据。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class template.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <SortOrder>290</SortOrder>
        <DefaultName>MyClass</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

 在此示例中，`SortOrder`元素相对较高。 其他[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]项模板`SortOrder`的值可能低于`290`，并且将显示在"**新建项目"** 对话框中此模板之前。

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项目模板](../ide/creating-project-and-item-templates.md)
