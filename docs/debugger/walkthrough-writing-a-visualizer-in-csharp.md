---
title: 在 | 中C#编写可视化工具Microsoft Docs
ms.custom: seodec18
ms.date: 04/12/2019
ms.topic: conceptual
dev_langs:
- CSharp
helpviewer_keywords:
- visualizers, writing
- walkthroughs [Visual Studio], visualizers
ms.assetid: 53467461-8e0f-45ee-9bc4-374bbaeaf00f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a46967d5f46c4f495a07d80e5f73cfc9f9d60c1a
ms.sourcegitcommit: 7b07e7b5e06e2e13f622445c568b78a284e1a40d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2020
ms.locfileid: "76542628"
---
# <a name="walkthrough-writing-a-visualizer-in-c"></a>演练：用 C\# 编写可视化工具
本演练演示如何使用 C# 编写简单的可视化工具。 本演练中创建的可视化工具使用 Windows 窗体消息框显示字符串的内容。 这种简单的字符串可视化工具本身并不有用，但它显示为其他数据类型创建更有用的可视化工具时必须遵循的基本步骤。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你的当前设置或版本。 若要更改设置，请转到 "**工具**" 菜单，然后选择 "**导入和导出设置**"。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

可视化工具代码必须放置在一个 DLL 中，该 DLL 将被调试器读取。 因此，第一步是为 DLL 创建类库项目。

## <a name="create-a-visualizer-manually"></a>手动创建可视化工具

按照以下任务创建可视化工具。

### <a name="to-create-a-class-library-project"></a>创建类库项目

1. 创建一个新类库项目。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口。 键入**Ctrl + Q**打开搜索框 **，键入 "类库"** ，选择 "**模板**"，然后选择 "**创建新的类库（.NET Framework）** "。 在出现的对话框中，选择“创建”。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件” > “新建” > “项目”。 在 "**新建项目**" 对话框的左窗格中，选择 **" C#视觉对象**" 下的 " **.NET Framework**"，然后在中间窗格中选择 "类库 **（.NET Framework）** "。
    ::: moniker-end

2. 为类库键入适当的名称，如 "`MyFirstVisualizer`"，然后单击 "**创建**" 或 **"确定"** 。

   创建类库后，必须添加对 Microsoft.VisualStudio.DebuggerVisualizers.DLL 的引用，以便使用其中定义的类。 但是，在添加引用之前，必须重命名某些类，使其具有有意义的名称。

### <a name="to-rename-class1cs-and-add-microsoftvisualstudiodebuggervisualizers"></a>重命名 Class1.cs 并添加 VisualStudio. Microsoft.visualstudio.debuggervisualizers.dll

1. 在**解决方案资源管理器**中，右键单击 Class1.cs，然后在快捷菜单上选择 "**重命名**"。

2. 将名称从 Class1.cs 更改为有意义的名称，如 DebuggerSide.cs。

   > [!NOTE]
   > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 会自动更改 DebuggerSide.cs 中的类声明，以便与新文件名匹配。

3. 在**解决方案资源管理器**中，右键单击 "**引用**"，然后选择快捷菜单上的 "**添加引用**"。

4. 在 "**添加引用**" 对话框中的 "**浏览**" 选项卡上，选择 "**浏览**"，然后找到 VisualStudio. microsoft.visualstudio.debuggervisualizers.dll。

    可在 Visual Studio 安装目录的 *\<Visual Studio 安装目录 > \Common7\IDE\PublicAssemblies*子目录中找到该 DLL。

5. 单击" **确定**"。

6. 在 DebuggerSide.cs 中，将以下内容添加到 `using` 指令中：

   ```csharp
   using Microsoft.VisualStudio.DebuggerVisualizers;
   ```

   现在已经准备好创建调试器端代码了。 这是运行在调试器中以显示要可视化的信息的代码。 首先，必须更改 `DebuggerSide` 对象的声明，以便继承自基类 `DialogDebuggerVisualizer`。

### <a name="to-inherit-from-dialogdebuggervisualizer"></a>从 DialogDebuggerVisualizer 继承

1. 在 DebuggerSide.cs 中，请执行以下代码行：

   ```csharp
   public class DebuggerSide
   ```

2. 将代码更改为：

   ```csharp
   public class DebuggerSide : DialogDebuggerVisualizer
   ```

   `DialogDebuggerVisualizer` 具有一个抽象方法 (`Show`)，必须重写此方法。

