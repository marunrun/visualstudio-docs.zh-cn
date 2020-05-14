---
title: 自定义参数元素（可视化工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CustomParameters
helpviewer_keywords:
- CustomParameters element [Visual Studio project templates]
ms.assetid: cf3efc91-1532-4022-bbb8-a18658424fee
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f524996c226f001c68ddc7ac9aa8cb3b99857fc5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739419"
---
# <a name="customparameters-element-visual-studio-templates"></a>自定义参数元素（可视化工作室模板）
对向导进行参数替换时要传递给模板向导的自定义参数进行分组。

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
|[CustomParameter](../extensibility/customparameter-element-visual-studio-templates.md)|可选元素。<br /><br /> 包含自定义参数名称和值，用于从模板创建项目或项时使用。 `CustomParameter` 元素中可能有零个或零个以上的 `CustomParameters` 元素。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[模板内容](../extensibility/templatecontent-element-visual-studio-templates.md)|指定模板的内容。|

## <a name="remarks"></a>备注

## <a name="example"></a>示例
 下面的示例演示如何在模板中使用多个自定义参数。 当从具有以下自定义参数的模板创建项目或项时`$color1$`，模板文件中的所有实例将`$color2$`分别替换为`Red`和`Blue`。

```
<CustomParameters>
    <CustomParameter Name="$color1$" Value="Red"/>
    <CustomParameter Name="$color2$" Value="Blue "/>
</CustomParameters>
```

## <a name="see-also"></a>请参阅
- [自定义参数元素（可视化工作室模板）](../extensibility/customparameter-element-visual-studio-templates.md)
- [模板参数](../ide/template-parameters.md)
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
