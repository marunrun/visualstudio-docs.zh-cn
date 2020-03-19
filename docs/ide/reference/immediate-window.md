---
title: 即时窗口
ms.date: 02/25/2019
ms.topic: reference
dev_langs:
- VB
f1_keywords:
- VS.ImmediateWindow
helpviewer_keywords:
- design-time expression evaluation
- Immediate window
- first-chance exception notifications
ms.assetid: d33e7937-73f3-4c69-9df0-777a8713c6f2
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b21cdb9136abe1e960e5b74bbf09e7d1694519d7
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75568953"
---
# <a name="immediate-window"></a>即时窗口

使用“即时”窗口调试和计算表达式、执行语句、输出变量值  。 “即时”窗口通过生成和使用当前选定的项目来计算表达式  。

要显示“即时”窗口，请打开要编辑的项目，然后从“调试” > “窗口” > “即时”，或按 Ctrl+Alt+I        。 还可以在“命令”窗口中输入“Debug.Immediate”   。

“即时”窗口支持 IntelliSense  。

## <a name="display-the-values-of-variables"></a>显示变量的值

在调试应用时，“即时”窗口特别有用  。 例如，要检查变量 `varA` 的值，可使用 [Print 命令](../../ide/reference/print-command.md)：

```cmd
>Debug.Print varA
```

问号 (?) 是 `Debug.Print` 的别名，所以此命令也可写为：

```cmd
? varA
```

此命令的两个版本都返回变量 `varA` 的值。

> [!TIP]
> 要在“即时”窗口中发出 Visual Studio 命令，必须在命令的开头加上大于符号 (>)  。 要输入多个命令，请切换到[命令窗口](command-window.md)。

## <a name="design-time-expression-evaluation"></a>设计时表达式计算

用户可在设计时使用**即时**窗口执行函数或子例程。

### <a name="execute-a-function-at-design-time"></a>在设计时执行函数

1. 将下面的代码复制到 Visual Basic 控制台应用中：

   ```vb
   Module Module1

       Sub Main()
           MyFunction(5)
       End Sub

       Function MyFunction(ByVal input as Integer) As Integer
           Return input * 2
       End Function

   End Module
   ```

2. 在“调试”菜单上，选择“Windows” > “即时”    。

3. 在“即时”窗口中键入 `?MyFunction(2)`，然后按 Enter   。

    “即时”窗口将运行 `MyFunction` 并显示 `4`  。

如果函数或子例程包含断点，则 Visual Studio 会在适当断点处中断执行。 随后即可使用调试器窗口检查程序状态。 有关详细信息，请参见[演练：在设计时调试](../../debugger/walkthrough-debugging-at-design-time.md)。

不能在需要启动执行环境的项目类型（包括 Visual Studio Tools for Office 项目、Web 项目、智能设备项目和 SQL 项目）中使用设计时表达式计算。

### <a name="design-time-expression-evaluation-in-multi-project-solutions"></a>多项目解决方案中的设计时表达式计算

在为设计时表达式计算建立上下文时，Visual Studio 引用解决方案资源管理器中当前选择的项目。 如果没有在解决方案资源管理器中选择项目，则 Visual Studio 会尝试针对启动项目计算函数。 如果不能在当前上下文中计算函数，用户将收到错误消息。 如果尝试在不是解决方案的启动项目的项目中计算函数并收到错误，请在解决方案资源管理器中选择该项目，然后重新尝试计算。

## <a name="enter-commands"></a>输入命令

在“即时”窗口中发出 Visual Studio 命令时，必须输入大于符号 (>)  。 使用“向上键”和“向下键”可滚动显示以前用过的命令   。

|任务|解决方案|示例|
|----------|--------------|-------------|
|计算表达式的值。|表达式以问号 (?) 开头。|`? a+b`|
|在“即时”模式下临时进入“命令”模式（以执行单个命令）。|输入命令，在命令前面加一个大于号 (>)。|`>alias`|
|切换到“命令”窗口。|在窗口中输入 `cmd`，并在命令前面加一个大于号 (>)。|`>cmd`|
|切换回“即时”窗口。|在窗口中输入 `immed`，不带大于号 (>)。|`immed`|

## <a name="mark-mode"></a>标记模式

如果在**即时**窗口中单击前面的任意行，将自动切换到“标记”模式。 这允许你像在任何文本编辑器中那样选择、编辑和复制以前命令的文本，并将其粘贴到当前行中。

## <a name="examples"></a>示例

以下示例在 Visual Basic 项目的“即时”窗口中显示了四个表达式及其结果  。

```cmd
j = 2
Expression has been evaluated and has no value

? j
2

j = DateTime.Now.Day
Expression has been evaluated and has no value

? j
26
```

## <a name="first-chance-exception-notifications"></a>及早异常通知

在某些设置配置中，首次异常通知在**即时**窗口中显示。

### <a name="toggle-first-chance-exception-notifications-in-the-immediate-window"></a>在“即时”窗口中切换及早异常通知

1. 在“视图”  菜单上单击“其他窗口”  ，然后单击“输出”  。

2. 右键单击“输出”窗口的文本区域，然后选择或取消选择“异常消息”   。

## <a name="see-also"></a>请参阅

- [使用调试器浏览代码](../../debugger/navigating-through-code-with-the-debugger.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [初探调试器](../../debugger/debugger-feature-tour.md)
- [演练：在设计时调试](../../debugger/walkthrough-debugging-at-design-time.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
- [在 Visual Studio 中使用正则表达式](../../ide/using-regular-expressions-in-visual-studio.md)
