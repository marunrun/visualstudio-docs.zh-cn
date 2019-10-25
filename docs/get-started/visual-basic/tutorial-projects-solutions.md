---
title: 教程项目和解决方案 Visual Basic
ms.date: 12/12/2018
ms.technology: vs-ide-general
ms.custom: get-started
ms.topic: tutorial
author: jillre
ms.author: jillfra
manager: jillfra
dev_langs:
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 22c48086fb98cc4ae25098cb70c642f77f621209
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72632574"
---
# <a name="learn-about-projects-and-solutions-using-visual-basic"></a>通过 Visual Basic 了解项目和解决方案

在这篇介绍性的文章中，我们将探讨在 Visual Studio 中创建解决方案和项目的含义   。 解决方案是一个容器，用于组织一个或多个相关的代码项目，例如，一个类库项目和一个对应的测试项目。 我们会介绍项目的属性和其中包含的一些文件。 此外，我们还会在一个项目中创建对另一项目的引用。

::: moniker range="vs-2017"

> [!TIP]
> 如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

> [!TIP]
> 如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

我们会从头开始构建解决方案和项目，将此作为教学手段来介绍项目的概念。 一般来说，使用 Visual Studio 创建新项目时，很可能会用到 Visual Studio 提供的部分项目模板  。

> [!NOTE]
> 在 Visual Studio 中开发应用时不需要用到解决方案和项目。 也可只打开包含代码的文件夹，并开始编写代码、生成和调试。 例如，如果克隆 [GitHub](https://github.com/) 存储库，其中可能不包含 Visual Studio 项目和解决方案。 有关详细信息，请参阅[在 Visual Studio 中开发代码而无需创建项目或解决方案](../../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)。

## <a name="solutions-and-projects"></a>解决方案和项目

尽管其名称如此，但解决方案并不是“答案”。 解决方案仅仅是 Visual Studio 用来组织一个或多个相关项目的容器。 在 Visual Studio 中打开解决方案时，它会自动加载其中包含的所有项目。

### <a name="create-a-solution"></a>创建解决方案

我们先创建一个空的解决方案。 对 Visual Studio 有一定了解后，可能就不会经常创建空的解决方案。 在 Visual Studio 中创建新项目时，如果没有打开的解决方案，它会自动创建一个解决方案来存放项目。

::: moniker range="vs-2017"

1. 打开 Visual Studio。

1. 在菜单栏上选择“文件”  >“新建”  >“项目”  。

   **“新建项目”** 对话框随即打开。

1. 在左侧窗格中，展开“其他项目类型”，然后选择“Visual Studio 解决方案”   。 在中间窗格中，选择“空白解决方案”模板  。 将解决方案命名为“QuickSolution”，然后选择“确定”   。

   ![Visual Studio 中的空白解决方案模板](../media/tutorial-projects-new-solution.png)

   此时“起始页”关闭，Visual Studio 窗口右侧的“解决方案资源管理器”中出现解决方案   。 你可能会经常使用“解决方案资源管理器”来浏览项目的内容  。

::: moniker-end

::: moniker range=">=vs-2019"

1. 打开 Visual Studio。

2. 在“开始”窗口上，选择“创建新项目”  。

3. 在“创建新项目”页上，  在搜索框中输入“空白解决方案”  ，选择“空白解决方案”模板，然后选择“下一步”   。

   ![Visual Studio 2019 中的空白解决方案模板](../media/vs-2019/tutorial-projects-blank-solution-template.png)

4. 将解决方案命名为“QuickSolution”  ，然后选择“创建”  。

   解决方案将显示在 Visual Studio 窗口右侧的解决方案资源管理器中  。 你可能会经常使用“解决方案资源管理器”来浏览项目的内容  。

::: moniker-end

### <a name="add-a-project"></a>添加项目

现在我们将第一个项目添加到解决方案。 先从空项目开始，将所需项添加到项目中。

::: moniker range="vs-2017"

1. 在“解决方案资源管理器”中的“解决方案‘QuickSolution’”的右键菜单或上下文菜单中，依次选择“添加”>“新建项目”     。

   此时会打开 **“添加新项目”** 对话框。

1. 在左侧窗格中，展开“Visual Basic”，然后选择“Windows 桌面”   。 然后在中间窗格中，选择“空项目(.NET Framework)”模板  。 将项目命名为“QuickDate”，然后选择“确定”按钮   。

   随后名为“QuickDate”的项目出现在“解决方案资源管理器”中的解决方案下  。 目前它包含一个名为“App.config”的文件  。

   > [!NOTE]
   > 如果在对话框的左侧窗格中看不到“Visual Basic”，则需安装“.NET 桌面开发”Visual Studio“工作负载”    。 Visual Studio 使用基于工作负载的安装旨在安装所执行的开发类型需要的组件。 一种安装新工作负载的简单方法是选择“添加新项目”对话框左下角的“打开 Visual Studio 安装程序”链接   。 在“Visual Studio 安装程序”启动后，选择“.NET 桌面开发”工作负载，再单击“修改”按钮   。
   >
   > ![“打开 Visual Studio 安装程序”链接](media/tutorial-projects-open-installer-vb.png)

::: moniker-end

::: moniker range=">=vs-2019"

1. 在“解决方案资源管理器”中的“解决方案‘QuickSolution’”的右键菜单或上下文菜单中，依次选择“添加”>“新建项目”     。

   随即打开显示“添加新项目”的对话框  。

1. 在顶部的搜索框中输入文本“空”，然后在“语言”下选择“Visual Basic”    。

1. 然后选择“空项目 (.NET Framework)”模板并选择“下一步”   。

1. 将项目命名为“QuickDate”，然后选择“创建”   。

   随后名为“QuickDate”的项目出现在“解决方案资源管理器”中的解决方案下  。 目前它包含一个名为“App.config”的文件  。

   > [!NOTE]
   > 如果没有看到“空项目 (.NET Framework)”模板，则需要安装 .NET 桌面开发 Visual Studio 工作负载    。 Visual Studio 使用基于工作负载的安装旨在安装所执行的开发类型需要的组件。 在创建新项目时安装新工作负载的简便方法是，在显示“未找到你要查找的内容”的文本下选择“安装更多工具和功能”链接   。 在“Visual Studio 安装程序”启动后，选择“.NET 桌面开发”工作负载，再单击“修改”按钮   。
   >
   > ![Visual Studio 2019 中的安装程序链接](../media/vs-2019/tutorial-projects-open-installer.png)

::: moniker-end

## <a name="add-an-item-to-the-project"></a>向项目添加一个项

我们有一个空项目。 我们来添加代码文件。

1. 在“解决方案资源管理器”中的“QuickDate”项目的右键菜单或上下文菜单中，依次选择“添加” > “新建项”     。

   此时将打开“添加新项”  对话框。

1. 展开“常用项”，然后选择“代码”   。 在中间窗格中，选择“类”项模板  。 将类命名为“Calendar”，然后选择“添加”按钮   。

   名为“Calendar.vb”的文件已添加到项目  。 末尾的“.vb”是 Visual Basic 代码文件的文件扩展名  。 文件出现在“解决方案资源管理器”中的可视项目层次结构中，其内容在编辑器中打开  。

1. 将“Calendar.vb”文件的内容替换为以下代码  ：

   ```vb
   Class Calendar
       Public Shared Function GetCurrentDate() As Date
           Return DateTime.Now.Date
       End Function
   End Class
   ```

   `Calendar` 类包含一个函数 `GetCurrentDate`，它返回当前日期。

1. 双击“解决方案资源管理器”中的“我的项目”，打开项目属性   。 在“应用程序”选项卡上，将“应用程序类型”更改为“类库”    。 此步骤是成功生成项目所必需的。

1. 通过右键单击“解决方案资源管理器”中的“QuickDate”并选择“生成”来生成项目    。 “输出”窗口中会显示一条成功生成消息  。

## <a name="add-a-second-project"></a>添加第二个项目

包含多个项目的解决方案很常见，而且这些项目通常相互引用。 解决方案中的一些项目可能是类库，可能是可执行应用程序，也可能是单元测试项目或网站。

我们来向解决方案添加单元测试项目。 这次我们从项目模板开始，所以不需要向项目添加额外的代码文件。

1. 在“解决方案资源管理器”中的“解决方案‘QuickSolution’”的右键菜单或上下文菜单中，依次选择“添加” > “新建项目”     。

::: moniker range="Vs-2017"

2. 在左侧窗格中，展开“Visual Basic”，然后选择“测试”类别   。 在中间窗格中，选择“单元测试项目(.NET Framework)”项目模板  。 将项目命名为“QuickTest”，然后选择“确定”   。

   第二个项目已添加到“解决方案资源管理器”，且编辑器中打开了名为“UnitTest1.vb”的文件   。

   ![包含两个项目的“Visual Studio 解决方案资源管理器”](media/tutorial-projects-solution-explorer-vb.png)

::: moniker-end

::: moniker range=">=vs-2019"

2. 在“添加新项目”对话框中，在顶部的搜索框输入文本“单元测试”，然后在“语言”下选择“Visual Basic”     。

3. 选择“单元测试项目(.NET Framework)”项目模板，然后选择“下一步”   。

4. 将项目命名为“QuickTest”，然后选择“创建”   。

   第二个项目已添加到“解决方案资源管理器”，且编辑器中打开了名为“UnitTest1.vb”的文件   。

::: moniker-end

## <a name="add-a-project-reference"></a>添加项目引用

我们将使用新的单元测试项目测试“QuickDate”项目中的方法，因此需要添加对该项目的引用  。 创建引用会在两个项目间创建生成依赖关系，这意味着生成解决方案时，会先生成“QuickDate”，再生成“QuickTest”    。

1. 选择“QuickTest”项目中的“引用”节点，然后在右键菜单或上下文菜单中选择“添加引用”    。

   ![“添加引用”菜单](media/tutorial-projects-add-reference-vb.png)

   “引用管理器”对话框随即打开  。

1. 在左侧窗格中，展开“项目”，然后选择“解决方案”   。 在中间窗格中，选中“QuickDate”旁的复选框，然后选择“确定”按钮   。

   已添加对“QuickDate”项目的引用  。

## <a name="add-test-code"></a>添加测试代码

1. 现在我们向 Visual Basic 代码文件添加测试代码。 将“UnitTest1.vb”的内容替换为以下代码  。

   ```vb
   <TestClass()> Public Class UnitTest1

       <TestMethod()> Public Sub TestGetCurrentDate()
           Assert.AreEqual(Date.Now.Date, QuickDate.Calendar.GetCurrentDate())
       End Sub

   End Class
   ```

   你会看到某些代码下出现红色波浪线。 将测试项目设为“QuickDate”项目的[友元程序集](/dotnet/visual-basic/programming-guide/concepts/assemblies-gac/friend-assemblies)来解决此错误  。

1. 返回“QuickDate”项目，如果“Calendar.vb”文件尚未打开，则打开该文件，然后添加以下[导入语句](/dotnet/visual-basic/language-reference/statements/imports-statement-net-namespace-and-type)和 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性，以解决测试项目中的错误   。

   ```vb
   Imports System.Runtime.CompilerServices

   <Assembly: InternalsVisibleTo("QuickTest")>
   ```

   代码文件应如下所示：

   ![Visual Basic 代码](media/tutorial-projects-code-vb.png)

## <a name="project-properties"></a>项目属性

包含 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性的“Calendar.vb”文件中的行引用了“QuickTest”项目的程序集名称（文件名）   。 程序集名称可能不会始终与项目名称相同。 若要查看项目的程序集名称，请打开项目属性。

1. 在“解决方案资源管理器”中，选择“QuickTest”项目   。 在右键菜单或上下文菜单中，选择“属性”，或只按 Alt+Enter 即可    。 （还可以在“解决方案资源管理器”中双击“我的项目”   ）

   项目的“属性页”随即在“应用程序”选项卡上打开   。属性页包含项目的各种设置。 请注意，“QuickTest”项目的程序集名称确实为“QuickTest”  。 如果想要更改，可在此处更改。 随后，在生成测试项目时，生成的二进制文件的名称将从“QuickTest.dll”更改为所选择的名称  。

   ![项目属性](../media/tutorial-projects-properties.png)

1. 了解项目属性页的其他选项卡，例如“编译”和“设置”   。 这些选项卡对不同类型的项目是不同的。

## <a name="optional-run-the-test"></a>（可选）运行测试

若希望检查单元测试是否正常工作，请从菜单栏依次选择“测试” > “运行” > “所有测试”    。 此时名为“测试资源管理器”的窗口打开，你应该会看到“TestGetCurrentDate”测试通过   。

![Visual Studio 中显示已通过的测试的文本资源管理器](../media/tutorial-projects-test-explorer.png)

> [!TIP]
> 如果“测试资源管理器”未自动打开，请从菜单中选择“测试” > “Windows” > “测试资源管理器”     。

## <a name="next-steps"></a>后续步骤

如果想进一步了解 Visual Studio，请考虑按照某个 [Visual Basic 教程](index.yml)创建应用。

## <a name="see-also"></a>请参阅

- [创建项目和解决方案](../../ide/creating-solutions-and-projects.md)
- [管理项目和解决方案属性](../../ide/managing-project-and-solution-properties.md)
- [管理项目中的引用](../../ide/managing-references-in-a-project.md)
- [在 Visual Studio 中开发代码而无需项目或解决方案](../../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)
- [Visual Studio IDE 概述](../../get-started/visual-studio-ide.md)