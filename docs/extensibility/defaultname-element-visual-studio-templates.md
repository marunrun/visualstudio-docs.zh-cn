---
title: DefaultName 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#DefaultName
helpviewer_keywords:
- DefaultName element [Visual Studio project templates]
ms.assetid: 0ff056c8-b9d2-4747-9308-92adf1811491
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1dbb720bf04c36b2d9f018be5418a25088e259f4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348153"
---
# <a name="defaultname-element-visual-studio-templates"></a>DefaultName 元素 （Visual Studio 模板）
在创建时指定 Visual Studio 项目系统将生成的项目或项目的名称。

 \<VSTemplate> \<TemplateData> \<DefaultName>

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 此文本指定项目或项的默认名称。

## <a name="remarks"></a>备注
 `DefaultName` 是可选元素。

 对于项目，此元素指定将项目存储在磁盘的目录的名称。 对于项，它指定源代码文件的文件名称。

 在创建项目或项时，你可以修改默认名称使用**名称**选项，这是从可用**新项目**对话框或**添加新项**对话框。

 如果不希望项目系统在生成项目或项的默认名称，然后设置[ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md)元素`False`。

## <a name="example"></a>示例
 下面的示例演示为标准项模板的元数据[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]类。

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