#### <a name="to-override-the-dialogdebuggervisualizershow-method"></a>重写 DialogDebuggerVisualizer.Show 方法

- 在 `public class DebuggerSide` 中添加下面的方法：

  ```csharp
  protected override void Show(IDialogVisualizerService windowService, IVisualizerObjectProvider objectProvider)
  {
  }
  ```

  `Show` 方法包含实际创建可视化工具对话框或其他用户界面的代码，并显示已从调试器传递到可视化工具的信息。 您必须添加创建该对话框并显示该信息的代码。 在本演练中，将使用 Windows 窗体消息框执行此操作。 首先，必须为 System.web 添加 reference 和 `using` 指令。

### <a name="to-add-systemwindowsforms"></a>添加 System.Windows.Forms

1. 在**解决方案资源管理器**中，右键单击 "**引用**"，然后选择快捷菜单上的 "**添加引用**"。

2. 在 "**添加引用**" 对话框中的 "**浏览**" 选项卡上，选择 "**浏览**"，然后找到 "system.web"。

    可以在*C:\Windows\Microsoft.NET\Framework\v4.0.30319*中找到该 DLL。

3. 单击" **确定**"。

4. 在 DebuggerSide.cs 中，将以下内容添加到 `using` 指令中：

   ```csharp
   using System.Windows.Forms;
   ```

   现在，可添加一些代码以创建和显示可视化工具的用户界面。 由于这是您的第一个可视化工具，因此我们会使用户界面保持简单并使用消息框。

### <a name="to-show-the-visualizer-output-in-a-dialog-box"></a>在对话框中显示可视化工具输出

1. 在 `Show` 方法中，添加以下代码行：

   ```csharp
   MessageBox.Show(objectProvider.GetObject().ToString());
   ```

    此代码示例中不包含错误处理。 但在实际的可视化工具或任何其他类型的应用程序中，应当包含错误处理。

2. 在 "**生成**" 菜单上，选择 "**生成 MyFirstVisualizer**"。 该项目应能成功生成。 在继续前更正所有生成错误。

   这是调试器端代码的结尾部分。 但是还有一步操作：添加用于通知调试对象端哪些类集合构成可视化工具的属性。

### <a name="to-add-the-debuggee-side-code"></a>添加调试对象端代码

1. 在 `using` 指令之后但在 `namespace MyFirstVisualizer`之前，将以下特性代码添加到 DebuggerSide.cs：

   ```csharp
   [assembly:System.Diagnostics.DebuggerVisualizer(
   typeof(MyFirstVisualizer.DebuggerSide),
   typeof(VisualizerObjectSource),
   Target = typeof(System.String),
   Description = "My First Visualizer")]
   ```

2. 在 "**生成**" 菜单上，选择 "**生成 MyFirstVisualizer**"。 该项目应能成功生成。 在继续前更正所有生成错误。

   这时，第一个可视化工具就完成了。 如果您已正确地按照每一步操作，您可以生成该可视化工具，并将其安装到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中。 但在将可视化工具安装到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中之前，应对其进行测试以确保它能够正常运行。 你现在将创建一个测试套以在没有将可视化工具安装到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的情况下运行它。

### <a name="to-add-a-test-method-to-show-the-visualizer"></a>添加测试方法以显示可视化工具

1. 将下面的方法添加到类 `public DebuggerSide`：

   ```csharp
   public static void TestShowVisualizer(object objectToVisualize)
   {
      VisualizerDevelopmentHost visualizerHost = new VisualizerDevelopmentHost(objectToVisualize, typeof(DebuggerSide));
      visualizerHost.ShowVisualizer();
   }
   ```

2. 在 "**生成**" 菜单上，选择 "**生成 MyFirstVisualizer**"。 该项目应能成功生成。 在继续前更正所有生成错误。

   然后，您必须创建一个可执行项目以调用可视化工具 DLL。 为简单起见，我们将使用控制台应用程序项目。

### <a name="to-add-a-console-application-project-to-the-solution"></a>将控制台应用程序项目添加到解决方案中

1. 在解决方案资源管理器中，右键单击解决方案，选择 "**添加**"，然后单击 "**新建项目**"。

    ::: moniker range=">=vs-2019"
    在搜索框中，键入 "**控制台应用**"，选择 "**模板**"，然后选择 "**创建新的控制台应用（.NET Framework）** "。 在出现的对话框中，选择“创建”。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件” > “新建” > “项目”。 在“新建项目”对话框的左窗格中，在“Visual C#”下，选择“Windows 桌面”，然后在中间窗格中选择“控制台应用(.NET Framework)”。
    ::: moniker-end

