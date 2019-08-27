---
title: 如何：使用 XML 代码段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 3a27375b-81cc-48f6-a884-e1cb8c4f78f5
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ba4d98a1d6a59a35bf4aa279831036eecec99989
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440580"
---
# <a name="how-to-use-xml-snippets"></a>如何：使用 XML 代码段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以在“XML 编辑器”的快捷菜单上使用下列两个命令调用 XML 代码段。 **插入代码段**命令将在光标位置处插入 XML 代码段。 **Surround With**命令包装所选文本环绕 XML 代码段。 每个 XML 代码段具有指定的代码段类型。 代码段类型确定是否使用可用代码片段**插入代码段**命令， **Surround With**命令还是两个。  
  
 将 XML 代码段添加到编辑器之后，代码段中的任何可编辑字段将以黄色突出显示，光标位于第一个可编辑字段。  
  
## <a name="insert-snippet"></a>插入代码段  
 下面的过程介绍如何访问**插入代码段**命令。  
  
> [!NOTE]
> **插入代码段**命令也是可通过键盘快捷方式 （CTRL + K，然后选择 CTRL + X）。  
  
#### <a name="to-insert-snippets-from-the-shortcut-menu"></a>从快捷菜单插入代码段  
  
1. 将光标置于要插入 XML 代码段的位置。  
  
2. 右键单击并选择**插入代码段**。  
  
     此时出现可用 XML 代码段的列表。  
  
3. 使用鼠标从列表中选择代码段，或键入代码段的名称后按 TAB 或 ENTER 键来选择代码段。  
  
#### <a name="to-insert-snippets-using-the-intellisense-menu"></a>使用“智能感知”菜单插入代码段  
  
1. 将光标置于要插入 XML 代码段的位置。  
  
2. 从**编辑**菜单，依次指向**IntelliSense**，然后选择**插入代码段**。  
  
     此时出现可用 XML 代码段的列表。  
  
3. 使用鼠标从列表中选择代码段，或键入代码段的名称后按 TAB 或 ENTER 键来选择代码段。  
  
#### <a name="to-insert-snippets-through-the-intellisense-complete-word-list"></a>通过“智能感知完成单词”列表插入代码段  
  
1. 将光标置于要插入 XML 代码段的位置。  
  
2. 开始键入要添加到文件中的 XML 代码段。 如果启用了自动完成，将显示“智能感知完成单词”列表。 如果该列表没有出现，按 CTRL+空格键激活。  
  
3. 从“完成单词”列表中选择 XML 代码段。  
  
4. 按两次 TAB 键调用 XML 代码段。  
  
> [!NOTE]
> 有时可能无法调用 XML 代码段。 例如，如果尝试将 `xs:complexType` 元素插入 `xs:element` 节点，编辑器不会生成 XML 代码段。 如果在 `xs:complexType` 节点中使用 `xs:element` 元素，则不需要任何属性或子元素，所以，编辑器没有任何要插入的数据。  
  
#### <a name="to-insert-snippets-using-the-shortcut-name"></a>使用快捷名称插入代码段  
  
1. 将光标置于要插入 XML 代码段的位置。  
  
2. 在编辑器窗格中键入 `<`。  
  
3. 按 ESC 键关闭“智能感知完成单词”列表。  
  
4. 键入代码段的快捷名称，再按 TAB 键调用 XML 代码段。  
  
## <a name="surround-with"></a>环绕  
 下面的过程介绍如何访问**Surround With**命令。  
  
> [!NOTE]
> **Surround With**命令也是可通过键盘快捷方式 （CTRL + K，然后选择 CTRL + S）。  
  
#### <a name="to-use-surround-with-from-the-context-menu"></a>在上下文菜单中使用“环绕”命令  
  
1. 在“XML 编辑器”中选择要环绕的文本。  
  
2. 右键单击并选择**Surround With**。  
  
     此时出现可用的环绕 XML 代码段的列表。  
  
3. 使用鼠标从列表中选择代码段，或键入代码段的名称后按 TAB 或 ENTER 键来选择代码段。  
  
#### <a name="to-use-surround-with-from-the-intellisense-menu"></a>在“智能感知”菜单中使用“环绕”命令  
  
1. 在“XML 编辑器”中选择要环绕的文本。  
  
2. 从**编辑**菜单，依次指向**IntelliSense**，然后选择**Surround With**。  
  
     此时出现可用的环绕 XML 代码段的列表。  
  
3. 使用鼠标从列表中选择代码段，或键入代码段的名称后按 TAB 或 ENTER 键来选择代码段。  
  
## <a name="using-xml-snippets"></a>使用 XML 代码段  
 选择了 XML 代码段后，代码段的文本将自动插入光标位置。 代码段中的任何可编辑字段都将突出显示，并自动选中第一个可编辑字段。 当前选中的字段将框选。  
  
 选中某个字段后，可以为该字段键入新值。 按 TAB 键在代码段中的可编辑字段之间切换；按 SHIFT+TAB 键按照相反顺序在这些字段之间切换。 单击某个字段可将光标置于该字段中，而双击某个字段可选中该字段。 突出显示某个字段时，可能会显示工具提示，提供对该字段的说明。  
  
 只有给定字段的第一个实例是可编辑的。 突出显示该字段时，该字段的其他实例将以大纲方式显示。 更改了某个可编辑字段的值后，代码段中所有使用该字段的位置均将更改。  
  
 按 ENTER 或 ESC 键会取消字段编辑并使编辑器返回正常状态。  
  
 可以通过修改中的代码片段字段设置更改为可编辑的代码段字段的默认颜色**字体和颜色**窗格**选项**对话框。 有关详细信息，请参阅[如何：在编辑器中更改字体和颜色](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 代码段](../xml-tools/xml-snippets.md)   
 [如何：从 XML 架构生成 XML 代码段](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)   
 [如何：创建 XML 片段](../xml-tools/how-to-create-xml-snippets.md)
