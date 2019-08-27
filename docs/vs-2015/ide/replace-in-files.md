---
title: 在文件中替换 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.findreplace.replaceinfiles
- vs.replaceinfiles
helpviewer_keywords:
- text searches, replacing text
- Find and Replace window, Replace in Files tab
- Replace in Files tab, Find and Replace window
ms.assetid: ca361466-53bd-44db-a28a-3a74bc03b028
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 72a20b0271542dd914aeb592dda3f0cb446a0000
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698676"
---
# <a name="replace-in-files"></a>在文件中替换
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

借助“在文件中替换”功能，可以在一组指定文件的代码中搜索某个字符串或表达式，并更改一部分或全部的匹配项。 找到的匹配项与所执行的操作在“结果选项”中选择的“查找结果”窗口中列出。  
  
> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在“工具”菜单上选择“导入和导出设置”。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
 可以使用以下任一方法在“查找和替换”窗口中显示“在文件中替换”。  
  
### <a name="to-display-replace-in-files"></a>显示“在文件中替换”  
  
1. 在“编辑”菜单上展开“查找和替换”。  
  
2. 选择“在文件中替换”。  
  
     — 或 —  
  
     如果已经打开“查找和替换”窗口，则在工具栏上选择“在文件中替换”。  
  
## <a name="find-what"></a>查找内容  
 若要搜索一个新的文本字符串或表达式，请在框中进行指定。 若要搜索最近搜索的 20 条字符串中的任意一条，请打开列表并选择想要搜索的字符串。 若要在搜索字符串中使用一个或多个正则表达式，请选择相邻的“表达式生成器”按钮。 有关详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。  
  
## <a name="replace-with"></a>替换为  
 若要将“查找内容”框中的字符串实例替换为其他字符串，请在“替换为”框中输入替换字符串。 若要删除“查找内容”框中的字符串实例，则保留该字段为空。 打开列表，显示最近搜索的 20 个字符串。 若要在替换字符串中使用一个或多个正则表达式，请选择相邻的“表达式生成器”按钮。 有关详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。  
  
## <a name="look-in"></a>查找范围  
 从“查找范围”下拉列表中选择的选项可确定是仅在当前活动文件中进行“在文件中替换”搜索，还是在存储于某些文件夹的所有文件中进行此种搜索。 从列表中选择搜索范围，键入文件夹路径，或单击“浏览(...)”按钮，即可显示“选择搜索文件夹”对话框并选择要搜索的一组文件夹。 也可以直接在“查找范围”框中键入路径。  
  
> [!NOTE]
> 如果选中“查找范围”选项会导致搜索已从源代码管理中签出的文件，则只会搜索已下载到本机计算机的文件版本。  
  
## <a name="find-options"></a>查找选项  
 可以展开或折叠“查找选项”部分。 可以选择或清除以下选项：  
  
 区分大小写  
 选中时，“查找结果”窗口将仅显示内容和大小写均匹配的“查找内容”字符串实例。 例如，选中“区分大小写”后搜索“MyObject”会返回“MyObject”，而不会返回“myobject”或“MYOBJECT”。  
  
 全字匹配  
 选中时，“查找结果”窗口将仅显示全字匹配的“查找内容”字符串实例。 例如，搜索“MyObject”会返回“MyObject”，而不会返回“CMyObject”或“MyObjectC”。  
  
 使用正则表达式  
 选中此复选框后，可以使用特殊表示法在“查找内容”或“替换为”文本框中定义文本模式。 有关这些表示法的列表，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。  
  
 查找以下文件类型  
 此列表指示要在“查找范围”目录中搜索的文件类型。 如果此字段留空，则将搜索“查找范围”目录中的所有文件。  
  
 选择列表中的任意项以输入预配置的搜索字符串，该字符串将查找那些特定类型的文件。  
  
## <a name="result-options"></a>结果选项  
 可以展开或折叠“结果选项”部分。 可以选择或清除以下选项：  
  
 查找结果 1 窗口  
 如果选择此选项，当前的搜索结果将替换“查找结果 1”窗口中的内容。 此窗口将自动打开以显示搜索结果。 若要手动打开此窗口，请从“视图”菜单中选择“其他窗口”，然后选择“查找结果 1”。  
  
 查找结果 2 窗口  
 如果选择此选项，当前的搜索结果将替换“查找结果 2”窗口中的内容。 此窗口将自动打开以显示搜索结果。 若要手动打开此窗口，请从“视图”菜单中选择“其他窗口”，然后选择“查找结果 2”。  
  
 只显示文件名  
 如果选中此复选框，则“查找结果”窗口将列出所有包含搜索字符串的文件的完整名称和路径。 但是，结果不包含显示字符串的代码行。 此复选框仅可用于“在文件中查找”。  
  
 “全部替换”后，保持已修改的文件处于打开状态  
 如果选中此选项，进行过替换的文件会保持打开状态，便于撤消或保存所做的更改。 内存约束会限制替换操作之后保持打开状态的文件数。  
  
> [!CAUTION]
> 仅可对保持打开状态以供编辑的文件使用“撤消”。 如果未选择此选项，则尚未打开以供编辑的文件将保持关闭状态，并且“撤销”选项不可用于这些文件。  
  
## <a name="see-also"></a>请参阅  
 [查找和替换文本](../ide/finding-and-replacing-text.md)   
 [在文件中查找](../ide/find-in-files.md)   
 [Visual Studio 命令](../ide/reference/visual-studio-commands.md)
