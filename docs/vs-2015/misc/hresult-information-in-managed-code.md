---
title: 托管代码中的 HRESULT 信息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, HRESULT information
- HRESULT, managed VSPackages
ms.assetid: 0795ee94-17a8-4327-bf57-27cd5e312a4c
caps.latest.revision: 29
manager: jillfra
ms.openlocfilehash: 4f80b575656c2d8b1740f217f2e144f89f254078
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65681636"
---
# <a name="hresult-information-in-managed-code"></a>托管代码中的 HRESULT 信息
当遇到 HRESULT 返回值时，托管代码和 COM 之间的交互可能会导致一些问题。  
  
 在 COM 接口中，HRESULT 返回值可以发挥以下作用：  
  
- 提供错误信息（例如 <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG>）。  
  
- 提供有关正常程序行为的状态信息。  
  
  当 COM 调入托管代码时，HRESULT 可能会导致以下问题：  
  
- 返回小于零的 HRESULT 值（故障代码）的 COM 函数会生成异常。  
  
- 无法辨别定期返回两个或更多个不同成功代码（例如，<xref:Microsoft.VisualStudio.VSConstants.S_OK> 或 <xref:Microsoft.VisualStudio.VSConstants.S_FALSE>）的 COM 方法。  
  
  由于许多 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] COM 函数返回小于零的 HRESULT 值或返回不同的成功代码，因此，编写了 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] 互操作程序集以便保留方法签名。 所有 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] 互操作方法均为 `int` 类型。 HRESULT 值通过互操作层传递，无需更改且不会生成异常。  
  
  由于 COM 函数向调用它的托管方法返回 HRESULT，因此，进行调用的方法必须检查 HRESULT，并根据需要引发异常。  
  
## <a name="handling-hresults-returned-to-managed-code-from-com"></a>处理从 COM 返回到托管代码的 HRESULT  
 当从托管代码调用 COM 接口时，请检查 HRESULT 值并根据需要引发异常。 <xref:Microsoft.VisualStudio.ErrorHandler> 类包含 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 方法，该方法根据传递给它的 HRESULT 值引发 COM 异常。  
  
 默认情况下，每次向 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 传递值小于零的 HRESULT 时，它都会引发异常。 如果此类 HRESULT 是可接受的值，不应引发异常，那么，应在测试完其他 HRESULT 的值后，将这些值传递给 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A>。 如果所测试的 HRESULT 与显式传递到 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 的任何 HRESULT 值匹配，则不会引发异常。  
  
> [!NOTE]
> <xref:Microsoft.VisualStudio.VSConstants>类包含常见 hresult （例如， <xref:Microsoft.VisualStudio.VSConstants.S_OK> 和 <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> ）和 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] hresult （例如 <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA> 和）的常量 <xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT> 。 <xref:Microsoft.VisualStudio.VSConstants> 还提供 <xref:Microsoft.VisualStudio.ErrorHandler.Succeeded%2A> 和 <xref:Microsoft.VisualStudio.ErrorHandler.Failed%2A> 方法，分别对应于 COM 中的 SUCCEEDED 宏和 FAILED 宏。  
  
 例如，在以下函数调用中，<xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> 是可接受的返回值，而其他所有小于零的 HRESULT 均表示错误。  
  
 [!code-csharp[VSSDKHRESULTInformation#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs#1)]
 [!code-vb[VSSDKHRESULTInformation#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb#1)]  
  
 如果有多个可接受的返回值，只需在调用 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 时将其他 HRESULT 值追加到列表中。  
  
 [!code-csharp[VSSDKHRESULTInformation#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs#2)]
 [!code-vb[VSSDKHRESULTInformation#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb#2)]  
  
## <a name="returning-hresults-to-com-from-managed-code"></a>从托管代码将 HRESULT 返回到 COM  
 如果没有发生异常，托管代码会向调用它的 COM 函数返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK>。 COM 互操作支持托管代码中强类型化的常见异常。 例如，收到不可接受的 `null` 参数的方法会引发 <xref:System.ArgumentNullException>。  
  
 如果不确定要引发哪个异常，但知道要返回到 COM 的 HRESULT，则可以使用 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 方法引发相应的异常。 即使是非标准错误（例如 <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>），也同样可行。 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 会尝试将传递给它的 HRESULT 映射到强类型化的异常。 如果无法映射，它会改为引发一般的 COM 异常。 最终结果是，从托管代码传递到 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 的 HRESULT 返回到调用它的 COM 函数中。  
  
> [!NOTE]
> 异常会降低性能，它用于指示程序的异常状况。 对于所发生的状况，通常应以内联方式处理，而不是引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [托管 Vspackage](../misc/managed-vspackages.md)   
 [与非托管代码互操作](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)   
 [如何：映射 Hresult 和异常](https://msdn.microsoft.com/library/610b364b-2761-429d-9c4a-afbc3e66f1b9)   
 [为互操作生成 COM 组件](https://msdn.microsoft.com/7a2c657a-cfef-40f0-bed3-7c2c0ac4abdf)   
 [托管的 VSPackage](../misc/managed-vspackages.md)