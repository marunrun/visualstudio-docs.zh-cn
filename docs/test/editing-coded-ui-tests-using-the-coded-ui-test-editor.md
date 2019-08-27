---
title: 编辑编码的 UI 测试
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.codedUItest.testeditor
helpviewer_keywords:
- coded UI test, Coded UI Test Editor
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 88002f4187883d55f22ec9f3dc80f3ceb65e7e48
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62784373"
---
# <a name="edit-coded-ui-tests-using-the-coded-ui-test-editor"></a>使用编码的 UI 测试编辑器编辑编码的 UI 测试

通过编码的 UI 测试编辑器，可轻松修改编码的 UI 测试。 使用编码的 UI 测试编辑器，可以查找、查看和编辑测试方法和 UI 操作的属性。 此外，你还可以使用 UI 控件图查看和编辑其对应的控件。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**要求**

- Visual Studio Enterprise
- 编码的 UI 测试组件

## <a name="features-of-the-coded-ui-test-editor"></a>编码的 UI 测试编辑器的功能

使用编码的 UI 测试编辑器比使用代码编辑器在编码的 UI 测试方法中编辑代码速度更快，效率更高。 使用编码的 UI 测试编辑器，可以使用工具栏和快捷菜单快速查找和修改与 UI 操作和控件相关联的属性值。 例如，可以使用编码的 UI 测试编辑器的工具栏执行以下命令：

![UI 测试编辑器](../test/media/uitesteditor.png)

1. “[查找](../ide/finding-and-replacing-text.md)”有助于查找 UI 操作和控件。

2. **删除** 可删除不想要的 UI 操作。

3. **重命名** 可以更改测试方法和控件的名称。

4. 属性可以打开所选项的“属性”窗口。

5. **拆分成新方法** 可以模块化 UI 操作。

6. **移动代码** 可以将自定义代码添加到你的测试方法。

7. **在前面插入延迟** 可以在执行 UI 操作之前添加暂停，以毫秒为单位。

8. **查找 UI 控件** 可识别待测试应用程序的 UI 中控件的位置。

9. **查找全部**可帮助你验证控制属性和对应用程序控件所做的重大更改。

打开与编码的 UI 测试关联的 UIMap.uitest 文件时，编码的 UI 测试编辑器中随即打开编码的 UI 测试。 下面的过程介绍了随后如何使用编辑器工具栏和快捷菜单查找和编辑测试方法、UI 操作的属性和控件。

## <a name="open-a-coded-ui-test"></a>打开编码的 UI 测试

你可以使用编码的 UI 测试编辑器查看和编辑基于 Visual C# 和 Visual Basic 的编码的 UI 测试。

![“编码的 UI 测试生成器”的“编辑”上下文菜单](../test/media/editcodeduitest.png)

在“解决方案资源管理器”中，打开“UIMap.uitest”的快捷菜单，然后选择 “打开”。 编码的 UI 测试编辑器中随即显示编码的 UI 测试。 现在，你可以查看和编辑编码的 UI 测试中记录的方法、操作和和相应的控件。

> [!TIP]
> 当选择位于 **“UI 操作”** 窗格中的方法中的 UI 操作时，将突出显示相应的控件。 你还可以修改 UI 操作或控件属性。

## <a name="modify-ui-action-and-control-properties"></a>修改 UI 操作和控件属性

使用编码的 UI 测试编辑器，你可以快速查找和查看测试方法中所有的 UI 操作。 当在编辑器中选择的 UI 操作时，将自动突出显示相应的控件。 同样，如果选择一个控件，将突出显示相关联的 UI 操作。 这样，当选择 UI 操作或控件时，就可以轻松通过“属性”窗口来修改与之相对应的属性。

![UI 操作属性](../test/media/codeduiedituiaction.png)

若要修改 UI 操作的属性，在 **“UI 操作”** 窗格中，展开包含你想要为其编辑属性的 UI 操作的测试方法，选择 UI 操作，然后通过“属性”窗口修改属性。

例如，如果服务器不可用，并且 UI 操作与指示“转到网页 '<http://Contoso1/default.aspx>'”的 Web 浏览器关联，则可以将 URL 更改为 `'http://Contoso2/default.aspx'`。

![控件属性](../test/media/codeduitestcontrolprop.png)

修改控件属性的方式与 UI 操作的方式相同。 在“UI 控件图”窗格中，选择你想使用“属性”窗口编辑和修改器属性的控件。

例如，开发人员可能已将某个按钮控件上的 (ID) 属性从“idSubmit”更改为“idLogin”，此按钮控件位于正在测试的应用程序源代码中。 应用程序中的“(ID)” **(ID)** 属性更改后，编码的 UI 测试将无法查找按钮控件且会失败。 在这种情况下，测试人员可以打开 **“搜索属性”** 集合，并更改 **“Id”** 属性以匹配开发人员在应用程序中使用的新值。 测试人员还可以将“友好名称”属性值从“提交”更改为“登录”。 通过进行此更改，更新了编码的 UI 测试编辑器中关联的 UI 操作，从“选择‘提交’按钮”更改为“选择‘登录’按钮”。

