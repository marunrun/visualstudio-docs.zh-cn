---
title: 使用 UI 自动化来测试代码 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
f1_keywords:
- vs.codedUITest
- vs.codedUITest.recorder
- vs.codedUITest.testbuilder
- vs.codedUITest.addAssertions
- vs.codedUITest.createdialog
helpviewer_keywords:
- automated tests, testing UI interface
- coded UI test
ms.assetid: ad9e3eaa-ab86-436e-95b8-dc20eb1f8b2a
caps.latest.revision: 87
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 54a050fc6d9d585be2613a27ca177dc77af61121
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68871638"
---
# <a name="use-ui-automation-to-test-your-code"></a>使用 UI 自动化来测试代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过应用程序的用户界面 (UI) 来操作该应用程序的自动测试称为编码的 UI 测试 (CUIT)。 这些测试包括对 UI 控件的功能测试。 它们使你可以验证整个应用程序（包括其用户界面）是否正常运行。 编码的 UI 测试对于在用户界面中存在验证或其他逻辑（例如在网页中）的情况特别有用。 它们也经常用于自动化现有的手动测试。

 如下图所示，一种典型的开发体验可能是这样一种情况：最初，你只需建立自己的应用程序（F5），并通过单击 UI 控件来验证一切是否运行正常。 你可能会决定创建一个编码的测试，这样就不需要继续手动测试应用程序。 根据在应用程序中进行测试的特定功能，你可以针对任何一个功能测试或者针对可能会或可能不会包括 UI 级别测试的集成测试编写代码。 如果你只想直接访问某些业务逻辑，则可以编写单元测试代码。 然而，在特定情况下，在应用程序中包括各种 UI 控件的测试将是有益的。 编码的 UI 测试可以自动化初始 (F5) 方案，以便验证代码改动不会影响你的应用程序的功能。

 ![在应用程序开发过程中进行测试](../test/media/cuit-overview.png "CUIT_Overview")

 创建编码的 UI 测试很容易。 当 CUIT 测试生成器在后台运行时，你只需手动执行该测试。 你还可以指定在特定字段中应显示哪些值。 CUIT 测试生成器录制操作并且从中生成代码。 在创建测试后，你可以在专用编辑器中对其进行编辑，该编辑器使你能够修改操作的序列。

 或者，如果你具有在 Microsoft 测试管理器中录制的测试用例，你可以从中生成代码。 有关详细信息，请参阅[录制和播放手动测试](/azure/devops/test/mtm/record-play-back-manual-tests)。

 专用的 CUIT 测试生成器和编辑器可以方便地创建和编辑编码的 UI 测试，即使你的主要技能都集中于测试而不是编码。 但如果你是一位开发人员，想要以更先进的方式扩展测试，则结构化代码，以便于更简单地复制和改写。 例如，你可以录制在网站购物的测试，然后编辑生成的代码以添加购买许多商品的循环。

 **要求**

- Visual Studio Enterprise

  有关编码的 UI 测试支持哪些平台和配置的详细信息，请参阅[支持编码的 UI 测试和操作录制的配置和平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)。

  **在本主题中**

