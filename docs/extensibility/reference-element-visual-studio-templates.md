---
title: 参考元素（视觉工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Reference
helpviewer_keywords:
- Reference element [Visual Studio templates]
- <Reference> element [Visual Studio templates]
ms.assetid: 852772ea-c324-42e9-8c8a-6d565414a109
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 11d893f6268a69172d27a0f7caee707767abfe89
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701626"
---
# <a name="reference-element-visual-studio-templates"></a>参考元素（可视化工作室模板）
指定向项目添加项时要添加的程序集引用。

 \<VStemplate \<>模板内容\<>参考\<>参考>

## <a name="syntax"></a>语法

```xml
<Reference>
    <Assembly> ... </Assembly>
</Reference>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[装配](../extensibility/assembly-element-visual-studio-templates.md)|必需元素。<br /><br /> 指定有关程序集的信息，模板用于将该程序集的引用添加到项目。 每个`Reference`元素中必须有`Assembly`一个元素。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[参考](../extensibility/references-element-visual-studio-templates.md)|对模板添加到项目中的程序集引用进行分组。|

## <a name="remarks"></a>备注
 `Reference` 是 `References` 的必需子元素。

 `Reference`和`References`元素只能在 具有`Type`属性值 的`Item` *.vstemplate*文件中使用。

## <a name="example"></a>示例
 下面的示例说明了项模板`TemplateContent`的元素。 此 XML 添加对*System.dll*和*System.Data.dll*程序集的引用。

```xml
<TemplateContent>
    <References>
        <Reference>
            <Assembly>
                System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
            </Assembly>
        </Reference>
        <Reference>
            <Assembly>
                System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
            </Assembly>
        </Reference>
    </References>
    ...
</TemplateContent>
```

## <a name="see-also"></a>请参阅
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
