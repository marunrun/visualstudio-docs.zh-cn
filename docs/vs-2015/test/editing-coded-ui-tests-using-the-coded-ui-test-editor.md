---
title: 使用编码的 UI 测试编辑器编辑编码的 UI 测试 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
f1_keywords:
- vs.codedUItest.testeditor
helpviewer_keywords:
- coded UI test, Coded UI Test Editor
ms.assetid: 76435c4b-593e-43a3-a9fe-709a7f9f5e0f
caps.latest.revision: 42
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c070f1bafb157e3979eb9c1f49b317b17807f1e7
ms.sourcegitcommit: da5ebc29544fdbdf625ab4922c9777faf2bcae4a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2020
ms.locfileid: "82586998"
---
# <a name="editing-coded-ui-tests-using-the-coded-ui-test-editor"></a>使用编码的 UI 测试编辑器编辑编码的 UI 测试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过编码的 UI 测试编辑器，可轻松修改编码的 UI 测试。 使用编码的 UI 测试编辑器，可以查找、查看和编辑测试方法和 UI 操作的属性。 此外，你还可以使用 UI 控件图查看和编辑其对应的控件。

 **要求**

- Visual Studio Enterprise

## <a name="why-should-i-do-this"></a>为什么应这样做?
 使用编码的 UI 测试编辑器比使用代码编辑器在编码的 UI 测试方法中编辑代码速度更快，效率更高。 使用编码的 UI 测试编辑器，可以使用工具栏和快捷菜单快速查找和修改与 UI 操作和控件相关联的属性值。 例如，可以使用编码的 UI 测试编辑器的工具栏执行以下命令：

 ![UI 测试编辑器](../test/media/uitesteditor.png "UITestEditor")

1. “[查找](../ide/finding-and-replacing-text.md)”有助于查找 UI 操作和控件。

