---
title: " (Visual Studio 模板) 的 CustomParameter 元素 |Microsoft Docs"
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CustomParameter
helpviewer_keywords:
- CustomParameters element [Visual Studio project templates]
ms.assetid: 743c4489-74ac-403a-bbaa-eed7d785a3ac
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9063a354f03b896e189566e8d84a18caf7509db8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739430"
---
# <a name="customparameter-element-visual-studio-templates"></a> (Visual Studio 模板的 CustomParameter 元素) 
包含从模板创建项目或项时要使用的自定义参数名和值。

## <a name="syntax"></a>语法

```
<CustomParameter Name="name" Value="value">
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|`Name`|必需。 参数的名称。 参数的格式为 $*name*$。|
|`Value`|必需。 参数的替换值。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CustomParameters](../extensibility/customparameters-element-visual-studio-templates.md)|在向导进行参数替换时，将要传递给模板向导的自定义参数分组。|

## <a name="remarks"></a>备注
 如果模板包含 `CustomParameter` 元素，则每个实例都会将 `Name` 属性替换为 `Value` 所创建项目或项文件中的属性。

## <a name="example"></a>示例
 下面的示例演示如何在模板中使用多个自定义参数。 使用以下自定义参数从模板创建项目或项时， `$color1$` 模板文件中和的所有实例 `$color2$` 将分别替换为 `Red` 和 `Blue` 。

```
<CustomParameters>
    <CustomParameter Name="$color1$" Value="Red"/>
    <CustomParameter Name="$color2$" Value="Blue "/>
</CustomParameters>
```

## <a name="see-also"></a>另请参阅
- [ (Visual Studio 模板的 CustomParameters 元素) ](../extensibility/customparameters-element-visual-studio-templates.md)
- [模板参数](../ide/template-parameters.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
