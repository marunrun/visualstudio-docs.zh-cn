---
title: UsedCommand 元素 |Microsoft Docs
description: UsedCommand 元素允许 VSPackage 访问在另一个 .vsct 文件中定义的命令。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 99cd05d3-644a-42ff-b289-8458cd1b20c0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6d1dcef25413bddbb1eb5c35a47a9dc0d30f4a8f
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715959"
---
# <a name="usedcommand-element"></a>UsedCommand 元素
允许 VSPackage 访问在 .vsct 文件中定义的命令。 例如，如果你的 VSPackage 使用由 shell 定义的标准 **复制** 命令， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 则可以将命令添加到菜单或工具栏，而无需重新实现它。

## <a name="syntax"></a>语法

```
<UsedCommand guid="guidMyCommandGroup" id="MyCommand" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|guid|必需。 标识命令的 GUID ID 对的 GUID。|
|id|必需。 标识命令的 GUID ID 对的 ID。|
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|无||

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[UsedCommands 元素](../extensibility/usedcommands-element.md)|将 UsedCommand 元素和其他 UsedCommands 分组分组。|

## <a name="remarks"></a>备注
 通过将命令添加到 `<UsedCommands>` 元素，VSPackage 向 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 环境通知 VSPackage 需要该命令。 应 `<UsedCommand>` 为包所需的任何命令添加一个元素，Visual Studio 的所有版本和配置中可能不包含此元素。 例如，如果你的包调用特定于 Visual C++ 的命令，则 Visual Web Developer 的用户将不能使用该命令，除非你 `<UsedCommand>` 为该命令包含一个元素。

## <a name="example"></a>示例

```
<UsedCommands>
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>
</UsedCommands>
```

## <a name="see-also"></a>另请参阅
- [UsedCommands 元素](../extensibility/usedcommands-element.md)
- [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
