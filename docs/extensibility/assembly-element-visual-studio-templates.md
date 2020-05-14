---
title: 装配元件（可视化工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Assembly
helpviewer_keywords:
- Assembly element [Visual Studio templates]
- <Assembly> element [Visual Studio templates]
ms.assetid: 9242f76a-1273-4b8a-8f26-6606f91829ef
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c80044657b16448ba4567fff839274226985fa14
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740044"
---
# <a name="assembly-element-visual-studio-templates"></a>装配元件（可视化工作室模板）
指定有关程序集的信息，模板用于将该程序集的引用添加到项目。

 \<模板>\<模板内容>\<参考>\<参考>\<程序集>

## <a name="syntax"></a>语法

```
<Assembly> AssemblyName </Assembly>
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
|[参考](../extensibility/reference-element-visual-studio-templates.md)|指定向项目添加项时要添加的程序集引用。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 此文本指定在实例化项目模板时要添加到项目的程序集。 必须通过以下方式之一指定此程序集名称：

- 作为完整的程序集名称。 例如：

    ```
    <Assembly>
        MyAssembly, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom = null.
    </Assembly>
    ```

- 作为简单的文本引用。 例如：

    ```
    <Assembly> System </Assembly>
    ```

## <a name="remarks"></a>备注
 `Assembly` 是 `Reference` 的必需子元素。

 `References,`和`Reference``Assembly`元素只能在 具有`Type`属性值 的`Item` *.vstemplate*文件中使用。

## <a name="example"></a>示例
 下面的示例说明了项模板`TemplateContent`的元素。 此 XML 添加对*System.dll*和*System.Data.dll*程序集的引用。

```
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
