---
title: 让编码 UI 测试等待特定事件
ms.date: 11/04/2016
ms.topic: conceptual
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: df1e664b8574b5c362b57733dba63f45cc04cd1d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652952"
---
# <a name="make-coded-ui-tests-wait-for-specific-events-during-playback"></a>播放期间让编码 UI 测试等待特定事件

在编码的 UI 测试播放中，你可以指示测试等待某些事件发生，如某个窗口出现、进度栏消失等。 为此，请使用合适的 UITestControl.WaitForControlXXX() 方法，如下表中所述。 有关使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlEnabled%2A> 方法等待启用某个控件的编码的 UI 测试示例，请参阅[演练：创建、编辑和维护编码的 UI 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**要求**

Visual Studio Enterprise

> [!TIP]
> 使用编码的 UI 测试编辑器，还可以在操作之前添加延迟。 有关详细信息，请参阅[如何：使用编码的 UI 测试编辑器在 UI 操作之前插入延迟](editing-coded-ui-tests-using-the-coded-ui-test-editor.md#insert-a-delay-before-a-ui-action)。

**UITestControl.WaitForControlXXX() 方法**

<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlReady%2A>

等待控件准备好接受鼠标和键盘输入。 引擎会对所有操作隐式调用此 API 以在执行任何操作之前等待控件准备就绪。 但是在某些复杂方案中，可能需要进行显式调用。

<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlEnabled%2A>

在向导通过对服务器进行调用来执行输入的某种异步验证时，等待控件启用。 例如，可以执行方法以等待启用向导的“下一步”按钮。  有关此方法的示例，请参阅[演练：创建、编辑和维护编码的 UI 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)。

<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlExist%2A>

等待控件出现在 UI 上。 例如，你期望在应用程序完成参数验证之后出现一个错误对话框。 验证所需的时间是可变的。 可以使用此方法等待该错误对话框。

<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlNotExist%2A>

等待控件从 UI 中消失。 例如，可以等待进度栏消失。

<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlPropertyEqual%2A>

等待控件的指定属性具有给定值。 例如，等待状态文本更改为“完成”。 

<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlPropertyNotEqual%2A>

等待控件的指定属性具有与给定值相反的值。 例如，等待编辑框不是只读（即，可编辑）。

<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlCondition%2A>

等待指定谓词返回为 `true`。 这可以用于对给定控件执行的复杂等待操作（如 OR 条件）。 例如，可以等到状态文本为“成功”或“失败”，如下面的代码中所示：  

```csharp

// Define the method to evaluate the condition
private static bool IsStatusDone(UITestControl control)
{
    WinText statusText = control as WinText;
    return statusText.DisplayText == "Succeeded" || statusText.DisplayText == "Failed";
}

// In test method, wait till the method evaluates to true
statusText.WaitForControlCondition(IsStatusDone);
```

 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForCondition%2A>

前面的所有方法都是 UITestControl 的实例方法。 此方法是静态方法。 此方法也等待指定谓词为 `true`，但它可以用于对多个控件执行的复杂等待操作（如 OR 条件）。 例如，可以等到状态文本为“成功”或等到错误消息出现，如下面的代码中所示： 

```csharp

// Define the method to evaluate the condition
private static bool IsStatusDoneOrError(UITestControl[] controls)
{
    WinText statusText = controls[0] as WinText;
    WinWindow errorDialog = controls[1] as WinWindow;
    return statusText.DisplayText == "Succeeded" || errorDialog.Exists;
}

// In test method, wait till the method evaluates to true
UITestControl.WaitForCondition<UITestControl[]>(new UITestControl[] { statusText, errorDialog }, IsStatusDoneOrError);
```

所有这些方法都具有以下行为：

如果等待失败，则方法返回 true，如果等待失败，则返回 false。

等待操作的隐式超时由 <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.WaitForReadyTimeout%2A> 属性指定。 此属性的默认值是 60000 毫秒（1 分钟）。

这些方法具有采用显式超时（以毫秒为单位）的重载。 但是，当等待操作导致对控件进行隐式搜索时，或是当应用程序繁忙时，实际等待时间可能会多于指定超时。

前面的函数强大且灵活，应该可满足几乎所有情况。 但是，如果这些方法不能满足你的需求，并且你需要在代码中对 <xref:Microsoft.VisualStudio.TestTools.UITesting.Playback.Wait%2A> 或 <xref:System.Threading.Thread.Sleep%2A> 进行编码，则建议你使用 Playback.Wait()，而不是 Thread.Sleep() API。 这样做的原因是：

可以使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.ThinkTimeMultiplier%2A> 属性修改睡眠的持续时间。 默认情况下，此变量是 1，但可以增大或减小它以更改整个代码的等待时间。 例如，如果要专门在慢速网络上进行测试或是测试某种其他的慢速性能情况，则可以在一个位置（甚至是在配置文件中）将此变量更改为 1.5，以在所有位置增加 50% 的额外等待。

Playback.Wait() 采用 For 循环在较小区块中内部调用 Thread.Sleep()（进行以上计算之后），同时检查是否存在用户取消\中断操作。 换句话说，Playback.Wait() 使你可以在等待结束之前取消播放，而睡眠可能会也可能不会引发异常。

> [!TIP]
> 通过编码的 UI 测试编辑器，可轻松修改编码的 UI 测试。 使用编码的 UI 测试编辑器，可以查找、查看和编辑测试方法。 也可以在 UI 控件映射中编辑 UI 操作及其关联的控件。 有关详细信息，请参阅[使用编码的 UI 测试编辑器编辑编码的 UI 测试](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)。

## <a name="see-also"></a>请参阅

- [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)
- [创建编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md)
- [演练：创建、编辑和维护编码的 UI 测试](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
- [编码的 UI 测试剖析](../test/anatomy-of-a-coded-ui-test.md)
- [支持编码的 UI 测试和操作录制的配置和平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
- [如何：使用编码的 UI 测试编辑器在 UI 操作之前插入延迟](editing-coded-ui-tests-using-the-coded-ui-test-editor.md#insert-a-delay-before-a-ui-action)
