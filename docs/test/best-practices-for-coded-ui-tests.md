---
title: 编码的 UI 测试的最佳做法
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- coded UI tests, best practices
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 896531325b3630b97a5cc076955fae6201defac6
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68870207"
---
# <a name="best-practices-for-coded-ui-tests"></a>编码的 UI 测试的最佳做法

本主题介绍有关开发编码的 UI 测试的一些建议。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="best-practices"></a>最佳实践

使用以下准则来创建灵活的编码的 UI 测试。

- 尽可能使用**编码的 UI 测试生成器**。

- 请不要直接修改 UIMap.Designer.cs 文件  。 如果修改该文件，会覆盖对该文件的更改。

- 将测试创建为一系列记录的方法。 若要详细了解如何录制方法，请参阅[创建编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md)。

- 每个记录的方法应作用于单个页面、窗体或对话框。 为每个新页面、窗体或对话框创建新测试方法。

- 创建方法时，请使用有意义的方法名称，而不是默认名称。 有意义的名称有助于标识方法的用途。

- 如果可能，将每个记录的方法限制为少于 10 次操作。 这种模块化方法便于在 UI 更改时替换方法。

- 使用“编码的 UI 测试生成器”创建每个断言，这会自动向 UIMap.Designer.cs 文件添加断言方法   。

- 如果用户界面 (UI) 更改，请重新记录测试方法或断言方法，或重新记录现有测试方法中受影响的部分。

- 为受测应用程序中的每个模块创建一个单独的 [UIMap](/previous-versions/dd580454(v=vs.140)) 文件。 有关详细信息，请参阅[使用多个 UI 映射测试大型应用程序](../test/testing-a-large-application-with-multiple-ui-maps.md)。

- 在受测应用程序中创建 UI 控件时，请使用有意义的名称。 使用有意义的名称比自动生成的控件名称更清晰，更易于使用。

- 如果通过用 API 编码来创建断言，请为 UIMap.cs  文件中 [UIMap](/previous-versions/dd580454(v=vs.140)) 类部分中的每个断言创建一个方法。 若要执行断言，请从测试方法中调用此方法。

- 如果直接用 API 编码，请在代码中尽可能使用 UIMap.Designer.cs 文件中生成的类中的属性和方法  。 这些类将使您的工作更简单可靠，并帮助您提高效率。

编码的 UI 测试能够自动适应用户界面中的许多更改。 例如，在大多数情况下，如果 UI 元素更改了位置或颜色，则编码的 UI 测试仍将找到正确的元素。

在测试运行期间，测试框架使用一组搜索属性来定位 UI 控件。 搜索属性应用于“编码的 UI 测试生成器”在 UIMap.Designer.cs 文件中创建的定义中的每个控件类   。 搜索属性包含可用于标识控件的属性名称和属性值的名称-值对，例如控件的 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.FriendlyName%2A>、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.Name%2A> 和 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.ControlType%2A> 属性。 如果搜索属性未更改，则编码的 UI 测试会在 UI 中成功找到控件。 如果搜索属性发生更改，编码的 UI 测试会使用一个智能匹配算法，应用试探方法在 UI 中查找控件和窗口。 当 UI 已更改时，你或许能够修改以前标识的元素的搜索属性，以确保能够找到这些元素。

## <a name="if-your-user-interface-changes"></a>如果用户界面发生更改

在开发过程中，用户界面经常更改。 下面提供了一些可以降低这些更改的影响的方法：

- 查找引用此控件的已录制方法，并使用“编码的 UI 测试生成器”重新录制此方法的操作  。 可对方法使用同一名称，以覆盖现有操作。

- 如果控件有一个不再有效的断言，则执行下列操作：

  - 删除包含断言的方法。

  - 从测试方法中删除对此方法的调用。

  - 通过将十字线按钮拖动到 UI 控件上来添加新的断言，打开 UI 映射，并添加新的断言。

若要详细了解如何录制编码的 UI 测试，请参阅[使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)。

## <a name="if-a-background-process-needs-to-complete-before-the-test-can-continue"></a>如果需要先完成后台进程然后测试才能继续

可能必须等到进程完成，然后才能继续下一个 UI 操作。 为此，可以使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.WaitForReadyLevel%2A> 在测试继续之前等待，如以下示例所示：

```csharp
// Set the playback to wait for all threads to finish
Playback.PlaybackSettings.WaitForReadyLevel = WaitForReadyLevel.AllThreads;

// Press the submit button
this.UIMap.ClickSubmit();

// Reset the playback to wait only for the UI thread to finish
Playback.PlaybackSettings.WaitForReadyLevel = WaitForReadyLevel.UIThreadOnly;
```

## <a name="see-also"></a>请参阅

- [UIMap](/previous-versions/dd580454(v=vs.140))
- <xref:Microsoft.VisualStudio.TestTools.UITesting>
- [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)
- [创建编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md)
- [使用多个 UI 映射测试大型应用程序](../test/testing-a-large-application-with-multiple-ui-maps.md)
- [支持编码的 UI 测试和操作录制的配置和平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
