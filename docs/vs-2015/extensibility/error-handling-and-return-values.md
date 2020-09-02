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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696336"
---
# <a name="error-handling-and-return-values"></a>错误处理和返回值
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Vspackage 和 COM 使用相同的体系结构来实现错误。 `SetErrorInfo`和 `GetErrorInfo` 函数是 (API) 的 Win32 应用程序编程接口的一部分。  (IDE) 集成开发环境中的任何 VSPackage 都可以调用这些全局 Win32 Api，以便在收到错误通知时记录丰富的错误信息。 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]提供互操作程序集来管理错误信息。  
  
## <a name="interop-methods"></a>互操作方法  
 为方便起见，IDE 提供了一个方法，用于 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 代替调用 Win32 api。 在托管代码中使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 。 如果错误 `HRESULT` 到达应显示错误消息的级别 (通常是实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 命令处理程序) 的对象，则 IDE 将使用另一种方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 来显示相应的消息框。 在托管代码中使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 方法。  
  
 作为 VSPackage 实施者，你的 COM 对象通常实现 `ISupportErrorInfo` 。 `ISupportErrorInfo`接口可确保丰富的错误信息可以在调用链中纵向向上移动。 可能跨进程或跨线程使用的对象必须支持 `ISupportErrorInfo` ，以确保将丰富的错误消息正确地封送回调用方。  
  
 与 Vspackage 相关的所有对象（包括编辑器工厂、编辑器、层次结构和提供的服务）都应支持丰富的错误信息。 尽管 IDE 不需要这些 VSPackage 对象来实现，但 `ISupportErrorInfo` 始终鼓励这样做。  
  
 IDE 负责报告错误信息，并在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 每次 `HRESULT` 将传播到 IDE 时向用户显示该信息。 IDE 也是用于创建对象的机制 `ErrorInfo` 。  
  
## <a name="general-guidelines"></a>通用准则  
 您可以使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 方法来设置和报告 VSPackage 实现的内部错误。 但是，作为一般规则，请遵循以下准则来处理 VSPackage 中的错误消息：  
  
- `ISupportErrorInfo`在 VSPACKAGE COM 对象中实现。  
  
- 创建一个错误报告机制，用于调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 实现的对象中的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 方法。  
  
- 让 IDE 通过方法向用户显示错误 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 。  
  
## <a name="error-information-in-the-ide"></a>IDE 中的错误信息  
 以下规则指示如何在 IDE 中处理错误信息 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ：  
  
- 作为一种防御策略来保证不向用户报告过时错误信息，调用方法的函数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 应该首先调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 方法。 传入 `null` 以清除缓存的错误消息，然后调用可能会设置新错误信息的任何内容。  
  
- 如果函数返回错误，则仅允许不直接报告错误消息的函数调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 方法 `HRESULT` 。 允许在 `ErrorInfo` 函数上或在返回时清除项上的 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 。 此规则的唯一例外是当调用返回一个错误， `HRESULT` 接收方可以从中显式恢复或安全地忽略该错误。  
  
- 显式忽略错误的任何参与方 `HRESULT` 都必须 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 使用调用方法 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 。 否则， `ErrorInfo` 当另一方生成错误，但未提供自己的时，可能会意外使用该对象 `ErrorInfo` 。  
  
- 鼓励产生错误的所有方法 `HRESULT` 都可以调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 方法来提供丰富的错误信息。 如果返回的 `HRESULT` 是一个特殊 `FACILITY_ITF` 错误，则需要使用方法来提供适当的 `ErrorInfo` 对象。 如果返回的错误为标准系统错误 (例如，、、、等 <xref:Microsoft.VisualStudio.VSConstants.E_OUTOFMEMORY> <xref:Microsoft.VisualStudio.VSConstants.E_ABORT> <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG> <xref:Microsoft.VisualStudio.VSConstants.E_UNEXPECTED> 。 ) 可接受返回错误代码，而无需显式调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 方法。 作为一种防御性编码策略，引发错误时 `HRESULT` (包括) 的系统错误，请始终调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 方法，方法是 `ErrorInfo` 更详细地描述失败，或调用方法 `null` 。  
  
- 返回由另一个调用产生的错误的所有函数都必须传递从中失败调用接收的信息， `HRESULT` 而无需修改 `ErrorInfo` 对象。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 [SetErrorInfo (组件自动化) ](https://msdn.microsoft.com/8eaacfac-fc37-4eaa-870b-10b99d598d66)   
 [GetErrorInfo](https://msdn.microsoft.com/03317526-8c4f-4173-bc10-110c8112676a)   
 [ISupportErrorInfo 接口](https://msdn.microsoft.com/42d33066-36b4-4a5b-aa5d-46682e560f32)
