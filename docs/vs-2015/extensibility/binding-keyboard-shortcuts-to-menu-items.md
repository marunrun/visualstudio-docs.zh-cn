---
title: 绑定到菜单项的键盘快捷方式 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- keyboard command
- keyboards
- command key
- keyboard shortcuts
- menu items
ms.assetid: 19f483b6-4d3e-424e-9d68-dc129c788e47
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fb85bc64164acc09aef6464b69e72b7c6cf46d77
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63405620"
---
# <a name="binding-keyboard-shortcuts-to-menu-items"></a>将键盘快捷方式绑定到菜单项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要绑定到自定义菜单命令的键盘快捷方式，只需向包.vsct 文件添加一个条目。 本主题说明如何映射到自定义按钮、 菜单项或工具栏命令的键盘快捷方式以及如何将应用的默认编辑器中的键盘映射或将其限制到自定义编辑器。  
  
 若要将键盘快捷方式分配到现有的 Visual Studio 菜单项，请参阅[标识并自定义键盘快捷键](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。  
  
## <a name="choosing-a-key-combination"></a>选择键组合  
 Visual Studio 中已使用多个键盘快捷方式。 不应将相同的快捷方式分配给多个命令，因为很难检测到重复的绑定，并且可能还会导致不可预知的结果。 因此，最好先验证快捷方式的可用性，然后将其分配。  
  
#### <a name="to-verify-the-availability-of-a-keyboard-shortcut"></a>若要验证键盘快捷方式的可用性  
  
1. 在中**工具 / 选项 / 环境**窗口中，选择**键盘**。  
  
2. 请确保**新快捷方式**设置为**Global**。  
  
3. 在中**按快捷键**框中，键入你想要使用的键盘快捷方式。  
  
    如果在 Visual Studio 中，已使用该快捷方式**快捷键的当前使用**框将显示当前调用快捷方式命令。  
  
4. 直到找到未映射，请尝试不同的键组合。  
  
   > [!NOTE]
   > 使用 ALT 的键盘快捷方式可能打开一个菜单，并不是直接执行命令。 因此，**快捷键的当前使用**类型包括 ALT 的快捷方式时，框可能为空。 你可以验证快捷方式不会打开一个菜单，通过关闭**选项**对话框，然后按多个键。  
  
   以下过程假设您有一个菜单命令与现有 VSPackage。 如果您需要执行该操作的帮助，看一看[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
#### <a name="to-assign-a-keyboard-shortcut-to-a-command"></a>若要为命令分配键盘快捷方式  
  
1. 打开您的包的.vsct 文件。  
  
2. 创建一个空`<KeyBindings>`部分后`<Commands>`如果尚不存在。  
  
   > [!WARNING]
   > 键绑定的详细信息，请参阅[键绑定](../extensibility/keybinding-element.md)。  
  
    在中`<KeyBindings>`部分中，创建`<KeyBinding>`条目。  
  
    设置`guid`和`id`属性到那些想要调用的命令。  
  
    设置`mod1`归于**控制**， **Alt**，或**Shift**。  
  
    键绑定部分应如下所示：  
  
   ```xml  
   <KeyBindings>  
       <KeyBinding guid="<name of command set>" id="<name of command id>"  
           editor="guidVSStd97" key1="1" mod1="CONTROL"/>  
   </KeyBindings>  
  
   ```  
  
   如果您的键盘快捷方式需要两个以上的键，则设置`mod2`和`key2`属性。  
  
   在大多数情况下， **Shift**不应在由于已按导致大多数键入大写字母或符号的字母数字键使用不带第二个修饰符。  
  
   虚拟键代码使你可以访问不具有字符与它们，例如，功能键相关联的特殊键和**退格符**密钥。 有关详细信息，请参阅[虚拟键代码](http://go.microsoft.com/fwlink/?LinkID=105932)。  
  
   若要使该命令在 Visual Studio 中提供编辑器，将设置`editor`属性为`guidVSStd97`。  
  
   若要使该命令仅适用于自定义编辑器，将设置`editor`属性生成的自定义编辑器的名称为[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]包模板创建 VSPackage 时包括自定义编辑器。 若要查找的名称值，查看`<Symbols>`部分，了解`<GuidSymbol>`节点其`name`属性以结尾"`editorfactory`。"这是自定义编辑器的名称。  
  
## <a name="example"></a>示例  
 此示例绑定到名为的命令的键盘快捷方式 CTRL + ALT + C`cmdidMyCommand`在包中名为`MyPackage`。  
  
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
 此示例绑定到名为的命令的键盘快捷方式 CTL + B`cmdidBold`在项目中名为`TestEditor`。 仅在自定义编辑器中和不在其他编辑器提供了该命令。  
  
```xml  
<KeyBinding guid="guidVSStd97" id="cmdidBold" editor="guidTestEditorEditorFactory" key1="B" mod1="Control" />  
```  
  
## <a name="see-also"></a>请参阅  
 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
