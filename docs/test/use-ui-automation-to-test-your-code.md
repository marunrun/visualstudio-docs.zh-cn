---
title: 编码的 UI 测试
ms.date: 12/04/2018
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f3bd667579d9ff0645e7dd2753278257a9796709
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75585634"
---
# <a name="use-coded-ui-test-to-test-your-code"></a>使用编码的 UI 测试来测试代码

编码的 UI 测试 (CUIT) 通过其用户界面 (UI) 驱动应用程序。 这些测试包括对 UI 控件的功能测试。 它们使你可以验证整个应用程序（包括其用户界面）是否正常运行。 编码的 UI 测试对于在用户界面中存在验证或其他逻辑（例如在网页中）的情况非常有用。 它们也经常用于自动化现有的手动测试。

在 Visual Studio 中创建编码的 UI 测试很容易。 当编码的 UI 测试生成器在后台运行时，只需手动执行该测试  。 你还可以指定在特定字段中应显示哪些值。 编码的 UI 测试生成器录制操作并从中生成代码  。 在创建测试后，你可以在专用编辑器中对其进行编辑，该编辑器使你能够修改操作的序列。

专用的编码的 UI 测试生成器和编辑器可轻松创建和编辑编码的 UI 测试，即使你的主要技能都集中于测试而不是编码  。 但如果你是一位开发人员，想要以更先进的方式扩展测试，则结构化代码，以便于更简单地复制和改写。 例如，你可以录制在网站购物的测试，然后编辑生成的代码以添加购买许多商品的循环。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="requirements"></a>要求

- Visual Studio Enterprise
- 编码的 UI 测试组件

有关编码的 UI 测试支持哪些平台和配置的详细信息，请参阅[支持的平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)。

## <a name="install-the-coded-ui-test-component"></a>安装编码的 UI 测试组件

要访问编码的 UI 测试工具和模板，请安装 Visual Studio 的编码的 UI 测试组件  。

1. 选择“工具” > “获取工具和功能”，启动 Visual Studio 安装程序    。

1. 在 Visual Studio 安装程序中，选择“单个组件”选项卡，然后向下滚动到“调试和测试”部分    。 选择编码的 UI 测试组件  。

   ![编码的 UI 测试组件](media/coded-ui-test-component.png)

1. 选择“修改”  。

## <a name="create-a-coded-ui-test"></a>创建编码的 UI 测试

