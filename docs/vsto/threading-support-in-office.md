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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62978762"
---
# <a name="threading-support-in-office"></a>Office 中的线程支持
  本文提供了有关 Microsoft Office 对象模型中如何支持线程处理的信息。 Office 对象模型不是线程安全的，但可以在 Office 解决方案中使用多个线程。 Office 应用程序是组件对象模型 (COM) 服务器。 COM 允许客户端在任意线程上调用 COM 服务器。 对于非线程安全的 COM 服务器，COM 提供一种机制来序列化并发调用，以便在服务器上随时只执行一个逻辑线程。 此机制称为单线程单元 (STA) 模型。 由于调用是序列化的，因此在服务器繁忙或正在处理后台线程上的其他调用时，调用方可能会被阻止一段时间。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="knowledge-required-when-using-multiple-threads"></a>使用多个线程时所需的知识
 若要使用多个线程，你必须至少具有多线程处理的以下方面的基本知识：

- Windows Api

- COM 多线程概念

- 并发

- 同步

- 封送

  有关多线程处理的常规信息，请参阅 [托管线程处理](/dotnet/standard/threading/)。

  Office 在主 STA 中运行。 了解这种影响可以了解如何将多个线程与 Office 一起使用。

## <a name="basic-multithreading-scenario"></a>基本多线程方案
 Office 解决方案中的代码始终在主 UI 线程上运行。 你可能希望通过在后台线程上运行单独的任务来使应用程序性能变得平滑。 目标是一次完成两个任务，而不是一次完成另一个任务，这样做会导致更平稳的执行 (使用多个线程) 的主要原因。 例如，你可以在主 Excel UI 线程上使用事件代码，并且在后台线程上，你可以运行从服务器收集数据的任务，并使用服务器中的数据更新 Excel UI 中的单元格。

## <a name="background-threads-that-call-into-the-office-object-model"></a>调入 Office 对象模型的后台线程
 当后台线程调用 Office 应用程序时，该调用会自动跨 STA 边界进行封送处理。 但是，不能保证在后台线程发出调用时，Office 应用程序可以处理调用。 有几种可能性：

1. Office 应用程序必须抽取调用的消息才能进入。 如果它正在进行大量处理而不产生这种情况，则可能需要一些时间。

2. 如果单元中已存在另一个逻辑线程，则新线程将无法进入。 当逻辑线程进入 Office 应用程序，然后再对调用方的单元进行可重入回时，通常会发生这种情况。 应用程序被阻止，正在等待该调用返回。

3. Excel 可能处于某种状态，因此无法立即处理传入呼叫。 例如，Office 应用程序可能显示模式对话框。

   对于可能的2和3，COM 提供 [imessagefilter.prefiltermessage](/windows/desktop/api/objidl/nn-objidl-imessagefilter) 接口。 如果服务器实现，所有调用都通过 [HandleIncomingCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-handleincomingcall) 方法进入。 对于可能性2，将自动拒绝调用。 对于可能的3，服务器可能会拒绝调用，具体取决于环境。 如果调用被拒绝，则调用方必须确定要执行的操作。 通常情况下，调用方实现 [imessagefilter.prefiltermessage](/windows/desktop/api/objidl/nn-objidl-imessagefilter)，在这种情况下， [RetryRejectedCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-retryrejectedcall) 方法会通知其拒绝。

   但是，对于使用 Visual Studio 中的 Office 开发工具创建的解决方案，COM 互操作将所有拒绝的调用转换为 <xref:System.Runtime.InteropServices.COMException> ( "消息筛选器指示该应用程序忙" ) 。 无论何时在后台线程上调用对象模型，都必须准备好处理此异常。 通常，这涉及重试一定的时间，然后显示一个对话框。 不过，您也可以将后台线程创建为 STA，然后为该线程注册消息筛选器来处理这种情况。

## <a name="start-the-thread-correctly"></a>正确启动线程
 创建新的 STA 线程时，请在启动线程之前将单元状态设置为 STA。 下面的代码示例演示如何执行此操作。

 [!code-csharp[Trin_VstcoreCreatingExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/ThisWorkbook.cs#5)]
 [!code-vb[Trin_VstcoreCreatingExcel#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/ThisWorkbook.vb#5)]

 有关详细信息，请参阅 [托管线程处理最佳做法](/dotnet/standard/threading/managed-threading-best-practices)。

## <a name="modeless-forms"></a>无模式窗体
 在显示窗体时，无模式窗体允许与应用程序进行某种类型的交互。 用户与窗体进行交互，窗体与应用程序交互，而不关闭。 Office 对象模型支持托管无模式窗体;但是，它们不应在后台线程上使用。

## <a name="see-also"></a>另请参阅
- [线程处理 (C#)](/dotnet/csharp/programming-guide/concepts/threading/index)
- [线程处理 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/threading/index)
- [使用线程和线程处理](/dotnet/standard/threading/using-threads-and-threading)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
