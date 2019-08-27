---
title: 命令 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Visual Studio, commands
- commands, Visual Studio
- command syntax
ms.assetid: 76ffa394-ee89-4629-aba9-1a62b72e6cc1
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 10ce4bd59567d7d055dd107dd05358d994d22c36
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160869"
---
# <a name="visual-studio-commands"></a>Visual Studio 命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio 命令允许你调用“命令”  窗口、“即时”  窗口或“查找/命令”  框中的命令。 在每种情况下，都使用大于号 (`>`) 指示后面跟随的是命令，而不是搜索或调试操作。

 可以在“键盘，环境选项”  对话框中找到命令及其语法的完整列表。

 Visual Studio 命令的转义符是一个插入符号 (^) 字符，其表示紧随其后的字符将按字面意思而不是作为控制字符进行解释。 这可以用于嵌入参数或开关值中的直引号 (")、空格、前导斜杠，插入符号或其他任何字符，开关名称除外。 例如，应用于对象的

```
>Edit.Find ^^t /regex
```

 插入符号在引号内或引号外的作用相同。 如果插入符号是行的最后一个字符，则忽略不计。

 在 IDE 的本地化版本中，可用 IDE 的本地语言或英语输入命令名称。 例如，可以键入 `File.NewFile` 或法语 IDE 中的 `Fichier.NouveauFichier` 执行同一命令。

 许多命令具有别名。 有关命令别名列表的信息，请参阅 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)。

 以下命令采用参数和/或开关。

|命令名：|描述|
|------------------|-----------------|
|[添加现有项](../../ide/reference/add-existing-item-command.md)|将现有文件添加到当前解决方案中并打开它。|
|[添加现有项目](../../ide/reference/add-existing-project-command.md)|将现有项目添加到当前解决方案中。|
|[添加新项](../../ide/reference/add-new-item-command.md)|将新的解决方案项，如.htm、.css、.txt 或框架集添加到当前解决方案中并打开它。|
|[Alias](../../ide/reference/alias-command.md)|为完整命令、完整命令和参数、甚至另一个别名创建新别名。|
|[计算语句](../../ide/reference/evaluate-statement-command.md)|计算并显示给定的语句。|
|[查找](../../ide/reference/find-command.md)|使用“查找和替换”  控件上可用的选项子集搜索文件。|
|[在文件中查找](../../ide/reference/find-in-files-command.md)|使用“查找和替换” [在文件中查找](../../ide/find-in-files.md)。|
|[转到](../../ide/reference/go-to-command.md)|将光标移到指定的行。|
|[列出调用堆栈](../../ide/reference/list-call-stack-command.md)|显示当前调用堆栈。|
|[列出反汇编](../../ide/reference/list-disassembly-command.md)|开始调试进程，并允许指定如何处理错误。|
|[列出内存](../../ide/reference/list-memory-command.md)|显示指定范围内内存的内容。|
|[列出模块](../../ide/reference/list-modules-command.md)|列出当前进程的模块。|
|[列出寄存器](../../ide/reference/list-registers-command.md)|显示寄存器列表。|
|[列出源](../../ide/reference/list-source-command.md)|显示源代码的指定行。|
|[列出线程](../../ide/reference/list-threads-command.md)|显示当前程序中线程的列表。|
|[日志命令窗口输出](../../ide/reference/log-command-window-output-command.md)|将命令窗口的所有输入和输出复制到文件中。|
|[新建文件](../../ide/reference/new-file-command.md)|创建新文件并将其添加到当前选定的项目中。|
|[打开文件](../../ide/reference/open-file-command.md)|打开现有文件，并允许指定编辑器。|
|[打开项目](../../ide/reference/open-project-command.md)|打开现有项目，并允许将该项目添加到当前解决方案中。|
|[打开解决方案](../../ide/reference/open-solution-command.md)|打开现有解决方案。|
|[打印](../../ide/reference/print-command.md)|计算表达式并显示结果或指定的文本。|
|[“快速监视”命令](../../ide/reference/quick-watch-command.md)|在“快速监视”  对话框的“表达式”  字段中显示选定或指定的文本。|
|[替换](../../ide/reference/replace-command.md)|使用“查找和替换”  控件上可用的选项子集替换文件中的文本。|
|[在文件中替换](../../ide/reference/replace-in-files-command.md)|使用 [在文件中替换](../../ide/replace-in-files.md)。|
|[设置当前堆栈帧](../../ide/reference/set-current-stack-frame-command.md)|允许查看特定的堆栈帧。|
|[设置当前线程](../../ide/reference/set-current-thread-command.md)|允许查看特定的线程。|
|[设置基数](../../ide/reference/set-radix-command.md)|确定要查看的字节数。|
|[shell](../../ide/reference/shell-command.md)|从 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 内部启动程序，就像已从命令提示符处执行过此命令一样。|
|[ShowWebBrowser 命令](../../ide/reference/showwebbrowser-command.md)|在集成开发环境 (IDE) 中或 IDE 外部显示在 Web 浏览器窗口中指定的 URL。|
|[Start](../../ide/reference/start-command.md)|开始调试进程，并允许指定如何处理错误。|
|[路径](../../ide/reference/symbol-path-command.md)|设置调试器的目录列表，以搜索符号。|
|[切换断点](../../ide/reference/toggle-breakpoint-command.md)|在文件中的当前位置，根据其当前状态打开或关闭断点。|
|[“监视”命令](../../ide/reference/watch-command.md)|创建并打开指定“监视”  窗口的实例。|

## <a name="see-also"></a>请参阅
 [命令窗口](../../ide/reference/command-window.md)[查找/命令框](../../ide/find-command-box.md) [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
