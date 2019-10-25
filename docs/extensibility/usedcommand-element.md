---
title: UsedCommand 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 99cd05d3-644a-42ff-b289-8458cd1b20c0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44ea8f27cafb166968f66c53dc68398526e0aa5d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72718777"
---
# <a name="usedcommand-element"></a>UsedCommand 元素
允许 VSPackage 访问在 .vsct 文件中定义的命令。 例如，如果你的 VSPackage 使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] shell 定义的标准**复制**命令，则可以将命令添加到菜单或工具栏，而无需重新实现它。

## <a name="syntax"></a>语法

```
<UsedCommand guid="guidMyCommandGroup" id="MyCommand" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|guid|必须的。 标识命令的 GUID ID 对的 GUID。|
|id|必须的。 标识命令的 GUID ID 对的 ID。|
|条件|可选。 请参阅[条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|None||

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[UsedCommands 元素](../extensibility/usedcommands-element.md)|将 UsedCommand 元素和其他 UsedCommands 分组分组。|

## <a name="remarks"></a>备注
 通过将命令添加到 `<UsedCommands>` 元素，VSPackage 向 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 环境通知 VSPackage 需要该命令。 应为包所需的任何命令添加一个 `<UsedCommand>` 元素，Visual Studio 的所有版本和配置中可能不包含此元素。 例如，如果你的包调用特定于视觉对象C++的命令，则 Visual Web Developer 的用户将不能使用该命令，除非你为该命令包含 `<UsedCommand>` 元素。

## <a name="example"></a>示例

```
<UsedCommands>
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>
</UsedCommands>
```

## <a name="see-also"></a>请参阅
- [UsedCommands 元素](../extensibility/usedcommands-element.md)
- [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)