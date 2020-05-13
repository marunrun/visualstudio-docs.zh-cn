---
title: 将键盘快捷键绑定到菜单项 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- keyboard command
- keyboards
- command key
- keyboard shortcuts
- menu items
ms.assetid: 19f483b6-4d3e-424e-9d68-dc129c788e47
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 94feafbc614be61aaa4eef9e26669c0fbe901ed5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740021"
---
# <a name="bind-keyboard-shortcuts-to-menu-items"></a>将键盘快捷键绑定到菜单项
要将键盘快捷方式绑定到自定义菜单命令，只需向包的 *.vsct*文件添加一个条目。 本主题介绍如何将键盘快捷方式映射到自定义按钮、菜单项或工具栏命令，以及如何在默认编辑器中应用键盘映射或将其限制为自定义编辑器。

 要将键盘快捷键分配给现有的 Visual Studio 菜单项，请参阅[标识和自定义键盘快捷键](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。

## <a name="choose-a-key-combination"></a>选择键组合
 许多键盘快捷键已在可视化工作室中使用。 不应将同一快捷方式分配给多个命令，因为重复绑定很难检测到，并且还可能导致不可预知的结果。 因此，最好在分配快捷方式之前验证快捷方式的可用性。

### <a name="to-verify-the-availability-of-a-keyboard-shortcut"></a>验证键盘快捷键的可用性

1. 在 **"工具** > **选项** > **环境"** 窗口中，选择 **"键盘**"。

2. 确保**在 中使用新快捷方式**设置为**全局**。

3. 在 **"按"快捷键"** 框中，键入要使用的键盘快捷方式。

    如果快捷方式已在 Visual Studio 中使用，则"当前由"框**使用的快捷方式**将显示快捷方式当前调用的命令。

4. 尝试不同的键组合，直到找到未映射的键。

   > [!NOTE]
   > 使用**Alt**的键盘快捷键可能会打开菜单，而不是直接执行命令。 因此，当您键入包含**Alt**的快捷方式时，框**当前使用的快捷方式**可能为空。您可以通过关闭 **"选项"** 对话框然后按键来验证快捷方式未打开菜单。

   以下过程假定您具有具有菜单命令的现有 VSPackage。 如果您需要帮助，请查看[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

### <a name="to-assign-a-keyboard-shortcut-to-a-command"></a>将键盘快捷方式分配给命令

1. 打开包的 *.vsct*文件。

2. 如果不存在，`<KeyBindings>``<Commands>`则在 之后创建空节。

   > [!WARNING]
   > 有关密钥绑定的详细信息，请参阅[密钥绑定](../extensibility/keybinding-element.md)。

    在"`<KeyBindings>`部分"中，`<KeyBinding>`创建一个条目。

    将`guid`和`id`属性设置为要调用的命令的属性。

    将`mod1`属性设置为 **"控件****"、Alt**或**Shift**。

    "键绑定"部分应如下所示：

   ```xml
   <KeyBindings>
       <KeyBinding guid="<name of command set>" id="<name of command id>"
           editor="guidVSStd97" key1="1" mod1="CONTROL"/>
   </KeyBindings>

   ```

   如果键盘快捷键需要两个以上键，请设置`mod2``key2`和 属性。

   在大多数情况下，不应在没有第二个修改器的情况下使用**Shift，** 因为按下它已会导致大多数字母数字键键入大写字母或符号。

   虚拟密钥代码允许您访问没有与其关联的字符的特殊键，例如函数键和**Backspace**键。 有关详细信息，请参阅[虚拟密钥代码](/windows/desktop/inputdev/virtual-key-codes)。

   要使该命令在 Visual Studio 编辑器中可用，`editor`将属性`guidVSStd97`设置为 。

   要使该命令仅在自定义编辑器中可用，可以将`editor`该属性设置为创建包含自定义编辑器的 VSPackage 时[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]包模板生成的自定义编辑器的名称。 要查找名称`<Symbols>`值，请查看`<GuidSymbol>``name`属性以" 结尾的`editorfactory`节点的节。这是自定义编辑器的名称。

## <a name="example"></a>示例
 本示例将键盘快捷键**Ctrl**+**Alt**+**C**绑定`cmdidMyCommand`到名为`MyPackage`的包中命名的命令。

```
<CommandTable>
. . .
<Commands>
. . .
</Commands>
<KeyBindings>
  <KeyBinding guid="guidMyPackageCmdSet" id="cmdidMyCommand"
      key1="C" mod1="CONTROL" mod2="ALT" editor="guidVSStd97" />
</KeyBindings>
. . .
</CommandTable>
```

## <a name="example"></a>示例
 本示例将键盘快捷键**Ctrl**+**B**绑定到`cmdidBold`名为`TestEditor`的项目中命名的命令。 该命令仅在自定义编辑器中可用，而在其他编辑器中不可用。

```xml
<KeyBinding guid="guidVSStd97" id="cmdidBold" editor="guidTestEditorEditorFactory" key1="B" mod1="Control" />
```

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
