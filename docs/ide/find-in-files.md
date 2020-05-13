---
title: 在文件中查找
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.findreplace.findinfiles
- vs.findinfiles
helpviewer_keywords:
- objects [Visual Studio], finding
- text searches, replacing text
- objects [Visual Studio], searching for
- Find and Replace window, Find in Files tab
- text searches, Find and Replace window
- documents, searching
- files, searching
- Find in Files tab, Find and Replace window
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5e1f067df647f843819e085f283005606699f3bb
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75595470"
---
# <a name="find-in-files"></a>在文件中查找

“在文件中查找”可用于搜索指定的一组文件  。 找到的匹配项与所执行的操作在“结果选项”中选择的“查找结果”窗口中列出   。

可以使用以下任一方法在“查找和替换”窗口中显示“在文件中查找”   。

## <a name="to-display-find-in-files"></a>显示“在文件中查找”

1. 在菜单栏中，依次选择“编辑” **“查找和替换”**  >   。

1. 选择“在文件中查找”  。

若要取消“查找”操作，请按 Ctrl**Break** +   。

> [!NOTE]
> “查找和替换”工具不会搜索具有 `Hidden` 或 `System` 属性的目录。

## <a name="find-what"></a>查找内容

若要搜索一个新的文本字符串或表达式，请在框中进行指定。 若要搜索最近搜索的 20 条字符串中的任意一条，请打开下拉列表并选择字符串。 若要在搜索字符串中使用一个或多个正则表达式，请选择相邻的“表达式生成器”按钮  。 有关详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

> [!NOTE]
> 只有在“查找选项”下选择了“使用正则表达式”后，“表达式生成器”按钮才会启用    。

## <a name="look-in"></a>查找范围

从“查找范围”  下拉列表中选择的选项将确定“在文件中查找”  是仅在当前活动文件中搜索，还是在特定文件夹内存储的所有文件中搜索。 从列表中选择搜索范围，或单击“浏览(...)”按钮以显示“选择搜索文件夹”对话框并输入自己的目录集   。 也可以直接在“查找范围”框中键入路径  。

> [!WARNING]
> 使用“整个解决方案”或“当前项目”选项，可不搜索项目和解决方案文件   。 如果想要在项目文件进行查找，请选择搜索文件夹。

> [!NOTE]
> 如果选中“查找范围”选项会导致搜索已从源代码管理中签出的文件，则只会搜索已下载到本机计算机的文件版本  。

## <a name="include-subfolders"></a>包含子文件夹

指定将搜索“查找范围”文件夹的子文件夹  。

## <a name="find-options"></a>查找选项

可以展开或折叠“查找选项”部分  。 可以选择或清除以下选项：

**区分大小写**

如果选择此选项，“查找结果”搜索将区分大小写 

**全字匹配**

如果选择此选项，“查找结果”窗口将仅返回全字匹配项  。

**使用正则表达式**

如果选中此复选框，则可以使用特殊表示法在“查找内容”或“替换为”文本框中定义要匹配的文本模式   。 有关这些表示法的列表，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

**查找以下文件类型**

此列表指示要在“查找范围”目录中搜索的文件类型  。 如果此字段为空白，则将搜索“查找范围”目录中的所有文件  。

选择列表中的任意项以输入预配置的搜索字符串，该字符串将查找那些特定类型的文件。

## <a name="result-options"></a>结果选项

可以展开或折叠“结果选项”部分  。 可以选择或清除以下选项：

**“查找结果 1”窗口**

如果选择此选项，当前的搜索结果将替换“查找结果 1”窗口中的内容  。 此窗口将自动打开以显示搜索结果。 若要手动打开此窗口，请从“视图”菜单中选择“其他窗口”，然后选择“查找结果 1”    。

**“查找结果 2”窗口**

如果选择此选项，当前的搜索结果将替换“查找结果 2”窗口中的内容  。 此窗口将自动打开以显示搜索结果。 若要手动打开此窗口，请从“视图”菜单中选择“其他窗口”，然后选择“查找结果 2”    。

**只显示文件名**

显示包含搜索匹配项的文件列表，而不显示搜索匹配项本身。

**附加结果**

从搜索的结果追加到以前的搜素结果。

## <a name="see-also"></a>另请参阅

- [查找和替换文本](../ide/finding-and-replacing-text.md)
- [在文件中替换](../ide/replace-in-files.md)
- [Visual Studio 命令](../ide/reference/visual-studio-commands.md)
