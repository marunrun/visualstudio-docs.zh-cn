---
title: 所需平台版本元素（可视化工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 6f0e4986-3157-4bba-aed3-c28413ebe976
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3bc22f97401fe5e3724f2e44c873c72acbf65be1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701493"
---
# <a name="requiredplatformversion-element-visual-studio-templates"></a>必需平台版本元素（可视化工作室模板）
指定项目模板正常工作所需的操作系统的最小版本。 此元素用于创建[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]应用的项目模板。

 该`RequiredPlatformVersion`值与操作系统的版本直接进行比较。 如果`RequiredPlatformVersion`高于操作系统版本，则模板不会显示在 **"新项目**"对话框中。 要为[!INCLUDE[win8](../debugger/includes/win8_md.md)]或更高指定模板，请设置为`RequiredPlatformVersion`6.2.0。 要为[!INCLUDE[win81](../debugger/includes/win81_md.md)]或更高指定模板，请设置为`RequiredPlatformVersion`6.3.0。

 指定`RequiredPlatformVersion`|8 的模板与以前的客户[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]模板兼容。

 VSTemplate 模板数据 ...目标平台名称必需平台版本

## <a name="syntax"></a>语法

```xml
<RequiredPlatformVersion> OperatingSystem </RequiredPlatformVersion>
```

## <a name="attributes-and-elements"></a>特性和元素
 无。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[模板平台名称](../extensibility/templatedata-element-visual-studio-templates.md)|指定项目模板面向的平台。|

## <a name="text-value"></a>文本值
 需要一个文本值。

## <a name="remarks"></a>备注
 此文本指定模板所需的最小操作系统版本。

## <a name="example"></a>示例
 此示例指定项目模板面向 [!INCLUDE[win8](../debugger/includes/win8_md.md)] 或更高版本。

```xml
<VSTemplate Type="Project" Version="3.0.0"    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <TargetPlatformName>Windows</TargetPlatformName>
            <RequiredPlatformVersion>6.3.0</RequiredPlatformVersion>

    </TemplateData>
    <TemplateContent>

    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [目标平台名称元素（可视化工作室模板）](../extensibility/targetplatformname-element-visual-studio-templates.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