2. 为类库键入适当的名称，如 "`MyTestConsole`"，然后单击 "**创建**" 或 **"确定"** 。

   现在，必须添加必要的引用，以便 MyTestConsole 能够调用 MyFirstVisualizer。

### <a name="to-add-necessary-references-to-mytestconsole"></a>添加对 MyTestConsole 的必需引用

1. 在**解决方案资源管理器**中，右键单击**MyTestConsole** ，然后选择快捷菜单上的 "**添加引用**"。

2. 在 "**添加引用**" 对话框中，选择 "**浏览**" 选项卡，然后选择 VisualStudio. microsoft.visualstudio.debuggervisualizers.dll。

3. 单击" **确定**"。

4. 右键单击**MyTestConsole** ，然后再次选择 "**添加引用**"。

5. 在 "**添加引用**" 对话框中，单击 "**项目**" 选项卡，然后单击 "MyFirstVisualizer"。

6. 单击" **确定**"。

   现在，你将添加代码以完成测试套。

### <a name="to-add-code-to-mytestconsole"></a>将代码添加到 MyTestConsole

1. 在**解决方案资源管理器**中，右键单击 Program.cs，然后在快捷菜单上选择 "**重命名**"。

2. 将 Program.cs 中的名称编辑为更有意义的名称，如 TestConsole.cs。

    > [!NOTE]
    > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 会自动更改 TestConsole.cs 中的类声明，以便与新文件名匹配。

3. 在 TestConsole.cs 中，将以下代码添加到 `using` 指令：

   ```csharp
   using MyFirstVisualizer;
   ```

4. 在方法 `Main` 中，添加以下代码：

   ```csharp
   String myString = "Hello, World";
   DebuggerSide.TestShowVisualizer(myString);
   ```

   现在已准备好测试你的第一个可视化工具了。

### <a name="to-test-the-visualizer"></a>测试可视化工具

1. 在**解决方案资源管理器**中，右键单击**MyTestConsole** ，然后在快捷菜单上选择 "**设为启动项目**"。

2. 在“调试”菜单上选择“启动”。

    控制台应用程序启动并显示可视化工具，并显示字符串 "Hello，World"。

   祝贺你。 你刚刚生成了第一个可视化工具并进行了测试。

   如果您想在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中使用可视化工具，而不是只从测试工具中调用它，则需要安装它。 有关详细信息，请参阅[如何：安装可视化工具](../debugger/how-to-install-a-visualizer.md)。

## <a name="create-a-visualizer-using-the-visualizer-item-template"></a>使用可视化工具项模板创建可视化工具

到目前为止，本演练演示了如何手动创建可视化工具。 这是一种学习训练。 了解简单的可视化工具的工作原理后，可以使用可视化工具项模板轻松创建一个。

首先，必须创建一个新的类库项目。

### <a name="to-create-a-new-class-library"></a>创建新的类库

1. 在“文件”菜单上，选择“新建”>“项目”。

2. 在 "**新建项目**" 对话框中的 **" C#视觉对象**" 下，选择 **.NET Framework**。

3. 在中间窗格中 **，选择 "类库"** 。

4. 在 "**名称**" 框中，为类库键入适当的名称，如 "MySecondVisualizer"。

5. 单击" **确定**"。

   现在，你可以向其添加可视化工具项：

### <a name="to-add-a-visualizer-item"></a>添加可视化工具项

1. 在**解决方案资源管理器**中，右键单击 MySecondVisualizer。

2. 在快捷菜单上，选择 "**添加**"，然后单击 "**新建项**"。

3. 在 "**添加新项**" 对话框中的 **" C#可视项**" 下，选择 "**调试器可视化工具**"。

4. 在 "**名称**" 框中，键入适当的名称，如 SecondVisualizer.cs。

5. 单击“添加”。

   就是这样。 查看文件 SecondVisualizer.cs，并查看模板添加的代码。 继续测试代码。 了解基础知识后，你将能够创建自己的更复杂、更有用的可视化工具。

## <a name="see-also"></a>另请参阅

- [可视化工具体系结构](../debugger/visualizer-architecture.md)
- [如何：安装可视化工具](../debugger/how-to-install-a-visualizer.md)
- [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)
