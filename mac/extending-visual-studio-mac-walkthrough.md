---
title: 扩展 Visual Studio for Mac 演练
author: conceptdev
ms.author: crdun
ms.date: 04/14/2017
ms.technology: vs-ide-sdk
ms.assetid: 7D00512B-9688-4D8D-87A7-F04F207E3D02
ms.openlocfilehash: cbf0d99bd87b31484b6c74e9a6d67ac88dc5ba99
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62984104"
---
# <a name="extending-visual-studio-for-mac-walkthrough"></a>扩展 Visual Studio for Mac 演练

本主题介绍如何生成[一个简单的扩展包](https://github.com/mjh4/AddIns/tree/master/DateInserter)。 扩展包将在 Visual Studio for Mac 的“编辑”菜单中创建新命令，用户通过该命令可以将当前的日期和时间插入到打开的文本文档中。

该示例使用 Add-in Maker。 Add-in Maker 创建新项目模板，并用自定义扩展包所需的文件填充该模板。

1. 如果尚未打开 Visual Studio for Mac，请启动它来开始操作：

   ![Visual Studio for Mac 屏幕截图](media/extending-visual-studio-mac-addin3.png)

2. 使用扩展管理器安装 Add-in Maker 扩展包。 从 Visual Studio 菜单，选择“扩展...”：

   ![加载项管理器选项卡](media/extending-visual-studio-mac-addin4.png)

3. 导航到“库”选项卡，在右上角的搜索栏中键入 `Addin Maker`。 从“加载项开发”类别中选择 Addin Maker，然后单击<kbd>安装</kbd>。 如果未显示任何内容，请点击“刷新”并再次搜索：

   ![加载项管理器](media/extending-visual-studio-mac-addin5.png)

4. 安装 Addin Maker 后，便可开始生成扩展包。 首先创建新的解决方案。

5. 从“新解决方案对话框”中，选择“其他”>“杂项”>“常规”>“Xamarin Studio 加载项”>“C#”模板，在接下来出现的屏幕中将新解决方案命名为 `DateInserter`：

   ![创建新解决方案](media/extending-visual-studio-mac-addin7New.png)

6. Visual Studio for Mac 将填充新解决方案：

   ![完成填充的解决方案](media/extending-visual-studio-mac-addin8.png)

7. 删除 `Manifest.addin.xml` 中的模板代码并替换为以下代码：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
      <ExtensionModel>
          <Extension path = "/MonoDevelop/Ide/Commands/Edit">
              <Command id = "DateInserter.DateInserterCommands.InsertDate"
                  _label = "Insert Date"
                  defaultHandler = "DateInserter.InsertDateHandler" />
          </Extension>

          <Extension path = "/MonoDevelop/Ide/MainMenu/Edit">
              <CommandItem id="DateInserter.DateInserterCommands.InsertDate" />
          </Extension>
      </ExtensionModel>
   ```

8. 现在需要设置文件，用于最终把日期和时间插入到文本编辑器中。 右键单击项目节点，然后添加新文件。 选择“常规”>“空类”，然后将新文件命名为“InsertDateHandler”：

   ![插入日期处理程序](media/extending-visual-studio-mac-addin9.png)

9. 请删除 `InsertDateHandler.cs` 中的模板代码并替换为以下代码：

   ```cs
   using MonoDevelop.Components.Commands;
   using MonoDevelop.Ide;
   using MonoDevelop.Ide.Gui;
   using System;

   namespace DateInserter
   {
      class InsertDateHandler : CommandHandler
      {
          protected override void Run()
          {

          }

          protected override void Update(CommandInfo info)
          {

          }
      }
   }
   ```

   我们将稍后详细介绍这两种占位符方法。

10. 右键单击“DateInserter”项目并选择“添加”>“新文件”。 选择“常规”>“空枚举”，然后将新文件命名为“DateInserterCommands”：

    ![DateInserterCommands](media/extending-visual-studio-mac-addin10.png)

11. 将 `InsertDate` 命令作为新枚举添加到 `DateInserterCommands.cs` 文件：

    ``` cs
    using System;

    namespace DateInserter
    {
      public enum DateInserterCommands
      {
          InsertDate,
      }
    }
    ```

12. 此时，应具有一个正在工作的扩展包。 保存工作并运行应用程序，对其进行测试。 IDE 将启动已安装新扩展包的 Visual Studio for Mac 新实例。 如果导航到“编辑”菜单，会看到 Visual Studio for Mac 具有一个名为“插入日期”的新选项，如下方的屏幕截图所示：

    ![插入日期命令](media/extending-visual-studio-mac-addin11.png)

    请注意，从菜单选择“插入日期”不会产生任何效果，因为当前实现只有占位符方法。

13. 框架已放置在可供扩展包使用的合适位置，可以开始写入实现插入日期的代码。 首先，请确保仅当用户使用以下代码替换 `InsertDateHandler.cs` 中的 `Update` 方法来打开文本文件时，才启用“插入日期命令”：

    ```cs
    protected override void Update(CommandInfo info)
    {
      info.Enabled = IdeApp.Workbench.ActiveDocument?.Editor != null;
    }
    ```

14. 更新该命令的 `Run` 方法，以便使用以下代码插入日期和时间：

    ``` cs
    protected override void Run () {
      var editor = IdeApp.Workbench.ActiveDocument.Editor;
      var date = DateTime.Now.ToString ();
      editor.InsertAtCaret (date);

    }
    ```

15. 最后，请运行扩展包以进行测试。 在 Visual Studio for Mac 新实例中，选择“编辑”>“插入日期”。 在脱字号处插入当前的日期和时间，如下方的屏幕截图所示：

    ![插入日期屏幕截图](media/extending-visual-studio-mac-addin12.png)

## <a name="see-also"></a>请参阅

- [创建你的首个扩展（Windows 上的 Visual Studio）](/visualstudio/extensibility/extensibility-hello-world)