---
title: 提供默认名称元素（视觉工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProvideDefaultName
helpviewer_keywords:
- ProvideDefaultName element [Visual Studio project templates]
ms.assetid: 7b0e7b20-fd6b-42e2-81d0-e5100cea0528
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 192716198f605a5f6b4f62730e84dcf83b4229cc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701719"
---
# <a name="providedefaultname-element-visual-studio-templates"></a>提供默认名称元素（可视化工作室模板）
指定[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]项目系统是否会在"**添加新项目**"或"**新项目**"对话框中为模板生成默认名称。

 \<>提供默认\<名称>>\<的 VStemplate>模板数据

## <a name="syntax"></a>语法

```xml
<ProvideDefaultName> true/false </ProvideDefaultName>
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

 文本必须为 或`true``false`，指示是否在 **"添加新项目**"或 **"新项目**"对话框中为模板生成默认名称。

## <a name="remarks"></a>备注
 `ProvideDefaultName` 是可选元素。 默认值为 `true`。

 如果`ProvideDefaultName``false`元素为 ，**则"添加新项**"和 **"新项目"** 对话框`<Enter_name>`**的名称**框包含值 。

 使用[默认名称](../extensibility/defaultname-element-visual-studio-templates.md)元素在 **"添加新项目和****新项目**"对话框中指定项目或项目的默认名称。 当`ProvideDefaultName`元素的值为`true`时，项目`DefaultName`元素的省略会用模板的名称填充对话框，即[名称](../extensibility/name-element-visual-studio-templates.md)元素中的值。

## <a name="example"></a>示例
 以下代码示例将`ProvideDefaultName`元素设置到`false`。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ProvideDefaultName>false</ProvideDefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