1. 创建编码的 UI 测试项目。

   编码的 UI 测试必须包含在编码的 UI 测试项目中。 如果还没有编码的 UI 测试项目，请创建一个。 依次选择“文件” > “新建” > “项目”    。 搜索并选择“编码的 UI 测试项目”项目模板  。

   ::: moniker range="vs-2017"

   ![“新建项目”对话框中的编码的 UI 测试项目模板](media/coded-ui-test-project-template.png)

   ::: moniker-end

   > [!NOTE]
   > 如未看到“编码的 UI 测试项目”模板，则需要[安装编码的 UI 测试组件](../test/use-ui-automation-to-test-your-code.md#install-the-coded-ui-test-component)  。

2. 添加编码的 UI 测试文件。

     如果你刚创建了编码的 UI 项目，则自动添加第一个 CUIT 文件。 要添加另一个测试文件，请在解决方案资源管理器中打开编码的 UI 测试项目上的快捷菜单，然后选择“添加” > “编码的 UI 测试”    。

     在“为编码的 UI 测试生成代码”对话框中，选择“录制操作” > “编辑 UI 映射”或“添加断言”    。

     ![“为编码的 UI 测试生成代码”对话框](media/generate-code-for-coded-ui-test.png)

     出现“编码的 UI 测试生成器”  。

     ![编码的 UI 测试生成器](../test/media/codedui_testbuilder.png)

3. 录制一系列操作。

     **若要开始录制**，请选择“录制”  图标。 执行要在应用程序中测试的操作，必要时还包括启动应用程序。 例如，如果测试一个 Web 应用程序，你可能会启动浏览器、导航到该网站，并登录到该应用程序。

     **若要暂停录制**（例如，如果你必须处理接收的邮件），请选择“暂停”  。

    > [!WARNING]
    > 将录制在桌面上执行的所有操作。 如果你正在执行可能会导致敏感数据被包括在录制中的操作，则暂停录制。

     若要删除错误录制的操作  ，请选择“编辑步骤”  。

     若要生成将复制你的操作的代码，请选择“生成代码”图标并且键入编码的 UI 测试方法的名称和描述   。

4. 验证 UI 字段（如文本框）中的值。

     在“编码的 UI 测试生成器”中，选择“添加断言”，然后在运行的应用程序中选择 UI 控件   。 在显示的属性列表中，选择属性，例如，在文本框中的“文本”  。 在快捷菜单上，选择“添加断言”  。 在对话框中，选择比较运算符、比较值以及错误消息。

     关闭断言窗口并且选择“生成代码”  。

     ![编码的 UI 测试目标元素](../test/media/codedui_1.png)

    > [!TIP]
    > 在录制操作和验证值之间交替。 在每个操作或验证序列的结尾生成代码。 如果你愿意，可以随后插入新的操作和验证。

     有关详细信息，请参阅[验证控件的属性](#validate-the-properties-of-ui-controls)。

5. 查看生成的测试代码。

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

6. 添加更多操作和断言。

   将光标放置到测试方法中合适的点，然后在快捷菜单上，选择“为编码的 UI 测试生成代码”  。 新的代码将会在该点插入。

7. 编辑测试操作和断言的详细信息。

     打开 UIMap.uitest  。 该文件在“编码的 UI 测试编辑器”中打开，其中可编辑所录制的操作的任何序列，还可编辑断言  。

     ![编码的 UI 测试编辑器](../test/media/cuit_editor_edit.png)

     有关详细信息，请参阅[使用编码的 UI 测试编辑器编辑编码的 UI 测试](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)。

8. 运行测试。

   使用测试资源管理器，或打开测试方法中的快捷菜单，然后选择“运行测试”  。 有关如何运行测试的详细信息，请参见本主题结尾处[后续步骤](#whats-next)部分中的[用测试资源管理器运行单元测试](../test/run-unit-tests-with-test-explorer.md)和“运行编码的 UI 测试的其他选项”  。

本主题中的剩余部分提供了有关此过程中步骤的更多详细信息。

有关更详细的示例，请参见[演练：创建、编辑和维护编码的 UI 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)。 在该演练中，你将创建一个简单的 Windows Presentation Foundation (WPF) 应用程序来演示如何创建、编辑和维护编码的 UI 测试。 本演练为更正由各种计时问题和控件重构中断的测试提供了解决方案。

## <a name="start-and-stop-the-application-under-test"></a>启动和停止受测应用程序

如果不想针对每个测试分别启动和停止应用程序、浏览器或数据库，请执行以下操作：

- 如果不希望录制启动受测应用程序的操作，则必须在选择“录制”图标之前启动应用程序。 

- 在测试的结尾，在其中运行测试的进程将终止。 如果你在测试中启动应用程序，该应用程序通常会关闭。  如果不希望测试退出时关闭应用程序，请将一个 .runsettings 文件添加到解决方案，并使用 `KeepExecutorAliveAfterLegacyRun` 选项。  有关详细信息，请参阅[使用 .runsettings 文件配置单元测试](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)。

- 添加一个在每个测试方法开始时运行代码的测试初始化方法（通过 `[TestInitialize]` 属性标识）。 例如，你可以从 TestInitialize 方法启动应用程序。

- 添加一个在每个测试方法开始时运行代码的测试清除方法（通过 `[TestCleanup]` 属性标识）。 例如，可以从 TestCleanup 方法调用用于关闭应用程序的方法。

## <a name="validate-the-properties-of-ui-controls"></a>验证 UI 控件的属性

使用“编码的 UI 测试生成器”  ，可以向测试的 [UIMap](/previous-versions/dd580454(v=vs.140)) 添加用户界面 (UI) 控件，也可为使用 UI 控件断言的验证方法生成代码。

要为 UI 控件生成断言，请选择“编码的 UI 测试生成器”中的“添加断言”工具，并且将其拖放到想要验证是否正确的受测应用程序上的控件   。 在框确定控件的轮廓时，释放鼠标。 此时将立即在 UIMap.Designer.cs 文件中创建该控件类代码  。

![编码的 UI 测试目标元素](../test/media/codedui_1.png)

此时，该控件的属性在“添加断言”  对话框中列出。

另一种导航到特定控件的方法是选择箭头“(<<)”  以展开“UI 控件映射”  的视图。 若要查找父控件、同级控件或子控件，可以在映射中的任何位置单击，然后使用箭头键在树中移动。

![编码的 UI 测试属性](../test/media/codedui_2.png)

> [!TIP]
> 如果在应用程序中选择控件时没有看到任何属性，或者没有在 UI 控件图中看到控件，请验证该控件在应用程序代码中具有唯一的 ID。 唯一 ID 可以是 HTML ID 属性，也可以是 WPF UId。

接下来，打开要验证的 UI 控件的属性上的快捷菜单，然后指向“添加断言”  。 在“添加断言”  对话框中，选择断言的“比较器”  （例如，<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A>），并且在“比较值”  中键入断言的值。

![编码的 UI 测试断言](../test/media/codedui_3.png)

在你为测试添加了所有断言后，选择“确定”  。

若要为断言生成代码并将控件添加到 UI 映射中，请选择“生成代码”  图标。 请为你的编码的 UI 测试方法键入名称以及该方法的描述，这将添加作为该方法的注释。 选择“添加并生成”  。 接下来，选择“关闭”  图标以关闭“编码的 UI 测试生成器”  。 这会生成类似于以下代码的代码。 例如，如果你输入的名称为 `AssertForAddTwoNumbers`，代码将类似于此示例：

- 向编码的 UI 测试文件中的测试方法添加对断言方法 AssertForAddTwoNumbers 的调用：

    ```csharp
    [TestMethod]
    public void CodedUITestMethod1()
    {
        this.UIMap.AddTwoNumbers();
        this.UIMap.AssertForAddTwoNumbers();
    }
    ```

     你可以编辑此文件以更改步骤和断言的顺序，或创建新测试方法。 若要添加更多代码，请将光标放在测试方法上并且在快捷菜单上选择“为编码的 UI 测试生成代码”  。

- 将名为 `AssertForAddTwoNumbers` 的方法添加到你的 UI 映射 (UIMap.uitest)  。 此文件在可编辑断言的“编码的 UI 测试编辑器”中打开  。

     ![使用编码的 UI 测试编辑器编辑断言](../test/media/cuit_editor_assert.png)

     有关详细信息，请参阅[使用编码的 UI 测试编辑器编辑编码的 UI 测试](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)。

     还可在 UIMap.Designer.cs 中查看断言方法的生成代码  。 但是，不应编辑此文件。 如果想要制作代码的改编版，将方法复制到另一个文件（如 UIMap.cs），重命名方法，并在此处对它们进行编辑  。

    ```csharp
    public void AssertForAddTwoNumbers()
    {
        ...
    }
    ```

### <a name="select-a-hidden-control-using-the-keyboard"></a>使用键盘选择隐藏控件

如果尝试从“编码的 UI 测试生成器”选择“添加断言”工具时，想要选择的控件失去焦点并且消失   ：

有时，添加控件并验证它们的属性时，可能必须使用键盘。 例如，在尝试录制使用右键单击菜单控件的已编码 UI 测试时，如果你尝试从“编码的 UI 测试生成器”中选择“添加断言”工具，控件中的菜单项列表会失去焦点并消失   。 下图证明了这一点，如果你尝试使用“添加断言”  工具选择右键单击菜单，Internet Explorer 中的右键单击菜单就会失去焦点并消失。

![CodedUITest&#95;SelectControlKeyboard](../test/media/codeduitest_selectcontrolkeyboard.png)

若要使用键盘选择 UI 控件，请使用鼠标悬停在该控件上。 然后，同时按住“Ctrl”  键和“I”  键。 释放这些键。 此控件由“编码的 UI 测试生成器”录制  。

#### <a name="manually-record-mouse-hovers"></a>手动录制鼠标悬停

如果无法录制控件上的鼠标悬停：

某些情况下，编码的 UI 测试中使用的特定控件可能需要用户使用键盘来手动记录鼠标悬停事件。 例如，当你测试 Windows 窗体或 Windows Presentation Foundation (WPF) 应用程序时，可能是自定义代码。 或者，可能是针对悬停控件所定义的特殊行为，如当用户在树节点上悬停时，树节点会展开。 要测试类似这样的情况，必须通过按下预定义的键盘按键，手动通知“编码的 UI 测试生成器”正在控件上悬停  。

当你执行编码的 UI 测试时，在该控件上悬停。 在键盘上按住 Shift 和 R 键时，同时按住 Ctrl 键    。 释放这些键。 鼠标悬停事件由“编码的 UI 测试生成器”录制  。

![CodedUI&#95;Hover](../test/media/codedui_hover.png)

生成测试方法后，类似于以下示例的代码将添加到 UIMap.Designer.cs 文件  ：

```csharp
// Mouse hover '1' label at (87, 9)
Mouse.Hover(uIItem1Text, new Point(87, 9));
```

### <a name="configure-mouse-hover-keyboard-assignments"></a>配置鼠标悬停键盘分配

如果捕获鼠标悬停事件的键分配已用在环境中的其他位置：

如有必要，用于在编码的 UI 测试中应用鼠标悬停事件的默认 Ctrl+Shift+R 键盘分配可以配置为使用不同的键。   

> [!WARNING]
> 一般情况下，不必更改鼠标悬停事件的键盘分配。 在重新分配键盘分配时，请谨慎从事。 你的选择可能已用在 Visual Studio 内或测试的应用程序中的其他位置。

若要更改键盘分配，请修改以下配置文件：

%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CodedUITestBuilder.exe.config 

在配置文件中，更改 `HoverKeyModifier` 和 `HoverKey` 键的值以修改键盘分配：

```xml
<!-- Begin : Background Recorder Settings -->
<!-- HoverKey to use. -->
<add key="HoverKeyModifier" value="Control, Shift"/>
<add key="HoverKey" value="R"/>
```

### <a name="set-implicit-mouse-hovers-for-the-web-browser"></a>为 Web 浏览器设置隐式鼠标悬停

如果录制网站上的鼠标悬停时遇到了一些问题：

在很多网站中，当你在一个特定的控件上悬停时，它就会展开以显示更多细节。 通常，它们看起来像桌面应用程序中的菜单。 因为这是通用模式，因此编码的 UI 测试支持 Web 浏览的隐式悬停。 例如，如果你在 Internet Explorer 中录制悬停，会触发一个事件。 这些事件可能导致冗余悬停的录制。 因此，隐式悬停采用在 UI 测试配制文件中设置为 `ContinueOnError` 的 `true` 录制。 这可允许在悬停事件失败时，播放继续进行。

若要在 Web 浏览器中启用隐式悬停的录制，请打开配制文件：

%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CodedUITestBuilder.exe.config 

验证该配置文件是否具有设置为 `true` 值的 `RecordImplicitiHovers` 键，如以下示例所示：

```xml
<!--Use this to enable/disable recording of implicit hovers.-->
<add key="RecordImplicitHover" value="true"/>
```

## <a name="customize-the-coded-ui-test"></a>自定义编码的 UI 测试

在创建编码的 UI 测试之后，你可以通过使用 Visual Studio 中的以下任何工具对其进行编辑：

- 使用编码的 UI 测试生成器来将其他控件和验证添加到你的测试  。 请参阅本主题中的[添加控件并验证其属性](#validate-the-properties-of-ui-controls)部分。

- 通过编码的 UI 测试编辑器，可轻松修改编码的 UI 测试  。 使用编码的 UI 测试编辑器，可查找、查看和编辑测试方法  。 也可以在 UI 控件映射中编辑 UI 操作及其关联的控件。 有关详细信息，请参阅[使用编码的 UI 测试编辑器编辑编码的 UI 测试](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)。

- **代码编辑器：**

  - 按照本主题中的[编码的 UI 控件操作和属性](#coded-ui-control-actions-and-properties)部分的描述，为测试中的控件手动添加代码。

  - 在创建编码的 UI 测试以后，你可以将其修改为数据驱动。 有关详细信息，请参阅[创建数据驱动的编码的 UI 测试](../test/creating-a-data-driven-coded-ui-test.md)。

  - 在编码的 UI 测试播放中，你可以指示测试等待某些事件发生，如某个窗口出现、进度栏消失等。 为此，请添加相应的 UITestControl.WaitForControlXXX() 方法。 有关可用方法的完整列表，请参阅[播放期间让编码的 UI 测试等待特定事件](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md)。 有关使用 WaitForControlEnabled 方法等待启用某个控件的编码的 UI 测试示例，请参阅[演练：创建、编辑和维护编码的 UI 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)。

  - 编码的 UI 测试包括对某些包含在 Internet Explorer 9 和 Internet Explorer 10 中的 HTML5 控件的支持。 有关详细信息，请参阅[在编码的 UI 测试中使用 HTML5 控件](../test/using-html5-controls-in-coded-ui-tests.md)。

  - 编码的 UI 测试编码指导：

    - [编码的 UI 测试剖析](../test/anatomy-of-a-coded-ui-test.md)

    - [编码的 UI 测试的最佳做法](../test/best-practices-for-coded-ui-tests.md)

    - [通过多个 UI 映射测试大型应用程序](../test/testing-a-large-application-with-multiple-ui-maps.md)

    - [支持编码的 UI 测试和操作录制的配置和平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)

### <a name="the-generated-code"></a>生成的代码

当你选择“生成代码”  时，将创建多段代码：

- 测试方法中的行。

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

-  UIMap.uitest 中的方法。

     此方法包括你所录制的方法的详细信息或你验证的值。 打开 UIMap.uitest，可编辑此代码  。 它在专用编辑器中打开，你可以从中删除或重构录制的操作。

     还可在 UIMap.Designer.cs 中查看生成的方法  。 此方法执行运行测试时录制的操作。

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

     通过将这些方法复制到 UIMap.cs，可以制作方法的改编版  。 例如，你可以制作可以从测试方法调用的参数化版本：

    ```csharp
    // File: UIMap.cs
    public partial class UIMap // Same partial class
    {
      /// <summary>
      /// Add two numbers - parameterized version
      /// </summary>
      public void AddTwoNumbers(int firstNumber, int secondNumber)
      { ...   // Code modified to use parameters.
      }
    }
    ```

-  UIMap.uitest 中的声明。

    这些声明表示由你的测试所使用的应用程序的 UI 控件。 它们由生成的代码使用以操作控件并且访问它们的属性。

    如果你编写自己的代码，也可以使用它们。 例如，可以使测试方法选择 Web 应用程序中的超链接、在文本框中键入一个值，或基于字段中的值进行分支并采取不同的测试操作。

    可以添加多个编码的 UI 测试以及多个 UI 映射对象和文件，便于测试大型应用程序。 有关详细信息，请参阅[使用多个 UI 映射测试大型应用程序](../test/testing-a-large-application-with-multiple-ui-maps.md)。

有关生成的代码的详细信息，请参阅[编码的 UI 测试剖析](../test/anatomy-of-a-coded-ui-test.md)。

## <a name="coded-ui-control-actions-and-properties"></a>编码的 UI 控件操作和属性

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

### <a name="to-get-or-set-properties-from-ui-test-controls-directly"></a>从 UI 测试控件直接获取或设置属性

使用派生自 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl>如 [HtmlList](xref:Microsoft.VisualStudio.TestTools.UITesting.HtmlControls.HtmlList) 或 [WinComboBox](xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls.WinComboBox)）的控件，可以直接获取或设置其属性值。 以下代码演示了部分示例：

```csharp
int i = myHtmlList.ItemCount;
myWinCheckBox.Checked = true;
```

### <a name="to-get-properties-from-ui-test-controls"></a>从 UI 测试控件获取属性

- 若要从控件获取属性值，请使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A>。

- 若要指定要获取的控件属性，请在每个控件中使用来自 `PropertyNames` 类的相应字符串作为 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> 的参数。

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> 返回相应的数据类型，但此返回值将被强制转换为 <xref:System.Object>。 必须再将返回的 <xref:System.Object> 强制转换为相应的类型。

     示例：

     `int i = (int)GetProperty(myHtmlList.PropertyNames.ItemCount);`

### <a name="to-set-properties-for-ui-test-controls"></a>设置 UI 测试控件的属性

- 若要设置控件中的属性，请使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A>。

- 若要指定要设置的控件属性，请使用来自 `PropertyNames` 类的相应字符串作为 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A> 的第一个参数，使用属性值作为第二个参数。

     示例：

     `SetProperty(myWinCheckBox.PropertyNames.Checked, true);`

## <a name="debug"></a>调试

你可以使用编码的 UI 测试日志分析编码的 UI 测试。 编码的 UI 测试日志筛选并录制关于编码的 UI 测试运行的重要信息。 日志的格式使你能够快速调试问题。 有关详细信息，请参阅[使用编码的 UI 测试日志分析编码的 UI 测试](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)。

## <a name="whats-next"></a>后续步骤

**运行编码的 UI 测试的其他选项：** 可直接从 Visual Studio 运行编码的 UI 测试，如本主题前面所述。 此外，可以在 Microsoft 测试管理器中或使用 Azure Pipelines 运行自动 UI 测试。 与其他自动测试不同，当编码的 UI 测试为自动时，在运行时它们必须与桌面进行交互。

- [使用测试资源管理器运行单元测试](../test/run-unit-tests-with-test-explorer.md)

- [在你的生成过程中运行测试](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts)

- [如何：设置测试代理以运行与桌面交互的测试](https://msdn.microsoft.com/Library/3a94dd07-6d17-402c-ae8f-7947143755c9)

**添加对自定义控件的支持：** 编码的 UI 测试框架并非支持每个可能的 UI，可能不支持你要测试的 UI。 例如，不能立即创建 Microsoft Excel UI 的编码的 UI 测试。 然而，可以创建编码的 UI 测试框架的扩展来支持自定义控件。

- [启用控件的编码的 UI 测试](../test/enable-coded-ui-testing-of-your-controls.md)

- [扩展编码的 UI 测试和操作录制](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)

编码的 UI 测试通常用于自动化手动测试。 有关手动测试的详细信息，请参阅[使用 Microsoft 测试管理器运行手动测试](/azure/devops/test/mtm/run-manual-tests-with-microsoft-test-manager?view=vsts)。 有关自动测试的详细信息，请参阅 [Visual Studio 中的测试工具](../test/improve-code-quality.md)。

## <a name="see-also"></a>请参阅

- [录制和播放手动测试](/azure/devops/test/mtm/record-play-back-manual-tests?view=vsts)
- [Xamarin.UITest](/appcenter/test-cloud/uitest/)
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>
- [演练：创建、编辑和维护编码的 UI 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
- [创建编码的 UI 测试来测试 UWP 应用](test-uwp-app-with-coded-ui-test.md)
- [编码的 UI 测试剖析](../test/anatomy-of-a-coded-ui-test.md)
- [编码的 UI 测试的最佳做法](../test/best-practices-for-coded-ui-tests.md)
- [通过多个 UI 映射测试大型应用程序](../test/testing-a-large-application-with-multiple-ui-maps.md)
