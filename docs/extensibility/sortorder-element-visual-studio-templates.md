---
title: SortOrder 元素（Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SortOrder
helpviewer_keywords:
- SortOrder element [Visual Studio Templates]
- <SortOrder> element [Visual Studio Templates]
ms.assetid: 151932c1-f08a-4f78-a8d0-bd2f32211a9c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2875bcb4583c1d2ec47a935d1a8bb4f0de109a92
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72719916"
---
# <a name="sortorder-element-visual-studio-templates"></a>SortOrder 元素（Visual Studio 模板）
指定一个值，该值用于在同一类别中的其他模板之间进行排列，如在 "**新建项目**" 或 "**添加新项**" 对话框中显示的模板。

 \<VSTemplate > \<TemplateData > \<SortOrder >

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 表示排序顺序值的 `integer`。

## <a name="remarks"></a>备注
 `SortOrder` 是可选元素。 默认值为100，所有值都必须是10的倍数。

 对于用户创建的模板，将忽略 `SortOrder` 元素。 所有用户创建的模板都按字母顺序排序。

 具有低排序顺序值的模板会出现在 "**新建项目**" 或 "**新建添加项**" 对话框中，然后才会出现具有高排序顺序值的模板。

## <a name="example"></a>示例
 下面的示例演示标准 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 类模板的元数据。

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

 在此示例中，`SortOrder` 元素相对较高。 其他 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 项模板可能具有低于 `290` 的 `SortOrder` 值，并且将在 "**新建项**" 对话框中显示在此模板之前。

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)