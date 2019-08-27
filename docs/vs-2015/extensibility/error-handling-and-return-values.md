---
title: 错误处理和返回值 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- errors [Visual Studio SDK], handling
- error handling
- return values
ms.assetid: b2d9079d-39a6-438a-8010-290056694b5c
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 74e61e60384b3e98bf26eb8208696ecb9223efa3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696336"
---
# <a name="error-handling-and-return-values"></a>错误处理和返回值
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Vspackage 和 COM 使用相同的体系结构的错误。 `SetErrorInfo`和`GetErrorInfo`函数是 Win32 应用程序编程接口 (API) 的一部分。 在集成的开发环境 (IDE) 中的任何 VSPackage 可以调用这些全局 Win32 Api，用于记录丰富的错误消息时接收错误通知。 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]提供互操作程序集来管理错误的信息。  
  
## <a name="interop-methods"></a>互操作方法  
 为方便起见，IDE 提供了一种方法， <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>，若要使用而不是调用 Win32 Api。 在托管的代码使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>。 时出错`HRESULT`到达应在其中显示错误消息的级别 (这通常是该对象实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>命令处理程序)，IDE 使用另一种方法， <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>，以便显示相应的消息框。 在托管的代码使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>方法。  
  
 为 VSPackage 实施者，您的 COM 对象通常实现`ISupportErrorInfo`。 `ISupportErrorInfo`接口可确保丰富的错误信息可以调用链向上垂直移动。 跨进程或跨线程可能使用的对象必须支持`ISupportErrorInfo`以确保丰富的错误消息返回给调用方正确封送。  
  
 Vspackage 与相关的和，是参与扩展 IDE，包括编辑器工厂、 编辑器、 层次结构，并提供服务的所有对象都应都支持丰富的错误信息。 虽然 IDE 不需要这些 VSPackage 对象来实现`ISupportErrorInfo`，始终建议。  
  
 IDE 负责报告错误的信息和显示的用户[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]每当`HRESULT`传播到 IDE。 IDE 也是用于创建机制，`ErrorInfo`对象。  
  
## <a name="general-guidelines"></a>通用准则  
 可以使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>方法以设置和报告您的 VSPackage 实现的内部错误。 但是，作为一般规则，请遵循以下准则来处理你的 VSPackage 中的错误消息：  
  
- 实现`ISupportErrorInfo`VSPackage COM 对象中。  
  
- 创建错误报告调用的机制<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>中实现的对象的方法<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>。  
  
- 允许通过向用户显示错误 IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>方法。  
  
## <a name="error-information-in-the-ide"></a>在 IDE 中的错误信息  
 以下规则指示如何处理中的错误信息[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]IDE:  
  
- 如防御策略，以保证过时错误信息不会报告给用户，函数调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>方法首先应调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>方法。 传入`null`清除缓存的错误消息，然后调用的任何内容，可能会设置新的错误信息。  
  
- 仅允许使用不直接报告错误消息的函数调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>方法，如果它们返回错误`HRESULT`。 允许清除`ErrorInfo`条目的函数或返回<xref:Microsoft.VisualStudio.VSConstants.S_OK>。 此规则的唯一例外是当调用将返回错误`HRESULT`从其接收方可以显式恢复或放心地忽略。  
  
- 显式将忽略错误任何参与方`HRESULT`必须调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>方法替换<xref:Microsoft.VisualStudio.VSConstants.S_OK>。 否则为`ErrorInfo`另一方生成一个错误，而无需提供其自己时，对象可能会意外地使用`ErrorInfo`。  
  
- 发出错误的所有方法`HRESULT`建议调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>方法以提供丰富的错误信息。 如果返回`HRESULT`是一个特殊`FACILITY_ITF`错误，则该方法需要提供适当`ErrorInfo`对象。 如果返回的错误是标准的系统错误 (例如， <xref:Microsoft.VisualStudio.VSConstants.E_OUTOFMEMORY>， <xref:Microsoft.VisualStudio.VSConstants.E_ABORT>， <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG>， <xref:Microsoft.VisualStudio.VSConstants.E_UNEXPECTED>，等等。) 是可接受无需显式调用返回的错误代码的<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>方法。 作为一防御性编码策略，当发出错误`HRESULT`（包括系统错误），均应调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>方法，使用`ErrorInfo`描述更详细地故障或`null`。  
  
- 返回由另一次调用产生错误必须通过从发生故障的接收到的信息的所有函数中都调用`HRESULT`而无需修改`ErrorInfo`对象。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 [SetErrorInfo （组件自动化）](https://msdn.microsoft.com/8eaacfac-fc37-4eaa-870b-10b99d598d66)   
 [GetErrorInfo](https://msdn.microsoft.com/03317526-8c4f-4173-bc10-110c8112676a)   
 [ISupportErrorInfo 接口](https://msdn.microsoft.com/42d33066-36b4-4a5b-aa5d-46682e560f32)