完成修改后，通过选择 Visual Studio 工具栏上的“保存”，将所做更改保存到“UIMap.Designer”文件。

### <a name="tips"></a>提示

- 如果未显示“属性”窗口，请在按 Enter 的同时按住 Alt，或者按 F4。

- 若要撤消所做的属性更改，请选择“编辑”菜单中的“撤消”或按 Ctrl+Z。

- 可以使用编码的 UI 测试编辑器工具栏中的“查找”按钮打开 Visual Studio 中的“查找和替换”工具。 然后可以使用“查找”控件查找编码的 UI 测试编辑器中的 UI 操作。 例如，可以尝试查找“单击‘登录’按钮”。 这在大型测试中十分有用。 不能使用编码的 UI 测试编辑器中“查找和替换”工具中的替换功能。 有关详细信息，请参阅[查找和替换文本](../ide/finding-and-replacing-text.md)中的“查找控件”。

- 有时，可能很难直观显示控件在受测应用程序 UI 中的位置。 编码的 UI 测试编辑器的功能之一是，你可以选择 UI 控件图中列出的控件和查看其在受测应用程序中的位置。 有关详细信息，请参阅本文后面的[在受测应用程序中查找 UI 控件](#locate-a-ui-control-in-the-application-under-test)。

- 可能有必要展开包含你要编辑的控件的容器控件。 有关详细信息，请参阅本文后面的[查找控件及其后代](#locate-a-control-and-its-descendants)。

## <a name="delete-unwanted-ui-actions"></a>删除不需要的 UI 操作

在编码的 UI 测试中，可以轻松删除不需要的 UI 操作。

![删除 UI 操作](../test/media/codeduideleteuiaction.png)

在“UI 操作”  窗格中，展开包含想要删除的 UI 操作的测试方法。 打开 UI 操作的快捷菜单，然后选择“删除” 。

## <a name="split-a-test-method-into-two-separate-methods"></a>将测试方法拆分为两个不同方法

你可以拆分测试方法，以优化或模块化 UI 操作。 例如，你的测试可能只有一个测试方法，而 UI 操作则位于两个容器控件中。 建议最好将 UI 操作在两个方法中进行模块化，与一个容器相符。

![拆分测试方法](../test/media/codeduitestsplitmethod1.png)

![两种测试方法](../test/media/codeduitestsplitmethod2.png)

在“UI 操作”  窗格中，展开你想要拆分为两个不同方法的测试方法，然后选择 UI 操作，在其中开始新的测试方法。 可以打开 UI 操作的快捷菜单，然后选择“拆分成新方法” ，也可以选择编码的 UI 测试编辑器工具栏上的“拆分成新方法”  按钮。 新的测试方法将显示在“UI 操作”窗格中。 它包含 UI 操作，从指定拆分的操作开始进行。

拆分方法后，通过选择 Visual Studio 工具栏上的“保存”，可将所做更改保存到“UIMap.Designer”文件。

> [!WARNING]
> 如果拆分方法，则必须修改可调用现有方法的任何代码，使其在你仍然想要包括这些 UI 操作时也可以调用要创建的新方法。 拆分方法时，将显示一个 Microsoft Visual Studio 对话框。 它会警告你必须修改可调用现有方法的任何代码，使其还可以调用要创建的新方法。 选择 **“是”**。

### <a name="tips"></a>提示

- 若要撤消拆分，请选择“编辑”菜单中的“撤消”或按 Ctrl+Z。

- 你可以重命名新方法。 在“UI 操作”窗格中选择它，然后选择编码的 UI 测试编辑器工具栏中的“重命名”按钮。

   或

   打开新测试方法的快捷菜单，并选择“重命名” 。

   将显示一个 Microsoft Visual Studio 对话框。 它会警告你，必须修改引用该方法的任何代码。 选择 **“是”**。

## <a name="move-a-test-method-to-the-uimap-file-to-facilitate-customization"></a>将测试方法移动到 UIMap 文件以便于自定义

如果确定编码的 UI 测试中的其中一种测试方法需要自定义代码，则必须将其移动到“UIMap.cs”或“UIMap.vb”文件。 否则，只要编码的 UI 测试被重新编译，你的代码就会被重写。 如果不移动方法，则每次重新编译测试时都会重写你的自定义代码。

在“UI 操作”窗格中，选择要移动到“UIMap.cs”或“UIMap.vb ”文件的测试方法，以便在重新编译测试代码时不会覆盖自定义代码功能。 接下来，选择编码的 UI 测试编辑器工具栏上的“移动代码”  按钮，或打开测试方法的快捷菜单，然后选择“移动代码” 。 将从“UIMap.uitest”文件中移除该测试方法，并且“UI 操作”窗格中不再显示该测试方法。 若要编辑移动的测试文件，请从“解决方案资源管理器”中打开“UIMap.cs”或“UIMap.vb”文件。

移动方法后，选择 Visual Studio 工具栏上的“保存”，可将所做更改保存到“UIMap.Designer”文件。

> [!WARNING]
> 移动该方法后，就不再能使用编码的 UI 测试编辑器对其进行编辑。 你必须使用代码编辑器添加并维护你的自定义代码。 移动方法时，将显示一个 Microsoft Visual Studio 对话框。 该对话框将警告你，该方法将从“UIMap.uitest”文件移动到“UIMap.cs”或“UIMap.vb”文件，并且你将不能再使用编码的 UI 测试编辑器来编辑该方法。 选择 **“是”**。

### <a name="tips"></a>提示

若要撤消移动，请选择“编辑”菜单中的“撤消”或按 Ctrl+Z。 但是，随后必须手动从“UIMap.cs”或“UIMap.vb ”文件删除该代码。

## <a name="locate-a-ui-control-in-the-application-under-test"></a>在受测应用程序中查找 UI 控件

有时，可能很难直观显示控件在受测应用程序 UI 中的位置。 编码的 UI 测试编辑器的功能之一是，你可以选择 UI 控件图中列出的控件和查看其在受测应用程序中的位置。 受测应用程序中的“查找 UI 控件”  功能还可以用于验证你对控件所做的搜索属性修改。

![定位 UI 控件](../test/media/codeduilocatecontrol.png)

![位于正在接受测试的应用程序中的控件](../test/media/codeduilocatecontrol2.png)

在“UI 控件图”  窗格中，选择你想要在与测试关联的应用程序中查找的控件。 接下来，打开该控件的快捷菜单，然后选择“查找 UI 控件” 。 在受测应用程序中，为该控件指定了一个蓝色边框。

> [!NOTE]
> 查找 UI 控件之前，请验证与测试关联的应用程序是否正在运行。

### <a name="tips"></a>提示

可以使用“查找全部”选项验证是否可以准确查找容器中的所有控件。 下一部分中对此选项进行了介绍。

## <a name="locate-a-control-and-its-descendants"></a>查找控件及其后代

你可以验证是否可以在受测应用程序的 UI 中准确查找容器中的所有控件。 这对于验证你对容器所做的搜索属性更改非常有帮助。 此外，如果对受测应用程序的 UI 进行了重大更改，你可以验证现有的控件搜索属性是否仍正确。

![定位所有后代控件](../test/media/codeduilocateall.png)

![找到的所有控件](../test/media/codeduilocateall2.png)

在“UI 控件图”  窗格中，选择你想要为其查找和查看所有后代的容器控件。 接下来，打开该控件的快捷菜单，然后选择“查找全部” 。 在编码的 UI 测试编辑器中，容器控件及其所有后代控件都有一个绿色复选标记或红色“X”标记。 这些标记可让你知道是否可以在受测应用程序中成功查找这些控件。

> [!NOTE]
> 查找 UI 控件之前，请验证与测试关联的应用程序是否正在运行。

## <a name="insert-a-delay-before-a-ui-action"></a>在 UI 操作前插入延迟

有时，可能需要让测试等待某些事件发生，如某个窗口出现、进度栏消失等。 使用编码的 UI 测试编辑器，你可以通过在 UI 操作之前插入延迟完成此操作。 你可以指定希望延迟的秒数。

![在 UI 操作前插入延迟](../test/media/codeduidelay.png)

![延迟时间增加 5 秒](../test/media/codeduidealy2.png)

在“UI 操作”  窗格中，展开包含你想要在其前插入延迟的 UI 操作的测试方法。 选择 UI 操作。 接下来，打开 UI 操作的快捷菜单，然后选择“在前面插入延迟” 。 在所选 UI 操作之前插入并突出显示具有以下文本的延迟：“为操作之间的用户延迟等待 1 秒”。 在“属性”窗口中，将“延迟”属性的值更改为所需的毫秒数。

插入延迟后，选择 Visual Studio 工具栏上的“保存”，可将所做更改保存到“UIMap.Designer”文件。

如果需要确保特定控件在 UI 操作之前可用，应考虑使用相应的 uitestcontrol.waitforcontrolxxx () 方法将自定义代码添加到你的测试方法。 有关详细信息，请参阅[播放期间让编码的 UI 测试等待特定事件](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md)。

## <a name="see-also"></a>请参阅

- [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)
- [创建编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md)
- [创建数据驱动的编码 UI 测试](../test/creating-a-data-driven-coded-ui-test.md)
- [演练：创建、编辑和维护编码的 UI 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)