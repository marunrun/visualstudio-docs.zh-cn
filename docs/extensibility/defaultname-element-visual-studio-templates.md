---
title: 默认名称元素（可视化工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#DefaultName
helpviewer_keywords:
- DefaultName element [Visual Studio project templates]
ms.assetid: 0ff056c8-b9d2-4747-9308-92adf1811491
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 92bd29824cf1d3b91a7bdaa7220479c583ad0f23
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712305"
---
# <a name="defaultname-element-visual-studio-templates"></a>默认名称元素（可视化工作室模板）
指定可视化工作室项目系统在创建项目或项目时将生成的名称。

 \<VStemplate>\<模板数据>\<默认名称>

## <a name="syntax"></a>语法

```
<DefaultName>
    Default Project Name
</DefaultName>
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

 此文本指定项目或项目的默认名称。

## <a name="remarks"></a>备注
 `DefaultName` 是可选元素。

 对于项目，此元素指定将项目存储在磁盘上的目录的名称。 对于项，它指定源文件的文件名。

 创建项目或项目时，可以使用"**名称"** 选项修改默认名称，该选项可从 **"新项目**"对话框或 **"添加新项目"** 对话框中提供。

 如果不希望项目系统为项目或项目生成默认名称，则将[ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md)元素设置为`False`。

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
