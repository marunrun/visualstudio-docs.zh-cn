---
title: 如何使用 XML 代码段
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 3a27375b-81cc-48f6-a884-e1cb8c4f78f5
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: decc565eca9b7299761405e06c0cecf82f63319d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592602"
---
# <a name="how-to-use-xml-snippets"></a>如何：使用 XML 代码段

可以通过在 "XML 编辑器" 快捷菜单上使用以下两个命令来调用 XML 代码段。 "**插入代码段**" 命令将 XML 代码段插入到光标位置。 "**环绕**" 命令环绕所选文本周围的 XML 代码段。 每个 XML 代码段具有指定的代码段类型。 代码段类型通过 "**插入代码段**" 命令、"**环绕**" 命令或两者来确定代码段是否可用。

将 XML 代码段添加到编辑器之后，代码段中的任何可编辑字段将以黄色突出显示，光标位于第一个可编辑字段。

## <a name="insert-snippet"></a>插入代码段

以下过程描述如何访问 "**插入代码段**" 命令。

> [!NOTE]
> 还可以通过键盘快捷方式（**ctrl**+**K**，然后按**ctrl**+**X**）访问 "**插入代码段**" 命令。

### <a name="to-insert-snippets-from-the-shortcut-menu"></a>从快捷菜单插入代码段

1. 将光标置于要插入 XML 代码段的位置。

2. 右键单击并选择 "**插入代码片段**"。

   此时出现可用 XML 代码段的列表。

3. 使用鼠标从列表中选择代码段，或键入代码段的名称并按**tab**或**enter**。

### <a name="to-insert-snippets-using-the-intellisense-menu"></a>使用“智能感知”菜单插入代码段

1. 将光标置于要插入 XML 代码段的位置。

2. 在 "**编辑**" 菜单中，指向 " **IntelliSense**"，然后选择 "**插入代码片段**"。

   此时出现可用 XML 代码段的列表。

3. 使用鼠标从列表中选择代码段，或键入代码段的名称并按**tab**或**enter**。

### <a name="to-insert-snippets-through-the-intellisense-complete-word-list"></a>通过 "IntelliSense 完成单词" 列表插入代码段

1. 将光标置于要插入 XML 代码段的位置。

2. 开始键入要添加到文件中的 XML 代码段。 如果启用了自动完成，将显示“智能感知完成单词”列表。 如果未显示，请按**Ctrl** **+"** 以激活它。

3. 从“完成单词”列表中选择 XML 代码段。

4. 按**tab**键 **，调用**XML 代码段。

> [!NOTE]
> 有时可能无法调用 XML 代码段。 例如，如果尝试将 `xs:complexType` 元素插入 `xs:element` 节点，编辑器不会生成 XML 代码段。 如果在 `xs:complexType` 节点中使用 `xs:element` 元素，则不需要任何属性或子元素，所以，编辑器没有任何要插入的数据。

### <a name="to-insert-snippets-using-the-shortcut-name"></a>使用快捷名称插入代码段

1. 将光标置于要插入 XML 代码段的位置。

2. 在编辑器窗格中键入 `<`。

3. 按**Esc**关闭 "IntelliSense 完成单词" 列表。

4. 键入代码段的快捷方式名称，然后按**tab**键调用 XML 代码段。

## <a name="surround-with"></a>环绕

以下过程描述如何访问 "**外侧代码**" 命令。

> [!NOTE]
> "**环绕**" 命令也可通过键盘快捷方式（**ctrl**+**K**，然后按**ctrl**+**S**）提供。

### <a name="to-use-surround-with-from-the-context-menu"></a>在上下文菜单中使用 "外侧代码"

1. 选择要在 XML 编辑器中环绕的文本。

2. 右键单击并选择 "**外侧代码**"。

   此时出现可用的环绕 XML 代码段的列表。

3. 使用鼠标从列表中选择代码段，或键入代码段的名称并按**tab**或**enter**。

### <a name="to-use-surround-with-from-the-intellisense-menu"></a>在 IntelliSense 菜单中使用 "外侧代码"

1. 选择要在 XML 编辑器中环绕的文本。

2. 在 "**编辑**" 菜单中，指向 " **IntelliSense**"，然后选择 "**外侧代码**"。

   此时出现可用的环绕 XML 代码段的列表。

3. 使用鼠标从列表中选择代码段，或键入代码段的名称并按**tab**或**enter**。

## <a name="use-xml-snippets"></a>使用 XML 片段

选择了 XML 代码段后，代码段的文本将自动插入光标位置。 代码段中的任何可编辑字段都将突出显示，并自动选中第一个可编辑字段。 当前选中的字段将框选。

选中某个字段后，可以为该字段键入新值。 按**tab**循环遍历代码段的可编辑字段;按**Shift**+**tab**按相反的顺序循环切换。 单击某个字段可将光标置于该字段中，而双击某个字段可选中该字段。 突出显示某个字段时，可能会显示工具提示，提供对该字段的说明。

只有给定字段的第一个实例是可编辑的。 突出显示该字段时，该字段的其他实例将以大纲方式显示。 更改了某个可编辑字段的值后，代码段中所有使用该字段的位置均将更改。

按**enter**或**Esc**可取消字段编辑，并将编辑器返回到 normal。

可以通过修改 "**选项**" 对话框的 "**字体和颜色**" 窗格中的 "**代码片段字段**" 设置来更改可编辑代码段字段的默认颜色。 有关详细信息，请参阅[如何：更改编辑器中的字体和颜色](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md)。

## <a name="see-also"></a>另请参阅

- [XML 代码段](../xml-tools/xml-snippets.md)
- [如何：从 XML 架构生成 XML 代码段](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)
- [如何：创建 XML 代码段](../xml-tools/how-to-create-xml-snippets.md)
