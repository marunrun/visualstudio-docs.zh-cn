---
title: Office 中的线程支持
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- multiple threads [Office development in Visual Studio]
- threading [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], threading support
- object models [Office development in Visual Studio], threading support
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3218a12add86739c76cd50f82fdda5d845e2b069
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978762"
---
# <a name="threading-support-in-office"></a>Office 中的线程支持
  本文提供了有关如何线程处理在 Microsoft Office 对象模型中支持的信息。 Office 对象模型不是线程安全的但可以使用的 Office 解决方案中的多个线程。 Office 应用程序是组件对象模型 (COM) 服务器。 COM 允许客户端在任意线程上调用 COM 服务器。 对于不是线程安全的 COM 服务器，COM 提供了一种机制来序列化并发调用，以便在服务器上执行任何时候只有一个逻辑线程。 此机制称为单线程单元 (STA) 模型。 调用进行序列化，因为调用方可能阻止一段时间中，而服务器太忙或处理在后台线程上的其他调用。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="knowledge-required-when-using-multiple-threads"></a>使用多个线程时所需的知识
 若要使用的多个线程，必须具有至少基本了解以下方面的多线程处理：

- Windows Api

- COM 多线程的概念

- 并发

- 同步

- 封送处理

  有关常规信息有关的多线程处理，请参阅[托管线程处理](/dotnet/standard/threading/)。

  在主 STA 中运行 office 了解其含义，使可能了解如何通过 Office 使用多个线程。

## <a name="basic-multithreading-scenario"></a>多线程处理的基本方案
 在 Office 解决方案中的代码始终在主 UI 线程上运行。 你可能想要通过在后台线程上运行单独的任务来消除应用程序的性能。 目标是两项任务看似同时完成而不是跟另一个，这应该产生更流畅的执行 （的主要原因要使用多个线程） 中的一个任务。 例如，事件代码可能对主 Excel UI 线程，并可能会在后台线程上运行的任务从服务器收集数据，并使用来自服务器的数据更新 Excel UI 中的单元格。

## <a name="background-threads-that-call-into-the-office-object-model"></a>调入 Office 对象模型的后台线程
 当后台线程到 Office 应用程序的调用时，调用进行自动封送跨 STA 边界。 但是，则 Office 应用程序可以处理后台线程进行的调用时无法保证。 有几种可能性：

1. Office 应用程序必须发送调用能够在没有输入的信息。 如果它在执行大量处理，但不产生结果，则可能需要时间。

2. 如果另一个逻辑线程单元中已存在，不能输入新线程。 这通常发生在逻辑线程进入 Office 应用程序，并将返回到调用方的单元的可重入调用。 应用程序被阻止等待该调用返回。

3. Excel 可能处于的状态，以便它不能立即处理的传入呼叫。 例如，Office 应用程序可能会显示一个模式对话框。

   对于 2 和 3 的可能性，COM 提供了[IMessageFilter](/windows/desktop/api/objidl/nn-objidl-imessagefilter)接口。 通过服务器实现它，如果输入的所有调用[HandleIncomingCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-handleincomingcall)方法。 有关第 2 种可能性，调用将自动被拒绝。 对于第 3 种可能性，服务器可以拒绝的调用中，视情况而定。 如果调用被拒绝，调用方必须决定要执行的操作。 通常情况下，调用方实现[IMessageFilter](/windows/desktop/api/objidl/nn-objidl-imessagefilter)，在这种情况下它将通过拒绝的通知[RetryRejectedCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-retryrejectedcall)方法。

   但是，在 Visual Studio 中使用的 Office 开发工具创建的解决方案，对于 COM 互操作将转换到的所有被拒绝的调用<xref:System.Runtime.InteropServices.COMException>（"消息筛选器指示应用程序正忙"）。 每当进行调用的对象模型在后台线程，您必须准备好处理此异常。 通常，这涉及了一定时间重试，然后显示一个对话框。 但是，您还可以创建为 STA 的后台线程，然后注册该线程来处理这种情况的消息筛选器。

## <a name="start-the-thread-correctly"></a>正常启动线程
 在创建新的 STA 线程时，设置为 STA 的单元状态，启动线程之前。 下面的代码示例演示如何执行此操作。

 [!code-csharp[Trin_VstcoreCreatingExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/ThisWorkbook.cs#5)]
 [!code-vb[Trin_VstcoreCreatingExcel#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/ThisWorkbook.vb#5)]

 有关详细信息，请参阅[托管线程处理最佳做法](/dotnet/standard/threading/managed-threading-best-practices)。

## <a name="modeless-forms"></a>无模式窗体
 无模式窗体允许某种类型的与应用程序交互而显示窗体。 用户交互处理该窗体，并在窗体与无需关闭应用程序进行交互。 Office 对象模型支持托管的无模式窗体;但是，它们不应在后台线程上。

## <a name="see-also"></a>请参阅
- [线程处理 [C#]](/dotnet/csharp/programming-guide/concepts/threading/index)
- [线程 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/threading/index)
- [使用线程与线程处理](/dotnet/standard/threading/using-threads-and-threading)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
