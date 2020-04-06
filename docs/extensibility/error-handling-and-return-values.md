---
title: 错误处理和返回值 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- errors [Visual Studio SDK], handling
- error handling
- return values
ms.assetid: b2d9079d-39a6-438a-8010-290056694b5c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 30b6b9bff9056360f9ea840f47b1488f05bee872
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711932"
---
# <a name="error-handling-and-return-values"></a>错误处理和返回值
VS 包和 COM 使用相同的体系结构来处理错误。 和`SetErrorInfo``GetErrorInfo`函数是 Win32 应用程序编程接口 （API） 的一部分。 集成开发环境 （IDE） 中的任何 VSPackage 都可以调用这些全局 Win32 API，以在收到错误通知时记录丰富的错误信息。 提供[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]用于管理错误信息的互操作程序集。

## <a name="interop-methods"></a>互通方法
 为方便起见，IDE 提供了一种方法，<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>使用 而不是调用 Win32 API。 在托管代码使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>中。 当错误`HRESULT`到达应显示错误消息的级别（这通常是实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>命令处理程序的对象）时，IDE 使用另一种方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>，显示相应的消息框。 在托管代码中使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>方法。

 作为 VSPackage 实现者，COM 对象通常`ISupportErrorInfo`实现 。 该`ISupportErrorInfo`接口可确保丰富的错误信息可以垂直向上移动呼叫链。 跨进程或跨线程使用的对象必须支持`ISupportErrorInfo`，以确保将丰富的错误信息正确封送回调用方。

 与 VSPackages 相关且涉及扩展 IDE 的所有对象（包括编辑器工厂、编辑器、层次结构和提供的服务）都应支持丰富的错误信息。 虽然 IDE 不需要这些 VSPackage 对象来实现`ISupportErrorInfo`，但始终鼓励它。

 IDE 负责报告错误信息，并在将 错误信息传播到 IDE[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]时`HRESULT`将其显示给用户。 IDE 也是创建`ErrorInfo`对象的机制。

## <a name="general-guidelines"></a>一般性指导
 也可以使用 和<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>方法设置和报告 VSPackage 实现内部的错误。 但是，通常，请遵循以下准则来处理 VSPackage 中的错误消息：

- 在`ISupportErrorInfo`VSPackage COM 对象中实现。

- 创建错误报告机制，在实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A><xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>的对象中调用 方法。

- 让 IDE 通过 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>向用户显示错误。

## <a name="error-information-in-the-ide"></a>IDE 中的错误信息
 以下规则指示如何处理 IDE 中[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]的错误信息：

- 作为一种防御策略，以确保陈旧的错误信息不报告给用户，调用方法的<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>函数应首先调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>方法。 在调用`null`任何可能设置新错误信息的任何内容之前，先转接以清除缓存的错误消息。

- 不直接报告错误消息的函数只有在返回错误<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>`HRESULT`时才允许调用 方法。 允许清除函数的条目`ErrorInfo`上或返回<xref:Microsoft.VisualStudio.VSConstants.S_OK>时。 此规则的唯一例外是呼叫返回接收方可以显式恢复`HRESULT`或安全地忽略的错误。

- 显式忽略错误的`HRESULT`任何一方都必须使用 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>方法。 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 否则，当`ErrorInfo`另一方在未提供自己的`ErrorInfo`错误的情况下生成错误时，可能会意外使用该对象。

- 鼓励所有产生错误`HRESULT`的方法调用 该方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>以提供丰富的错误信息。 如果返回`HRESULT`的是特殊`FACILITY_ITF`错误，则需要该方法来提供正确的`ErrorInfo`对象。 如果返回的错误是标准系统错误（<xref:Microsoft.VisualStudio.VSConstants.E_OUTOFMEMORY>例如， <xref:Microsoft.VisualStudio.VSConstants.E_ABORT>、 <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG>、 <xref:Microsoft.VisualStudio.VSConstants.E_UNEXPECTED>、 、 等）， 则无需显式调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>方法即可返回错误代码。 作为防御性编码策略，当产生`HRESULT`错误（包括系统错误）时，始终调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>方法，以更详细地`ErrorInfo`描述故障，或`null`。

- 返回由另一个调用引起的错误的所有函数都必须传递从 中的失败调用接收的信息，`HRESULT``ErrorInfo`而无需修改对象。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [设置错误信息（组件自动化）](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-seterrorinfo)
- [GetErrorInfo](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-geterrorinfo)
- [ISupportErrorInfo 界面](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-isupporterrorinfo)
