---
title: 参考元素（可视化工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#References
helpviewer_keywords:
- <References> element [Visual Studio Templates]
- References element [Visual Studio Templates]
ms.assetid: 1969146d-46bf-422d-8d46-0e9493925003
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ef31c5e7550ec7c6e4570d156d364afcf4ad6819
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701604"
---
# <a name="references-element-visual-studio-templates"></a>引用元素（可视化工作室模板）
对模板添加到项目中的程序集引用进行分组。

 \<VStemplate \<>模板内容\<>引用>

## <a name="syntax"></a>语法

```xml
<References>
    <Reference>... </Reference>
    <Reference>... </Reference>
    ...
</References>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[参考](../extensibility/reference-element-visual-studio-templates.md)|必需元素。<br /><br /> 指定向项目添加项时要添加的程序集引用。 元素中必须存在一`Reference``References`个或多个元素。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[模板内容](../extensibility/templatecontent-element-visual-studio-templates.md)|指定模板的内容。|

## <a name="remarks"></a>备注
 `References` 是 `TemplateContent` 的可选子元素。

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
