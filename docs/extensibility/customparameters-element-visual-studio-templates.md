---
title: CustomParameters 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CustomParameters
helpviewer_keywords:
- CustomParameters element [Visual Studio project templates]
ms.assetid: cf3efc91-1532-4022-bbb8-a18658424fee
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8089e84f5414798fdf6a4707e8bde65e4df5e0a2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350211"
---
# <a name="customparameters-element-visual-studio-templates"></a>CustomParameters 元素 （Visual Studio 模板）
组是在该向导可以将参数替换项时要传递到模板向导的自定义参数。

## <a name="syntax"></a>语法

```
<CustomParameters>
    <CustomParameter/>
    <CustomParameter/>
</CustomParameters>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[CustomParameter](../extensibility/customparameter-element-visual-studio-templates.md)|可选元素。<br /><br /> 包含自定义参数名称和从模板创建项目或项时要使用的值。 `CustomParameter` 元素中可能有零个或零个以上的 `CustomParameters` 元素。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|指定模板的内容。|

## <a name="remarks"></a>备注

## <a name="example"></a>示例
 下面的示例演示如何在模板中使用多个自定义参数。 当从具有以下自定义参数的所有实例的模板创建项目或项`$color1$`并`$color2$`在模板中的文件将替换`Red`和`Blue`分别。

```
<CustomParameters>
    <CustomParameter Name="$color1$" Value="Red"/>
    <CustomParameter Name="$color2$" Value="Blue "/>
</CustomParameters>
```

## <a name="see-also"></a>请参阅
- [CustomParameter 元素 （Visual Studio 模板）](../extensibility/customparameter-element-visual-studio-templates.md)
- [模板参数](../ide/template-parameters.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)