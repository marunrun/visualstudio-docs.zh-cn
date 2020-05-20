---
title: “命令”窗口
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.CommandWindow
helpviewer_keywords:
- IDE, Command window
- Mark mode in Command window
- Command window
- Command mode in Command window
- IDE Command window
ms.assetid: 48711628-1909-4713-a73e-d7b714c77f8a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cb855cbed67bffc5ff2fb63b1785c577dd9fea25
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75570344"
---
# <a name="command-window"></a>“命令”窗口
“命令”窗口用于直接在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境 (IDE) 中执行命令或别名。 可以执行菜单命令和不在任何菜单上出现的命令。 若要显示“命令”窗口，请在“视图”菜单中选择“其他窗口”，然后选择“命令窗口”     。

## <a name="displaying-the-values-of-variables"></a>显示变量的值
若要检查变量 `varA` 的值，请使用 [Print 命令](../../ide/reference/print-command.md)：

```cmd
>Debug.Print varA
```

问号 (?) 是 `Debug.Print` 的别名，所以此命令也可写为：

```cmd
>? varA
```

此命令的这两个版本都将返回变量 `varA` 的值。

## <a name="entering-commands"></a>输入命令
大于号 (`>`) 作为新行提示符出现在“命令”窗口的左边缘。 使用向上键和向下键可滚动显示以前发出的命令。

|任务|解决方案|示例|
|----------|--------------|-------------|
|计算表达式的值。|表达式以问号 (`?`) 开头。|`? myvar`|
|切换到“即时”窗口。|在窗口中输入 `immed`，而不输入大于号 (>)|`immed`|
|从“即时”窗口切换回“命令”窗口。|在窗口中输入 `cmd`。|`>cmd`|

以下快捷键有助于在命令模式中进行导航。

|操作|光标位置|键绑定|
|------------| - |----------------|
|循环通过以前输入的命令的列表。|输入行|向上键 & 向下键|
|向上滚动窗口。|“命令”窗口内容|Ctrl+向上键|
|向下滚动窗口。|“命令”窗口内容|向下键或 Ctrl+向下键|

> [!TIP]
> 通过滚动到前一个命令，突出显示该命令的全部或部分内容，然后按 Enter，可以将该命令的全部或部分内容复制到输入行中。

## <a name="mark-mode"></a>标记模式
在“命令”窗口中单击前面的任何行时，将自动切换到“标记”模式  。 这允许你像在任何文本编辑器中那样选择、编辑和复制以前命令的文本，并将其粘贴到当前行中。

## <a name="the-equals--sign"></a>等号 (=)
用于输入 `EvaluateStatement` 命令的窗口确定是将等号 (=) 解释为比较运算符还是赋值运算符。

在“命令”窗口中，将等号 (=) 解释为比较运算符  。 不可以在“命令”窗口中使用赋值运算符  。 例如，如果变量 `varA` 和 `varB` 的值不同，则命令 `>Debug.EvaluateStatement(varA=varB)` 返回 `False` 值。

与此相反，在“即时”窗口中，将等号 (=) 解释为赋值运算符  。 例如，命令 `>Debug.EvaluateStatement(varA=varB)` 将变量 `varB` 的值赋给变量 `varA`。

## <a name="parameters-switches-and-values"></a>参数、开关和值
某些 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 命令具有必选和可选的参数、开关和值。 处理此类命令时，会应用某些规则。 下面是一个用来阐明术语的复杂命令示例。

```cmd
Edit.ReplaceInFiles /case /pattern:regex var[1-3]+ oldpar
```

在此示例中，

- `Edit.ReplaceInFiles` 是命令

- `/case` 和 `/pattern:regex` 是开关（以斜杠 [/] 字符开头）

- `regex` 是 `/pattern` 开关的值；`/case` 开关没有值

- `var[1-3]+` 和 `oldpar` 是参数

    > [!NOTE]
    > 任何包含空格的命令、参数、开关或值都必须用双引号引起来。

在命令行上，开关和参数的位置可以随便互换，但 [Shell](../../ide/reference/shell-command.md) 命令是个例外，它要求开关和参数按特定的顺序出现。

几乎命令所支持的每个开关都有两种格式：短格式（一个字符）和长格式。 多个短格式开关可组合为一组。 例如，`/p /g /m` 可表示为 `/pgm`。

如果短格式开关组合为一组，而且给定一个值，则该值应用于每个开关。 例如，`/pgm:123` 等同于 `/p:123 /g:123 /m:123`。 如果该组中的任何开关都不接受值，则发生错误。

## <a name="escape-characters"></a>转义字符
命令行中的插入符号 (^) 字符表示紧随其后的字符将按字面意思而不是作为控制字符进行解释。 这可以用于嵌入参数或开关值中的直引号 (")、空格、前导斜杠，插入符号或其他任何字符，开关名称除外。 例如，应用于对象的

```cmd
>Edit.Find ^^t /regex
```

插入符号在引号内或引号外的作用相同。 如果插入符号是行的最后一个字符，则忽略不计。 此处显示的示例演示如何搜索模式“^t”。

## <a name="use-quotes-for-path-names-with-spaces"></a>对带有空格的路径名称使用引号
例如，如果要打开的文件的路径中含有空格，必须在包含空格的路径或路径段两边添加双引号：C:\\"Program Files" 或 "C:\Program Files"。

## <a name="see-also"></a>另请参阅

- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
