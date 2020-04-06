---
title: 自定义参数元素（可视化工作室模板） |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739430"
---
# <a name="customparameter-element-visual-studio-templates"></a>自定义参数元素（可视化工作室模板）
包含自定义参数名称和值，用于从模板创建项目或项时使用。

## <a name="syntax"></a>语法

```
<CustomParameter Name="name" Value="value">
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`Name`|必需。 参数的名称。 参数的格式是 $*名称*$。|
|`Value`|必需。 参数的替换值。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[CustomParameters](../extensibility/customparameters-element-visual-studio-templates.md)|对向导进行参数替换时要传递给模板向导的自定义参数进行分组。|

## <a name="remarks"></a>备注
 当模板包含`CustomParameter`元素时，每个实例的属性`Name`都将替换为创建的项目或项`Value`文件中的属性。

## <a name="example"></a>示例
 下面的示例演示如何在模板中使用多个自定义参数。 当从具有以下自定义参数的模板创建项目或项时`$color1$`，模板文件中的所有实例将`$color2$`分别替换为`Red`和`Blue`。

```
<CustomParameters>
    <CustomParameter Name="$color1$" Value="Red"/>
    <CustomParameter Name="$color2$" Value="Blue "/>
</CustomParameters>
```

## <a name="see-also"></a>请参阅
- [自定义参数元素（可视化工作室模板）](../extensibility/customparameters-element-visual-studio-templates.md)
- [模板参数](../ide/template-parameters.md)
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
