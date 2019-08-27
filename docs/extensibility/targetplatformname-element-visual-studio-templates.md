---
title: TargetPlatformName 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 3a6b1f45-b5d6-418e-add1-87ee8f15033d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c307a52b8f252f5059f2d4009e98fc4d497f616e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316698"
---
# <a name="targetplatformname-element-visual-studio-templates"></a>TargetPlatformName 元素（Visual Studio 模板）
指定项目模板面向的平台。 此元素用于指定项目模板用于创建 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用。

## <a name="syntax"></a>语法

```xml
<VSTemplate>
    <TemplateData>
        <TargetPlatformName> OperatingSystem</TargetPlatformName>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[RequiredPlatformVersion](../extensibility/requiredplatformversion-element-visual-studio-templates.md)|指定项目模板面向的操作系统版本。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

## <a name="remarks"></a>备注
 文本必须为 **Windows**。

## <a name="example"></a>示例
 此示例指定项目模板面向 [!INCLUDE[win8](../debugger/includes/win8_md.md)] 或更高版本。

```xml
<VSTemplate Type="Project" Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <TargetPlatformName>Windows</TargetPlatformName>
        <RequiredPlatformVersion>8</RequiredPlatformVersion>
    </TemplateData>
    <TemplateContent> </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)