2. [删除](#CodedUITestEditor_DeleteUIActions) 可删除不想要的 UI 操作。

3. **重命名** 可以更改测试方法和控件的名称。

4. **属性** 可以打开所选项的属性窗口。

5. [拆分成新方法](#CodedUITestEditor_SplitMethods) 可以模块化 UI 操作。

6. [移动代码](#CodedUITestEditor_MoveMethods) 可以将自定义代码添加到你的测试方法。

7. [在前面插入延迟](#CodedUITestEditor_InsertDelay) 可以在执行 UI 操作之前添加暂停，以毫秒为单位。

8. [查找 UI 控件](#CodedUITestEditor_LocateUIControl) 可识别待测试应用程序的 UI 中控件的位置。

9. "[查找全部](#CodedUITestEditor_LocateDecendants)" 有助于验证控件属性和对应用程序控件的重大更改。

## <a name="how-do-i-do-this"></a>如何操作？
 在 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]中，打开与编码的 UI 测试项目中编码的 UI 测试关联的 UIMap.uitest 文件将自动在编码的 UI 测试编辑器中显示编码的 UI 测试。 下面的过程介绍了随后如何使用编辑器工具栏和快捷菜单查找和编辑测试方法、UI 操作的属性和控件。

## <a name="open-a-coded-ui-test"></a>打开编码的 UI 测试
 你可以使用编码的 UI 测试编辑器查看和编辑基于 Visual C# 和 Visual Basic 的编码的 UI 测试。

 ![“编码的 UI 测试生成器”的“编辑”上下文菜单](../test/media/editcodeduitest.png "EditCodedUITest")

 在解决方案资源管理器中，打开**uitest**的快捷菜单，然后选择 "**打开**"。 编码的 UI 测试编辑器中将显示编码的 UI 测试。 现在，你可以查看和编辑编码的 UI 测试中记录的方法、操作和和相应的控件。

> [!TIP]
> 当选择位于 **“UI 操作”** 窗格中的方法中的 UI 操作时，将突出显示相应的控件。 你还可以修改 UI 操作或控件属性。

 *我看不到* 编码的 UI 测试编辑器。
你可能正在使用的 Visual Studio Enterprise 2012 之前的版本。 订阅 MSDN 的 Visual Studio 2010 功能包 2 中也提供编码的 UI 测试编辑器。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Microsoft Visual Studio 2010 功能包 2](https://msdn.microsoft.com/library/gg269474.aspx)。

## <a name="modify-ui-action-properties-and-their-corresponding-control-properties"></a><a name="CodedUITestEditor_EditActionAndControlProperties"></a> 修改 UI 操作属性及其对应的控件属性
 使用编码的 UI 测试编辑器，你可以快速查找和查看测试方法中所有的 UI 操作。 当在编辑器中选择的 UI 操作时，将自动突出显示相应的控件。 同样，如果选择一个控件，将突出显示相关联的 UI 操作。 这样，当选择 UI 操作或控件时，就可以轻松通过“属性”窗口来修改与之相对应的属性。

 ![UI 操作属性](../test/media/codeduiedituiaction.png "CodedUIEditUIAction")编辑 UI 操作属性

 若要修改 UI 操作的属性，在 **“UI 操作”** 窗格中，展开包含你想要为其编辑属性的 UI 操作的测试方法，选择 UI 操作，然后通过“属性”窗口修改属性。

 例如，如果服务器不可用，并且 UI 操作与指示“转到网页 <http://Contoso1/default.aspx’>”的 Web 浏览器关联，则可以将 URL 更改为 `‘http://Contoso2/default.aspx’`****。

 ![控件属性](../test/media/codeduitestcontrolprop.png "CodedUITestControlProp")编辑控件属性

 修改控件属性的方式与 UI 操作的方式相同。 在 " **UI 控件图**" 窗格中，选择要编辑的控件，并使用属性窗口修改其属性。

 例如，开发人员可能已更改从 "idSubmit" 到 "idLogin" 测试的应用程序源代码中的按钮控件上的 **（ID）** 属性。 应用程序中的“(ID)” **(ID)** 属性更改后，编码的 UI 测试将无法查找按钮控件且会失败。 在这种情况下，测试人员可以打开 **“搜索属性”** 集合，并更改 **“Id”** 属性以匹配开发人员在应用程序中使用的新值。 测试人员还可以将 "**友好名称**" 属性值从 "提交" 更改为 "Login"。 通过进行此更改，编码的 UI 测试编辑器中关联的 UI 操作的“选择‘提交’按钮”已更改为“选择‘登录’按钮”。

 完成修改后，通过更改 **工具栏上的“保存”**[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，将所做更改保存到 UIMap.Designer 文件。

 *我应该知道哪些其他内容？*
 **提示**

- ![提示](../test/media/tip.png "提示")如果属性窗口未显示，请在按住**Alt**的同时按**enter**，或者按**F4**。

- ![提示](../test/media/tip.png "提示")若要撤消所做的属性更改，请从 "**编辑**" 菜单中选择 "**撤消**"，或按 Ctrl + Z。

- ![提示](../test/media/tip.png "提示")您可以使用编码的 UI 测试编辑器工具栏中的 "**查找**" 按钮打开 Visual Studio 中的 "查找和替换" 工具。 然后可以使用“查找”控件查找编码的 UI 测试编辑器中的 UI 操作。 例如，你可以尝试查找“单击‘登录’按钮”。 这在大型测试中十分有用。 请注意，不能使用编码的 UI 测试编辑器中“查找和替换”工具中的替换功能。 有关详细信息，请参阅 [Finding and Replacing Text](../ide/finding-and-replacing-text.md)中的“查找控件”。

- ![提示](../test/media/tip.png "提示")有时，可能很难直观显示控件在受测应用程序 UI 中的位置。 编码的 UI 测试编辑器的功能之一是，你可以选择 UI 控件图中列出的控件和查看其在受测应用程序中的位置。 [!INCLUDE[crdefault](../includes/crdefault-md.md)]本主题后面的[在受测应用中查找 UI 控件](#CodedUITestEditor_LocateUIControl)。

- ![提示](../test/media/tip.png "提示")可能需要展开包含要编辑的控件的容器控件。 [!INCLUDE[crdefault](../includes/crdefault-md.md)]本主题后面的[查找控件及其后代](#CodedUITestEditor_LocateDecendants)。

## <a name="delete-unwanted-ui-actions"></a><a name="CodedUITestEditor_DeleteUIActions"></a>删除不需要的 UI 操作
 在编码的 UI 测试中，可以轻松删除不需要的 UI 操作。

 ![删除 UI 操作](../test/media/codeduideleteuiaction.png "CodedUIDeleteUIAction")

 在“UI 操作”  窗格中，展开包含想要删除的 UI 操作的测试方法。 打开 UI 操作的快捷菜单，然后选择“删除”  。

## <a name="split-a-test-method-into-two-separate-methods"></a><a name="CodedUITestEditor_SplitMethods"></a>将测试方法拆分为两个不同的方法
 你可以拆分测试方法，以优化或模块化 UI 操作。 例如，你的测试可能只有一个测试方法，而 UI 操作则位于两个容器控件中。 建议最好将 UI 操作在两个方法中进行模块化，与一个容器相符。

 ![拆分测试方法](../test/media/codeduitestsplitmethod1.png "CodedUITestSplitMethod1")

 ![两种测试方法](../test/media/codeduitestsplitmethod2.png "CodedUITestSplitMethod2")

 在“UI 操作”  窗格中，展开你想要拆分为两个不同方法的测试方法，然后选择 UI 操作，在其中开始新的测试方法。 可以打开 UI 操作的快捷菜单，然后选择“拆分成新方法”  ，也可以选择编码的 UI 测试编辑器工具栏上的“拆分成新方法”  按钮。 新的测试方法将显示在“UI 操作”窗格中。 它包含 UI 操作，从指定拆分的操作开始进行。

 拆分方法完成后，通过选择 **工具栏上的“保存”**[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，可将所做更改保存到 UIMap.Designer 文件。

 *我应该知道哪些其他内容？*
 **重要事项**

- 警告![图标](../test/media/caution.gif "注意")**警告：** 如果你拆分方法，则必须修改调用现有方法的任何代码，以便还在你仍想要包括这些 UI 操作时调用要创建的新方法。 拆分方法时，将显示一个 Microsoft Visual Studio 对话框。 它会警告你必须修改可调用现有方法的任何代码，使其还可以调用要创建的新方法。 选择 **“是”** 。

  **提示**

- ![提示](../test/media/tip.png "提示")若要撤消拆分，请从 "**编辑**" 菜单中选择 "**撤消**"，或按 Ctrl + Z。

- ![提示](../test/media/tip.png "提示")您可以重命名新方法。 在 "UI 操作" 窗格中选择它，然后选择编码的 UI 测试编辑器工具栏中的 "**重命名**" 按钮。

   \- 或 -

   打开新测试方法的快捷菜单，并选择“重命名”  。

   将显示一个 Microsoft Visual Studio 对话框。 它会警告你，必须修改引用该方法的任何代码。 选择 **“是”** 。

## <a name="move-a-test-method-to-the-uimap-file-to-facilitate-customization"></a><a name="CodedUITestEditor_MoveMethods"></a>将测试方法移动到 UIMap 文件以便于自定义
 如果确定编码的 UI 测试中的其中一种测试方法需要自定义代码，则必须将其移动到 UIMap.cs 或 UIMap.vb 文件。 否则，只要编码的 UI 测试被重新编译，你的代码就会被重写。 如果不移动方法，则每次重新编译测试时都会重写你的自定义代码。

 在 " **UI 操作**" 窗格中，选择要移动到 UIMap.cs 或 UIMap 文件的测试方法，以便在重新编译测试代码时不会覆盖自定义代码功能。 接下来，选择编码的 UI 测试编辑器工具栏上的“移动代码”  按钮，或打开测试方法的快捷菜单，然后选择“移动代码”  。 将从 UIMap.uitest 文件中移除该测试方法，并且“UI 操作”窗格中将不再显示该测试方法。 若要编辑移动的测试文件，请从解决方案资源管理器中打开 UIMap.cs 或 UIMap.vb 文件。

 移动方法后，通过选择 **工具栏上的“保存”**[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，可将所做更改保存到 UIMap.Designer 文件。

 *我应该知道哪些其他内容？*
 **重要事项**

- 警告![图标](../test/media/caution.gif "注意")**警告：** 一旦移动了方法，就不能再使用编码的 UI 测试编辑器对其进行编辑。 你必须使用代码编辑器添加并维护你的自定义代码。 移动方法时，将显示一个 Microsoft Visual Studio 对话框。 该对话框将警告你，该方法将从 UIMap.uitest 文件移动到 UIMap.cs 或 UIMap.vb 文件，并且你将不能再使用编码的 UI 测试编辑器来编辑该方法。 选择 **“是”** 。

  **提示**

- ![提示](../test/media/tip.png "提示")若要撤消移动，请从 "**编辑**" 菜单中选择 "**撤消**"，或按 Ctrl + Z。 但是，随后必须手动从 UIMap.cs 或 UIMap.vb 文件删除该代码。

## <a name="locating-a-ui-control-in-the-application-under-test"></a><a name="CodedUITestEditor_LocateUIControl"></a>在受测应用程序中查找 UI 控件
 有时，可能很难直观显示控件在受测应用程序 UI 中的位置。 编码的 UI 测试编辑器的功能之一是，你可以选择 UI 控件图中列出的控件和查看其在受测应用程序中的位置。 受测应用程序中的“查找 UI 控件”  功能还可以用于验证你对控件所做的搜索属性修改。

 ![定位 UI 控件](../test/media/codeduilocatecontrol.png "CodedUILocateControl")

 ![位于正在接受测试的应用程序中的控件](../test/media/codeduilocatecontrol2.png "CodedUILocateControl2")

 在“UI 控件图”  窗格中，选择你想要在与测试关联的应用程序中查找的控件。 接下来，打开该控件的快捷菜单，然后选择“查找 UI 控件”  。 在受测应用程序中，为该控件指定了一个蓝色边框。

 *我应该知道哪些其他内容？*
 **重要事项**

- 警告![图标](../test/media/caution.gif "注意")**警告：** 查找 UI 控件之前，请验证与测试关联的应用程序是否正在运行。

  **提示**

- ![提示](../test/media/tip.png "提示")或者，您可以使用 "**查找全部**" 选项验证容器下的所有控件是否可以正确定位。 下一部分中对此选项进行了介绍。

## <a name="locating-a-control-and-its-descendants"></a><a name="CodedUITestEditor_LocateDecendants"></a>查找控件及其后代
 你可以验证是否可以在受测应用程序的 UI 中准确查找容器中的所有控件。 这对于验证你对容器所做的搜索属性更改非常有帮助。 此外，如果对受测应用程序的 UI 进行了重大更改，你可以验证现有的控件搜索属性是否仍正确。

 ![定位所有后代控件](../test/media/codeduilocateall.png "CodedUILocateAll")

 ![找到的所有控件](../test/media/codeduilocateall2.png "CodedUILocateAll2")

 在“UI 控件图”  窗格中，选择你想要为其查找和查看所有后代的容器控件。 接下来，打开该控件的快捷菜单，然后选择“查找全部”  。 容器控件及其所有后代控件在编码的 UI 测试编辑器标记为一个绿色复选标记或红色 X。 这些标记可让你知道是否可以在受测应用程序中成功查找这些控件。

 *我应该知道哪些其他内容？*
 **重要事项**

- 警告![图标](../test/media/caution.gif "注意")**警告：** 在定位 UI 控件之前，请验证与测试关联的应用程序是否正在运行。

## <a name="inserting-a-delay-before-a-ui-action"></a><a name="CodedUITestEditor_InsertDelay"></a> 在 UI 操作之前插入延迟
 有时，可能需要让测试等待某些事件发生，如某个窗口出现、进度栏消失等。 使用编码的 UI 测试编辑器，你可以通过在 UI 操作之前插入延迟完成此操作。 你可以指定希望延迟的秒数。

 ![在 UI 操作前插入延迟](../test/media/codeduidelay.png "CodedUIDelay")

 ![延迟时间增加 5 秒](../test/media/codeduidealy2.png "CodedUIDealy2")

 在“UI 操作”  窗格中，展开包含你想要在其前插入延迟的 UI 操作的测试方法。 选择 UI 操作。 接下来，打开 UI 操作的快捷菜单，然后选择“在前面插入延迟”  。 在所选 UI 操作之前插入并突出显示具有以下文本的延迟：“为操作之间的用户延迟等待 1 秒”  。 在属性窗口中，将 "**延迟**" 属性的值更改为所需的毫秒数。

 插入延迟完成后，通过选择 **工具栏上的“保存”**[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，将所做更改保存到 UIMap.Designer 文件。

 *我应该知道哪些其他内容？*
 **说明**

- ![先决条件](../test/media/prereq.png "Prereq")如果需要确保特定控件在 UI 操作之前可用，应考虑使用相应的的 uitestcontrol.waitforcontrolxxx Uitestcontrol.waitforcontrolxxx （）方法将自定义代码添加到测试方法。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Making Coded UI Tests Wait For Specific Events During Playback](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md)。

  **提示**

- ![提示](../test/media/tip.png "提示")如果属性窗口未显示，请在按住 Alt 的同时按 Enter，或者按 F4。

## <a name="external-resources"></a>外部资源

### <a name="guidance"></a>指南
 [通过 Visual Studio 2012 对持续交付进行测试-第2章：单元测试：测试内部](https://msdn.microsoft.com/library/jj159340.aspx)

### <a name="faq"></a>常见问题解答
 [编码的 UI 测试常见问题 - 1](https://docs.microsoft.com/archive/blogs/mathew_aniyan/content-index-for-coded-ui-test)

 [编码的 UI 测试常见问题 - 2](https://social.msdn.microsoft.com/Forums/en-US/vsautotest/thread/3a74dd2c-cef8-4923-abbf-7a91f489e6c4)

### <a name="forum"></a>论坛
 [Visual Studio UI 自动测试（包括 CodedUI）](https://social.msdn.microsoft.com/Forums/en-US/vsautotest)

## <a name="see-also"></a>另请参阅
 [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)[创建编码](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)[的](../test/creating-a-data-driven-coded-ui-test.md)ui 测试创建编码的 ui 测试[从现有操作录制生成编码的 ui](https://msdn.microsoft.com/library/56736963-9027-493b-b5c4-2d4e86d1d497)测试[演练：创建、编辑和维护编码的 ui 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
