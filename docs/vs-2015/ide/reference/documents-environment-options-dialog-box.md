---
title: “选项”对话框 ->“环境”->“文档”| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.Environment.Documents
- VS.ToolsOptionsPages.Environment.Documents
- VS.ToolsOptionsPag.Environment.Documents
helpviewer_keywords:
- Documents Environment Options dialog box
- defaults, directories
- error messages, customizing
- files [Visual Studio], default options
- files [Visual Basic], auto-loading modified
- windows, customizing environment
- in-memory editing
- folders [Visual Studio], specifying where Open File goes
- Open File dialog box
- windows, enabling re-use of current
- notifications, files changed
- files [Visual Studio], displaying in Solution Explorer
- default directories
- read-only files, editing
- Options dialog box, showing Miscellaneous Files
- directories [Visual Studio], IDE environment options
- Options dialog box, Documents page
- warnings, files changed
- Solution Explorer, displaying files in
ms.assetid: 4e3ccf1b-cd68-4db6-9470-710c911b47fc
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a6616593f01218b4a7e15809f841ee3cb4e7edb0
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65700800"
---
# <a name="documents-environment-options-dialog-box"></a>“选项”对话框 ->“环境”->“文档”
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用“选项”对话框的此页，可以控制文档在集成开发环境 (IDE) 中的显示，并管理对文档和文件的外部更改。 通过在“工具”菜单上单击“选项”，然后在“环境”节点中选择“文档”，即可访问此对话框。 如果“文档”未出现在列表中，请在“选项”对话框中选择“显示所有设置”。  
  
> [!NOTE]
> 对话框中的可用选项以及显示的菜单命令的名称和位置可能与“帮助”中的描述不同，具体取决于您的当前设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
 **如果已保存，请再次使用当前文档窗口**  
 选定后，若当前文档已保存，则将其关闭，而后在同一窗口中打开一个新文档。 如果尚未保存当前文档，则保持打开状态，并在单独的窗口中打开新文档。 清除此选项后，新文档始终在单独的窗口中打开。  
  
 如果不经常执行多文档剪切和粘贴操作，并希望尽可能减少工作区中打开的文档和窗口数，可尝试使用此选项。  
  
 **当文件在该环境外发生更改时进行检测**  
 选中此选项后，如果打开的文件在 IDE 外由某个编辑器进行了更改，则会有一条消息立即通知你有关的更改。 消息会让你从存储重新加载文件。  
  
 **自动加载更改(如果已保存)**  
 如果选中了“当文件在该环境外发生更改时进行检测”，并且 IDE 中有打开的文件在 IDE 外被更改，默认情况下将生成一条警告消息。 启用此选项后，将不会出现警告，并且文档将在 IDE 中重新加载以纳入外部更改。  
  
 **允许编辑只读文件，但在尝试保存时发出警告**  
 启用此选项后，可以打开并编辑只读文件。 完成后，若要保存所做更改的记录，必须使用“另存为”命令以新的名称保存文件。  
  
 **使用当前活动文档的目录打开文件**  
 选中后，此选项会指定“打开文件”对话框显示活动文档的目录。 清除此选项后，“打开文件”对话框会显示上次打开文件使用的目录。  
  
 **加载时检查一致的行尾**  
 如果选择此选项，编辑器便会扫描文件中的行尾，如果检测到行尾的格式有不一致的情况，则显示一个消息框。  
  
 **当全局撤消操作会导致修改已编辑的文件时发出警告**  
 如果选择此选项，则在“全局撤消”命令将回滚在重构操作后也被更改的文件中的重构更改时，将显示一个消息框。 将文件返回其重构前状态可能会放弃随后在文件中进行的更改。  
  
 **在解决方案资源管理器中显示杂项文件**  
 选择此选项可在“解决方案资源管理器”中显示“杂项文件”节点。 杂项文件是与项目或解决方案并不关联的文件，但为了方便使用，可将它们显示在“解决方案资源管理器”中。  
  
> [!NOTE]
> 选择此选项可对没有包括在活动 Web 应用程序中的 Web 文档启用“文件”菜单上的“在浏览器中查看”命令。  
  
 \< n > 保存在杂项文件项目中的项  
 指定要保留在“解决方案资源管理器”的“杂项文件”文件夹中的文件数。 即使编辑器中不再打开这些文件，它们也将被列出。 可以指定从 0 到 256 之间的任意整数。 默认数为 0。  
  
 例如，如果将此选项设为 5，而且已打开了 10 个杂项文件，则在关闭全部 10 个文件后，前 5 个文件仍将显示在“杂项文件”文件夹中。  
  
 **不能以代码页的形式保存数据时将文档保存为 Unicode**  
 如果选择此选项，则默认情况下，将包含与选定代码页不兼容信息的文件另存为 Unicode。  
  
## <a name="see-also"></a>请参阅  
 [“选项”对话框 ->“环境”](../../ide/reference/environment-options-dialog-box.md)   
 [杂项文件](../../ide/reference/miscellaneous-files.md)   
 [查找和替换文本](../../ide/finding-and-replacing-text.md)