- [创建编码的 UI 测试](#VerifyingCodeUsingCUITCreate)

  - [主要过程](#VerifyingCodeUsingCUITCreate)

  - [启动和停止应用程序](#starting)

  - [验证 UI 控件的属性](#VerifyingCodeUsingCUITGenerateAssertions)

- [自定义编码的 UI 测试](#VerifyingCodeCUITModify)

  - [生成的代码](#generatedCode)

  - [编码 UI 控件操作和属性](#actions)

  - [调试](#debugging)

- [后续步骤](#VerifyCodeUsingCUITWhatsNext)

## <a name="VerifyingCodeUsingCUITCreate"></a> 创建编码的 UI 测试

1. **创建编码的 UI 测试项目。**

    编码的 UI 测试必须包含在编码的 UI 测试项目中。 如果你还没有编码的 UI 测试项目，则创建一个。 在“解决方案资源管理器”中，在该解决方案的快捷菜单上，依次选择“添加”、“新建项目”，然后选择“Visual Basic”或“Visual C#”。 接下来，依次选择“测试”、“编码的 UI 测试”。

   - <em>我没有看到 **“编码的 UI 测试”</em>* 项目模板。*

      你使用的 Visual Studio 版本可能不支持编码的 UI 测试。 若要创建编码的 UI 测试，你必须使用 Visual Studio Enterprise。

2. **添加编码的 UI 测试文件。**

    如果你刚创建了编码的 UI 项目，则自动添加第一个 CUIT 文件。 若要添加另一个测试文件，则打开编码的 UI 测试项目上的快捷菜单，指向“添加”，然后选择“编码的 UI 测试”。

    ![创建编码的 UI 测试](../test/media/codedui-create.png "CodedUI_Create")

    在“为编码的 UI 测试生成代码”对话框中，选择“录制操作、编辑 UI 映射或添加断言”。

    ![选择记录操作](../test/media/codedui-codegendialogb.png "CodedUI_CodeGenDialogB")

    显示“编码的 UI 测试生成器”并且 Visual Studio 将最小化。

    ![编码的 UI 测试生成器](../test/media/codedui-testbuilder.png "CodedUI_TestBuilder")

3. **录制一系列操作**。

    **若要开始录制**，请选择“录制”图标。 执行要在应用程序中测试的操作，必要时还包括启动应用程序。

    例如，如果测试一个 Web 应用程序，你可能会启动浏览器、导航到该网站，并登录到该应用程序。

    **若要暂停录制**（例如，如果你必须处理接收的邮件），请选择“暂停”。

   > [!WARNING]
   > 将录制在桌面上执行的所有操作。 如果你正在执行可能会导致敏感数据被包括在录制中的操作，则暂停录制。

    **若要删除错误录制的操作**，请选择“编辑操作”。

    **若要生成将复制你的操作的代码**，请选择“生成代码”图标并且键入编码的 UI 测试方法的名称和描述。

4. **验证 UI 字段（如文本框）中的值**。

    在编码的 UI 测试生成器中，选择“添加断言”，然后在你的运行的应用程序中选择 UI 控件。 在显示的属性列表中，选择属性，例如，在文本框中的“文本”。 在快捷菜单上，选择“添加断言”。 在对话框中，选择比较运算符、比较值以及错误消息。

    关闭断言窗口并且选择“生成代码”。

    ![编码的 UI 测试目标元素](../test/media/codedui-1.png "CodedUI_1")

   > [!TIP]
   > 在录制操作和验证值之间交替。 在每个操作或验证序列的结尾生成代码。 如果你愿意，可以随后插入新的操作和验证。

    有关详细信息，请参阅[验证控件的属性](#VerifyingCodeUsingCUITGenerateAssertions)。

5. **查看生成的测试代码**。

    若要查看生成的测试代码，请关闭 UI 测试生成器窗口。 在代码中，你可以看到你为每个步骤指定的名称。 此代码在你创建的 CUIT 文件中：

   ```csharp
   [CodedUITest]
   public class CodedUITest1
   { ...
     [TestMethod]
     public void CodedUITestMethod1()
     {
         this.UIMap.AddTwoNumbers();
         this.UIMap.VerifyResultValue();
         // To generate more code for this test, select
         // "Generate Code" from the shortcut menu.
     }
   }
   ```

6. **添加更多操作和断言**。

    将光标放置到测试方法中合适的点，然后在快捷菜单上，选择“为编码的 UI 测试生成代码”。 新的代码将会在该点插入。

7. **编辑测试操作和断言的详细信息**。

    打开 UIMap.uitest。 该文件在编码的 UI 测试编辑器中打开，其中你可以编辑你所录制的操作的任何序列，你还可以编辑断言。

    ![编码的 UI 测试编辑器](../test/media/cuit-editor-edit.png "CUIT_Editor_edit")

    有关详细信息，请参阅[使用编码的 UI 测试编辑器编辑编码的 UI 测试](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)。

8. **运行测试**。

    使用测试资源管理器，或打开测试方法中的快捷菜单，然后选择“运行测试”。 有关如何运行测试的详细信息，请参见本主题结尾处[后续步骤](#VerifyCodeUsingCUITWhatsNext)部分中的[用测试资源管理器运行单元测试](../test/run-unit-tests-with-test-explorer.md)和*运行编码的 UI 测试的其他选项*。

   本主题中的剩余部分提供了有关此过程中步骤的更多详细信息。

   有关更详细的示例，请参阅[演练：创建、编辑和维护已编码 UI 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)。 在该演练中，你将创建一个简单的 Windows Presentation Foundation (WPF) 应用程序来演示如何创建、编辑和维护编码的 UI 测试。 本演练为更正由各种计时问题和控件重构中断的测试提供了解决方案。

### <a name="starting"></a> 启动和停止受测应用程序
 *我不想针对每个测试分别启动和停止应用程序、浏览器或数据库。如何避免该操作?*

- ![先决条件](../test/media/prereq.png "Prereq") 如果不希望录制启动受测应用程序的操作，则必须在选择“录制”图标之前启动应用程序。

- ![先决条件](../test/media/prereq.png "Prereq")在测试的结尾，在其中运行测试的进程将终止。 如果你在测试中启动应用程序，该应用程序通常会关闭。  如果你不希望测试退出时关闭应用程序，则必须将一个 .runsettings 文件添加到你的解决方案并且使用 `KeepExecutorAliveAfterLegacyRun` 选项。 有关详细信息，请参阅[使用 .runsettings 文件配置单元测试](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)。

- ![先决条件](../test/media/prereq.png "Prereq") 可以添加一个在每个测试方法开始时运行代码的测试初始化方法（通过 [TestInitialize] 属性标识）。 例如，你可以从 TestInitialize 方法启动应用程序。

- ![先决条件](../test/media/prereq.png "Prereq") 可以添加一个在每个测试方法结束时运行代码的测试清理方法（通过 [TestCleanup] 属性标识）。 例如，可以从 TestCleanup 方法调用用于关闭应用程序的方法。

### <a name="VerifyingCodeUsingCUITGenerateAssertions"></a> 验证 UI 控件的属性
 您可以使用**编码的 UI 测试生成器**将用户界面 (UI) 控件添加到您的测试的[UIMap](/previous-versions/dd580454(v=vs.140)) , 或者为使用 UI 控件断言的验证方法生成代码。

 若要为 UI 控件生成断言，请选择编码的 UI 测试生成器中的“添加断言”工具，并且将其拖放到受测应用程序上的控件，因为你希望验证该应用程序是否正确。 在框确定控件的轮廓时，释放鼠标。 将立即在 `UIMap.Designer.cs` 文件中创建该控件类代码。

 ![编码的 UI 测试目标元素](../test/media/codedui-1.png "CodedUI_1")

 此时，该控件的属性在“添加断言”对话框中列出。

 另一种导航到特定控件的方法是选择箭头“(<<)”以展开“UI 控件映射”的视图。 若要查找父控件、同级控件或子控件，可以在映射中的任何位置单击，然后使用箭头键在树中移动。

 ![编码的 UI 测试属性](../test/media/codedui-2.png "CodedUI_2")

- *当我在应用程序中选择控件时，我看不到任何属性，或者我看不到 UI 控件映射中的控件。*

   在应用程序代码中，你想要验证的控件必须具有唯一 ID，如 HTML ID 特性或 WPF UId。 你可能需要更新应用程序代码以添加这些 ID。

  接下来，打开要验证的 UI 控件的属性上的快捷菜单，然后指向“添加断言”。 在“添加断言”对话框中，选择断言的“比较器”（例如，<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A>），并且在“比较值”中键入断言的值。

  ![编码的 UI 测试断言](../test/media/codedui-3.png "CodedUI_3")

  在你为测试添加了所有断言后，选择“确定”。

  若要为断言生成代码并将控件添加到 UI 映射中，请选择“生成代码”图标。 请为你的编码的 UI 测试方法键入名称以及该方法的描述，这将添加作为该方法的注释。 选择“添加并生成”。 接下来，选择“关闭”图标以关闭“编码的 UI 测试生成器”。 这会生成类似于以下代码的代码。 例如，如果你输入的名称为 `AssertForAddTwoNumbers`，代码将类似于此示例：

- 向编码的 UI 测试文件中的测试方法添加对断言方法 AssertForAddTwoNumbers 的调用：

  ```
  [TestMethod]
  public void CodedUITestMethod1()
  {
      this.UIMap.AddTwoNumbers();
      this.UIMap.AssertForAddTwoNumbers();
  }
  ```

   你可以编辑此文件以更改步骤和断言的顺序，或创建新测试方法。 若要添加更多代码，请将光标放在测试方法上并且在快捷菜单上选择“为编码的 UI 测试生成代码”。

- 将名为 `AssertForAddTwoNumbers` 的方法添加到你的 UI 映射 (UIMap.uitest)。 此文件在编码的 UI 测试编辑器中打开，其中你可以编辑断言。

   ![使用编码的 UI 测试编辑器编辑断言](../test/media/cuit-editor-assert.png "CUIT_Editor_assert")

   有关详细信息，请参阅[使用编码的 UI 测试编辑器编辑编码的 UI 测试](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)。

   你还可以在 UIMap.Designer.cs 中查看断言方法的生成代码。 但是，不应编辑此文件。 如果你想要制作代码的改编版，则将方法复制到另一个文件，如 UIMap.cs，重命名方法，并在此处对它们进行编辑。

  ```
  public void AssertForAddTwoNumbers()
  {
      ...
  }
  ```

  *当我尝试从编码的 UI 测试生成器选中“添加断言”工具时，我想要选择的控件失去焦点并且消失。如何实现选择控件吗？使用键盘**选择隐藏控件** * 
  

  有时候，当[添加控件并验证它们的属性](#VerifyingCodeUsingCUITGenerateAssertions)时，你可能必须使用键盘。 例如，当你尝试录制使用上下文菜单控件的编码的 UI 测试时，如果你尝试从编码的 UI 测试生成器选择“添加断言”工具，则在该控件中的菜单项列表会失去焦点并消失。 下图说明了这一点，如果你尝试使用“添加断言”工具选择上下文菜单，其中 Internet Explorer 中的上下文菜单将会失去焦点并且消失。

  ![CodedUITest&#95;SelectControlKeyboard](../test/media/codeduitest-selectcontrolkeyboard.png "CodedUITest_SelectControlKeyboard")

  若要使用键盘选择 UI 控件，请使用鼠标悬停在该控件上。 然后，同时按住“Ctrl”键和“I”键。 释放这些键。 此控件由编码的 UT 测试生成器录制。

> [!WARNING]
> 如果你使用 Microsoft Lync，必须在启动编码的 UI 测试生成器前关闭 Lync。 Microsoft Lync 会影响“Ctrl+I”键盘快捷方式。

 *我无法录制控件上的鼠标悬停。是否有解决此问题的方法？*
 **手动录制鼠标悬停**

 某些情况下，在编码的 UI 测试中使用的特定控件可能需要你使用键盘来手动记录鼠标悬停事件。 例如，当你测试 Windows 窗体或 Windows Presentation Foundation (WPF) 应用程序时，可能是自定义代码。 或者，可能是针对悬停控件所定义的特殊行为，如当用户在树节点上悬停时，树节点会展开。 若要测试类似这样的情况，你必须通过按下预定义的键盘按键，手动通知编码的 UI 测试生成器你正在控件上悬停。

 当你执行编码的 UI 测试时，在该控件上悬停。 当你在键盘上按住 Shift 和 R 键时，同时按住 Ctrl 键。 释放这些键。 鼠标悬停事件由编码的 UT 测试生成器录制。

 ![CodedUI&#95;Hover](../test/media/codedui-hover.png "CodedUI_Hover")

 在你生成测试方法后，会将类似于以下示例的代码添加到 UIMap.Desinger.cs 文件：

```csharp
// Mouse hover '1' label at (87, 9)
Mouse.Hover(uIItem1Text, new Point(87, 9));

```

 *捕获鼠标悬停事件的键分配已用在我环境中的其他位置。我是否能够更改默认的键分配？*
 **配置鼠标悬停键盘分配**

 如有必要，用于在编码的 UI 测试中应用鼠标悬停事件的默认 Ctrl+Shift+R 键盘分配可以配置为使用不同的键。

> [!WARNING]
> 一般情况下，不必更改鼠标悬停事件的键盘分配。 在重新分配键盘分配时，请谨慎从事。 你的选择可能已用在 Visual Studio 内或测试的应用程序中的其他位置。

 若要更改键盘分配，你必须修改以下配置文件：

 `<drive letter:>\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\CodedUITestBuilder.exe.config`

 在配置文件中，更改 `HoverKeyModifier` 和 `HoverKey` 键的值以修改键盘分配：

```
<!-- Begin : Background Recorder Settings -->
<!-- HoverKey to use. -->
<add key="HoverKeyModifier" value="Control, Shift"/>
<add key="HoverKey" value="R"/>

```

 *在录制网站上的鼠标悬停时我遇到了一些问题。是否也存在对于此问题的修复？*
 **为 Web 浏览器设置隐式鼠标悬停**

 在很多网站中，当你在一个特定的控件上悬停时，它就会展开以显示更多细节。 通常，它们看起来像桌面应用程序中的菜单。 因为这是通用模式，因此编码的 UI 测试支持 Web 浏览的隐式悬停。 例如，如果你在 Internet Explorer 中录制悬停，会触发一个事件。 这些事件可能导致冗余悬停的录制。 因此，隐式悬停采用在 UI 测试配制文件中设置为 `ContinueOnError` 的 `true` 录制。 这可允许在悬停事件失败时，播放继续进行。

 若要在 Web 浏览器中启用隐式悬停的录制，请打开配制文件：

 `<drive letter:>\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\CodedUITestBuilder.exe.config`

 验证该配置文件是否具有设置为 `RecordImplicitiHovers` 值的 `true` 键，如以下示例所示：

```
<!--Use this to enable/disable recording of implicit hovers.-->
<add key="RecordImplicitHover" value="true"/>

```

## <a name="VerifyingCodeCUITModify"></a> 自定义编码的 UI 测试
 在创建编码的 UI 测试之后，你可以通过使用 Visual Studio 中的以下任何工具对其进行编辑：

- **编码的 UI 测试生成器:** 使用编码的 UI 测试生成器将其他控件和验证添加到测试中。 请参阅本主题中的[添加控件并验证它们的属性](#VerifyingCodeUsingCUITGenerateAssertions)部分。

- **编码的 UI 测试编辑器：** 通过编码的 UI 测试编辑器，可轻松修改编码的 UI 测试。 使用编码的 UI 测试编辑器，可以查找、查看和编辑测试方法。 也可以在 UI 控件映射中编辑 UI 操作及其关联的控件。 有关详细信息，请参阅[使用编码的 UI 测试编辑器编辑编码的 UI 测试](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)。

- **代码编辑器：**

  - 按照本主题中的[编码 UI 控件操作和属性](#actions)部分的描述，为测试中的控件手动添加代码。

  - 在创建编码的 UI 测试以后，你可以将其修改为数据驱动。 有关详细信息，请参阅[创建数据驱动的编码的 UI 测试](../test/creating-a-data-driven-coded-ui-test.md)。

  - 在编码的 UI 测试播放中，你可以指示测试等待某些事件发生，如某个窗口出现、进度栏消失等。 为此，请添加相应的 UITestControl.WaitForControlXXX() 方法。 有关可用方法的完整列表，请参阅[播放期间让编码的 UI 测试等待特定事件](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md)。 有关使用 WaitForControlEnabled 方法等待启用某个控件的编码的 UI 测试示例，请参阅[演练：创建、编辑和维护已编码 UI 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)。

  - 编码的 UI 测试包括对某些包含在 Internet Explorer 9 和 Internet Explorer 10 中的 HTML5 控件的支持。 有关详细信息，请参阅[在编码的 UI 测试中使用 HTML5 控件](../test/using-html5-controls-in-coded-ui-tests.md)。

  - **编码的 UI 测试编码指导：**

    - [编码的 UI 测试剖析](../test/anatomy-of-a-coded-ui-test.md)

    - [编码的 UI 测试的最佳做法](../test/best-practices-for-coded-ui-tests.md)

    - [使用多个 UI 映射测试大型应用程序](../test/testing-a-large-application-with-multiple-ui-maps.md)

    - [支持编码的 UI 测试和操作录制的配置和平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)

### <a name="generatedCode"></a> 生成的代码
 当你选择“生成代码”时，将创建多段代码：

- **测试方法中的行。**

  ```csharp
  [CodedUITest]
  public class CodedUITest1
  { ...
    [TestMethod]
    public void CodedUITestMethod1()
    {
        this.UIMap.AddTwoNumbers();
        // To generate more code for this test, select
        // "Generate Code" from the shortcut menu.      }
  }
  ```

   你可以在此方法中右击以添加更多录制的操作和验证。 你还可以手动编辑它以扩展或修改代码。 例如，你可以将某些代码包含在循环中。

   你还可以添加新的测试方法并且以同样的方式将代码添加到这些方法。 每个测试方法必须具有 `[TestMethod]` 特性。

- **UIMap.uitest 中的方法**

   此方法包括你所录制的方法的详细信息或你验证的值。 通过打开 UIMap.uitest，你可以编辑此代码。 它在专用编辑器中打开，你可以从中删除或重构录制的操作。

   你还可以在 UIMap.Designer.cs 中查看生成的方法。 此方法执行运行测试时录制的操作。

  ```csharp
  // File: UIMap.Designer.cs
  public partial class UIMap
  {
    /// <summary>
    /// Add two numbers
    /// </summary>
    public void AddTwoNumbers()
    { ...   }
  }
  ```

  > [!WARNING]
  > 你不应编辑此文件，因为它在你创建更多测试时会重新生成。

   通过将这些方法复制到 UIMap.cs，你可以制作方法的改编版。 例如，你可以制作可以从测试方法调用的参数化版本：

  ```csharp
  // File: UIMap.cs
  public partial class UIMap // Same partial class
  {
    /// <summary>
    /// Add two numbers – parameterized version
    /// </summary>
    public void AddTwoNumbers(int firstNumber, int secondNumber)
    { ...   // Code modified to use parameters.
    }
  }
  ```

- **UIMap.uitest 中的声明**

   这些声明表示由你的测试所使用的应用程序的 UI 控件。 它们由生成的代码使用以操作控件并且访问它们的属性。

   如果你编写自己的代码，也可以使用它们。 例如，可以使测试方法选择 Web 应用程序中的超链接、在文本框中键入一个值，或基于字段中的值进行分支并采取不同的测试操作。

   可以添加多个编码的 UI 测试以及多个 UI 映射对象和文件以便于测试大型应用程序。 有关详细信息，请参阅[使用多个 UI 映射测试大型应用程序](../test/testing-a-large-application-with-multiple-ui-maps.md)。

  有关生成的代码的更多信息，请参阅[编码的 UI 测试剖析](../test/anatomy-of-a-coded-ui-test.md)。

### <a name="actions"></a> 编码 UI 控件操作和属性
 在编码的 UI 测试中使用 UI 测试控件时，这些控件分为两部分：操作和属性。

- 第一部分包括可对 UI 测试控件执行的操作。 例如，编码的 UI 测试可以模拟鼠标点击 UI 测试控件，或模拟键盘键入来影响 UI 测试控件。

- 第二部分包括允许你获取和设置 UI 测试控件的属性。 例如，编码的 UI 测试可以获取 `ListBox` 中的项计数，或将 `CheckBox` 设置为选定状态。

  **访问 UI 测试控件的操作**

  若要对 UI 测试控件执行操作（如鼠标点击或键盘操作），请使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.Mouse> 和 <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard> 类中的方法：

- 若要对 UI 测试控件执行面向鼠标的操作（如鼠标单击），请使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.Mouse.Click%2A>。

   `Mouse.Click(buttonCancel);`

- 若要执行面向键盘的操作（如在编辑控件中键入内容），请使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard.SendKeys%2A>。

   `Keyboard.SendKeys(textBoxDestination, @"C:\Temp\Output.txt");`

  **访问 UI 测试控件的属性**

  若要获取和设置 UI 控件的特定属性值，可以直接获取或设置控件的属性值，也可以通过要获取或设置的特定属性名称使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A?displayProperty=fullName> 和 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A?displayProperty=fullName> 方法。

  <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> 返回一个对象，该对象随后可强制转换为相应的 <xref:System.Type>。 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A> 为属性的值接受一个对象。

##### <a name="to-get-or-set-properties-from-ui-test-controls-directly"></a>从 UI 测试控件直接获取或设置属性

- 使用从 T:Microsoft.VisualStudio.TestTools.UITesting.UITestControl 派生的控件（如 T:Microsoft.VisualStudio.TestTools.UITesting.HtmlControls.HtmlList 或 T:Microsoft.VisualStudio.TestTools.UITesting.WinControls.WinComboBox），可以直接获取或设置其属性值，如下所示：

    ```
    int i = myHtmlList.ItemCount;
    myWinCheckBox.Checked = true;
    ```

##### <a name="to-get-properties-from-ui-test-controls"></a>从 UI 测试控件获取属性

- 若要从控件获取属性值，请使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A>。

- 若要指定要获取的控件属性，请在每个控件中使用来自 `PropertyNames` 类的相应字符串作为 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> 的参数。

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> 返回相应的数据类型，但此返回值将被强制转换为 <xref:System.Object>。 必须再将返回的 <xref:System.Object> 强制转换为相应的类型。

     示例：

     `int i = (int)GetProperty(myHtmlList.PropertyNames.ItemCount);`

##### <a name="to-set-properties-for-ui-test-controls"></a>设置 UI 测试控件的属性

- 若要设置控件中的属性，请使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A>。

- 若要指定要设置的控件属性，请使用来自 `PropertyNames` 类的相应字符串作为 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A> 的第一个参数，使用属性值作为第二个参数。

     示例:

     `SetProperty(myWinCheckBox.PropertyNames.Checked, true);`

### <a name="debugging"></a>调试
 你可以使用编码的 UI 测试日志分析编码的 UI 测试。 编码的 UI 测试日志筛选并录制关于编码的 UI 测试运行的重要信息。 日志的格式使你能够快速调试问题。 有关详细信息，请参阅[使用编码的 UI 测试日志分析编码的 UI 测试](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)。

## <a name="VerifyCodeUsingCUITWhatsNext"></a> 后续步骤
 **运行编码的 UI 测试的其他选项：** 可直接从 Visual Studio 运行编码的 UI 测试，如本主题前面所述。 此外，你可以从 [!INCLUDE[TCMext](../includes/tcmext-md.md)] 或从 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 运行自动 UI 测试。 与其他自动测试不同，当编码的 UI 测试为自动时，在运行时它们必须与桌面进行交互。

- [如何：通过 Microsoft Visual Studio 运行测试](https://msdn.microsoft.com/library/1a1207a9-2a33-4a1e-a1e3-ddf0181b1046)

- [在 Microsoft 测试管理器中运行自动测试](https://msdn.microsoft.com/0632f265-63fe-4859-a413-9bb934c66835)

- [如何：在生成应用程序后配置和运行计划的测试](https://msdn.microsoft.com/32acfeb1-b1aa-4afb-8cfe-cc209e6183fd)

- [在你的生成过程中运行测试](https://msdn.microsoft.com/library/d05743a1-c5cf-447e-bed9-bed3cb595e38)

- [从命令行运行自动测试](https://msdn.microsoft.com/library/f18179c6-b688-4e41-9898-8aca130c4fc3)

- [如何：将测试代理设置为运行与桌面交互的测试](/visualstudio/test/how-to-set-up-your-test-agent-to-run-tests-that-interact-with-the-desktop?view=vs-2015)

- [[已停用] 在负载测试中使用编码的 UI 测试](https://msdn.microsoft.com/library/704339ff-7da7-4d5f-acb3-c3b23f4acb43)

  **添加对自定义控件的支持：** 编码的 UI 测试框架并非支持每个可能的 UI，可能不支持你要测试的 UI。 例如，不能立即创建 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] UI 的编码的 UI 测试。 然而，可以创建编码的 UI 测试框架的扩展来支持自定义控件。

- [启用控件的编码的 UI 测试](../test/enable-coded-ui-testing-of-your-controls.md)

- [扩展编码的 UI 测试和操作录制以支持 Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)

  编码的 UI 测试通常用于自动化手动测试。 有关其他指南, 请[参阅通过 Visual Studio 2012 对持续交付进行测试-第5章:自动系统测试](http://go.microsoft.com/fwlink/?LinkID=255196)。 有关手动测试的详细信息，请参阅 [[已停用] 使用 Microsoft 测试管理器创建手动测试用例](https://msdn.microsoft.com/library/9989e184-c8e4-444b-998d-a1a5ec94461e)。 有关自动系统测试的详细信息，请参阅[使用 Microsoft 测试管理器创建自动测试](https://msdn.microsoft.com/7b5075ee-ddfe-411d-b1d4-94283550a5d0)。

## <a name="external-resources"></a>外部资源

### <a name="guidance"></a>指导
- [通过 Visual Studio 2012 对持续交付进行测试-第2章:单元测试：测试内部](http://go.microsoft.com/fwlink/?LinkID=255188)

- [通过 Visual Studio 2012 对持续交付进行测试-第5章:自动系统测试](http://go.microsoft.com/fwlink/?LinkID=255196)

### <a name="faq"></a>FAQ
- [编码的 UI 测试常见问题 - 1](http://go.microsoft.com/fwlink/?LinkID=230576)

- [编码的 UI 测试常见问题 - 2](http://go.microsoft.com/fwlink/?LinkID=230578)

### <a name="forum"></a>论坛
- [Visual Studio UI 自动测试（包括 CodedUI）](http://go.microsoft.com/fwlink/?LinkID=224497)

## <a name="see-also"></a>请参阅

- [UIMap](/previous-versions/dd580454(v=vs.140))
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>
- [提高代码质量](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)
- [演练：创建、编辑和维护已编码 UI 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
- [编码的 UI 测试剖析](../test/anatomy-of-a-coded-ui-test.md)
- [编码的 UI 测试的最佳做法](../test/best-practices-for-coded-ui-tests.md)
- [使用多个 UI 映射测试大型应用程序](../test/testing-a-large-application-with-multiple-ui-maps.md)
- [使用编码的 UI 测试编辑器编辑编码的 UI 测试](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)
- [支持编码的 UI 测试和操作录制的配置和平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
- [从 Visual Studio 2010 升级编码的 UI 测试](../test/upgrading-coded-ui-tests-from-visual-studio-2010.md)
- [通过现有操作录制生成编码的 UI 测试](https://msdn.microsoft.com/library/56736963-9027-493b-b5c4-2d4e86d1d497)
