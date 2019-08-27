---
title: 调试 Web 窗体 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Web pages [.NET Framework], debugging
- Web sites [.NET Framework], debugging
- ASP.NET, debugging Web applications
- Web applications [.NET Framework], debugging
- ASP.NET Web sites, debugging
- ASP.NET Web pages, debugging
- debugging ASP.NET Web applications, Web Forms
- debugging [Visual Studio], Web Forms
ms.assetid: e2b4fa14-8f5b-444d-a903-54070b784bd4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f884206ecafebbe26bfdadfaa7e95f3dbd0f389f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901552"
---
# <a name="walkthrough-debugging-a-web-form"></a>演练：调试 Web 窗体
本演练中的步骤向你演示如何调试 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序（也称为 Web 窗体）。 此外，还会演示如何启动和停止执行、设置断点以及在“监视”窗口中检查变量。

> [!NOTE]
> 若要完成本演练，您必须在服务器计算机上具有管理员特权。 默认情况下，[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 进程（aspnet_wp.exe 或 w3wp.exe）作为 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 进程运行。 若要调试 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]，您必须在运行 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 的计算机上拥有管理员特权。 有关详细信息，请参阅 [System Requirements](../debugger/aspnet-debugging-system-requirements.md)。

显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你的当前设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

## <a name="to-create-the-web-form"></a>创建 Web 窗体

1. 如果您已经打开了一个解决方案，请先关闭它。

2. 在“文件”菜单上单击“新建”，然后单击“网站”。

    “新建网站”对话框随即出现。

3. 在“模板”窗格中，单击“ASP.NET 网站”。

4. 上**位置**行，单击**HTTP**从列表中，并在文本框中，键入**http://localhost/WebSite**。

5. 在“语言”列表中，单击“Visual C#”或“Visual Basic”。

6. 单击 **“确定”**。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将创建一个新项目并显示默认的 HTML 源代码。 它还将在 IIS 中的“默认网站”下面创建一个名为“网站”的新虚拟目录。

7. 单击底部边距上的“设计”选项卡。

8. 单击左边距上的“工具箱”选项卡，或在“视图”菜单上选择“工具箱”。

    将打开 **“工具箱”** 。

9. 在“工具箱”中单击“Button”控件，并将其添加到主设计图面 (Default.aspx) 上。

10. 在“工具箱”中，单击“Textbox”控件，并将该控件拖到主设计图面 (Default.aspx) 上。

11. 双击所放置的按钮 (Button) 控件。

     这会转到代码页：为 Default.aspx.csC#或为 Default.aspx.vb [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]。 光标应位于函数 `Button1_Click` 中。

12. 在 `Button1_Click` 函数中，添加以下代码：

    ```vb
    TextBox1.Text = "Button was clicked!"
    ```

    ```csharp
    TextBox1.Text = "Button was clicked!";
    ```

13. 在 **“生成”** 菜单上，单击 **“生成解决方案”**。

     该项目应顺利生成，没有错误。

     现在，您可以开始调试了。

## <a name="to-debug-the-web-form"></a>调试 Web 窗体

1. 在 Default.aspx.cs 或 Default.aspx.vb 窗口中，单击所添加文本的同一行的左侧空白：

   ```vb
   TextBox1.Text = "Button was clicked!"
   ```

   ```csharp
   textBox1.Text = "Button was clicked!";
   ```

    出现一个红点并且该行上的文本突出显示为红色。 红点表示一个断点。 当您在调试器下运行该应用程序时，此调试器将在命中该代码时在该位置中断执行。 然后您可以查看应用程序的状态并调试它。 有关详细信息，请参见[断点](https://msdn.microsoft.com/library/fe4eedc1-71aa-4928-962f-0912c334d583)

2. 在“调试”菜单上，单击“启动调试”。

3. 随即会显示“未启用调试”对话框。 选择“修改 Web.config 文件以启用调试”选项，再单击“确定”。

    Internet Explorer 即启动并显示您刚设计的页。

4. 在 Internet Explorer 中，单击此按钮。

    在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中，此操作将带你转到代码页 Default.aspx.cs 或 Default.aspx.vb 上设置了断点的行上。 该行将用黄色突出显示。 现在，可以查看应用程序中的变量并控制其执行。 应用程序停止执行并等待您的命令。

5. 在“调试”菜单上，单击“窗口”，再单击“监视”，然后单击“Watch1”。

6. 在“监视”窗口中，键入“TextBox1.Text”。

    “监视”窗口将显示变量 `TextBox1.Text` 的值：

   '""'

7. 在“调试”菜单上，单击“逐过程”。

    `TextBox1.Text` 的值在“监视”窗口中更改为：

   `"Button was clicked!"`

8. 在“调试”菜单上，单击“继续”。

9. 在 Internet Explorer 中，再次单击此按钮。

     执行再次在断点处停止。

10. 在 Default.aspx.cs 或 Default.aspx.vb 窗口中，单击左空白中的红点。

     这将移除该断点。

11. 在“调试”菜单上，单击“停止调试”。

## <a name="to-attach-to-the-web-form-for-debugging"></a>附加到 Web 窗体以进行调试

1. 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中，可以将调试器附加到正在运行的进程上。 若要获得最佳调试效果，请将可执行文件编译为符号 (PDB) 文件的调试版本。

2. 在 Default.aspx.cs 或 Default.aspx.vb 窗口中，在左边距中单击以再次在所添加的行上设置断点：

   ```vb
   TextBox1.Text = "Button was clicked!"
   ```

   ```csharp
   textBox1.Text = "Button was clicked!";
   ```

3. 在“调试”菜单上，单击“开始执行(不调试)”。

    Web 窗体将开始在 Internet Explorer 下运行，但未附加调试器。

4. 附加到 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 进程。 有关详细信息，请参阅[调试部署 Web 应用程序](../debugger/debugging-deployed-web-applications.md)。

5. 在 Internet Explorer 中，单击窗体上的按钮。

    在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中，应当命中 Default.aspx.cs、Default.aspx.vb 或 Default.aspx 中的断点。

6. 完成调试后，在“调试”菜单上，单击“停止调试”。

## <a name="see-also"></a>请参阅

- [调试 ASP.NET 应用程序](../debugger/how-to-enable-debugging-for-aspnet-applications.md)