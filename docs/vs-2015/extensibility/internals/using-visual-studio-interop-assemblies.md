---
title: 使用互操作程序集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, interop assemblies
- interop assemblies, Visual Studio
- managed VSPackages, interop assemblies
ms.assetid: 1043eb95-4f0d-4861-be21-2a25395b3b3c
caps.latest.revision: 34
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7df241773d06574f8d070285c2b45b662ccd6403
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65675202"
---
# <a name="using-visual-studio-interop-assemblies"></a>使用 Visual Studio 互操作程序集
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio 互操作程序集允许访问提供 Visual Studio 可扩展性的 COM 接口的托管应用程序。 没有直接的 COM 接口和其互操作的版本之间的一些差异。 例如，Hresult 通常表示为一个整数值和需要为异常，相同的方式进行处理和参数 (尤其是 out 参数） 的处理方式不同。

## <a name="handling-hresults-returned-to-managed-code-from-com"></a>处理从 COM 返回到托管代码的 HRESULT
 当从托管代码调用 COM 接口时，请检查 HRESULT 值并根据需要引发异常。 <xref:Microsoft.VisualStudio.ErrorHandler> 类包含 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 方法，该方法根据传递给它的 HRESULT 值引发 COM 异常。

 默认情况下，每次向 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 传递值小于零的 HRESULT 时，它都会引发异常。 如果此类 HRESULT 是可接受的值，不应引发异常，那么，应在测试完其他 HRESULT 的值后，将这些值传递给 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A>。 如果所测试的 HRESULT 与显式传递到 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 的任何 HRESULT 值匹配，则不会引发异常。

> [!NOTE]
> <xref:Microsoft.VisualStudio.VSConstants>类通用 hresult 包含常量等<xref:Microsoft.VisualStudio.VSConstants.S_OK>并<xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL>，和[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]HRESULT，例如，<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>和<xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>。 <xref:Microsoft.VisualStudio.VSConstants> 还提供 <xref:Microsoft.VisualStudio.ErrorHandler.Succeeded%2A> 和 <xref:Microsoft.VisualStudio.ErrorHandler.Failed%2A> 方法，分别对应于 COM 中的 SUCCEEDED 宏和 FAILED 宏。

 例如，在以下函数调用中，<xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> 是可接受的返回值，而其他所有小于零的 HRESULT 均表示错误。

 [!code-csharp[VSSDKHRESULTInformation#1](../../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs#1)]
 [!code-vb[VSSDKHRESULTInformation#1](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb#1)]

 如果有多个可接受的返回值，只需在调用 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 时将其他 HRESULT 值追加到列表中。

 [!code-csharp[VSSDKHRESULTInformation#2](../../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs#2)]
 [!code-vb[VSSDKHRESULTInformation#2](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb#2)]

## <a name="returning-hresults-to-com-from-managed-code"></a>从托管代码将 HRESULT 返回到 COM
 如果没有发生异常，托管代码会向调用它的 COM 函数返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK>。 COM 互操作支持托管代码中强类型化的常见异常。 例如，收到不可接受的 `null` 参数的方法会引发 <xref:System.ArgumentNullException>。

 如果不确定要引发哪个异常，但知道要返回到 COM 的 HRESULT，则可以使用 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 方法引发相应的异常。 即使是非标准错误（例如 <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>），也同样可行。 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 会尝试将传递给它的 HRESULT 映射到强类型化的异常。 如果无法映射，它会改为引发一般的 COM 异常。 最终结果是，从托管代码传递到 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 的 HRESULT 返回到调用它的 COM 函数中。

> [!NOTE]
> 异常会降低性能，它用于指示程序的异常状况。 对于所发生的状况，通常应以内联方式处理，而不是引发异常。

## <a name="iunknown-parameters-passed-as-type-void"></a>IUnknown 参数作为类型 void * * 传递
 [Out] 参数被定义为类型寻找`void **`com 接口，但这指`[``iid_is``]`中[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]互操作程序集方法原型。

 有时，COM 接口生成`IUnknown`对象和 COM 接口然后将其作为传递类型`void **`。 这些接口是特别重要因为如果变量定义为 [out] 在 IDL，则`IUnknown`对象是使用引用计数`AddRef`方法。 如果无法正确处理该对象，则会发生内存泄漏。

> [!NOTE]
> `IUnknown`创建的 COM 接口和 [out] 变量中返回的对象会导致内存泄漏，如果未显式释放。

 处理此类对象的托管的方法应将<xref:System.IntPtr>指向的指针作为`IUnknown`对象，并调用<xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A>方法获取的对象。 调用方应然后返回值转换为任何类型是合适的。 当不再需要对象时，调用<xref:System.Runtime.InteropServices.Marshal.Release%2A>以将其释放。

 下面是调用示例<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>方法并处理`IUnknown`正确对象：

```
MyClass myclass;
Object object;
IntPtr pObj;
Guid iid = Typeof(MyClass).Guid;
int hr = windowFrame.QueryViewInterface(ref iid, out pObj);
if (NativeMethods.Succeeded(hr))
{
    try
    {
        object = Marshal.GetObjectForIUnknown(pObj);
        myclass = object;
    }
    finally
    {
        Marshal.Release(pObj);
    }
}
else
{
    // error calling QueryViewInterface
}
```

> [!NOTE]
> 已知以下方法传递`IUnknown`作为类型对象的指针<xref:System.IntPtr>。 在本部分中所述处理它们。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.CreateProject%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>

## <a name="optional-out-parameters"></a>[Out] 参数可选
 查找定义作为 [out] 参数的数据类型 (`int`， `object`，依次类推) 在 COM 接口，但被定义为数组中的相同数据类型[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]互操作程序集方法原型。

 一些 COM 接口，如<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>，将 [out] 参数为可选。 如果对象不是必需的这些 COM 接口返回`null`作为该参数而不是创建的 [out] 对象的值的指针。 这是设计使然。 对于这些接口，`null`指针被假定为 VSPackage 的正确行为的一部分且不会返回错误。

 CLR 不允许为一个 [out] 参数的值，所以`null`，这些接口的设计行为的一部分不是托管代码中直接可用。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]受影响的接口的互操作程序集方法解决此问题通过定义为数组的相关参数，因为 CLR 允许将传递`null`数组。

 这些方法的托管的实现应放置`null`到参数时没有任何要返回的数组。 否则为创建正确类型的一个元素数组并将返回值放在数组中。

 管理从接口使用可选的 [out] 接收信息的方法参数接收参数作为数组。 只需查看该数组的第一个元素的值。 如果不是`null`，就像原始参数将第一个元素。

## <a name="passing-constants-in-pointer-parameters"></a>指针参数中传递常量
 查找的参数定义为 [in] 指针中的 COM 接口，但定义为<xref:System.IntPtr>中键入[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]互操作程序集方法原型。

 COM 接口传递的特殊值，例如 0、-1 或 – 2，而不是一个对象指针时，会出现类似问题。 与不同[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]，CLR 不允许常量可强制转换为对象。 相反，[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]互操作程序集定义作为参数<xref:System.IntPtr>类型。

 这些方法的托管的实现应充分利用这一事实，<xref:System.IntPtr>类具有两`int`和`void *`构造函数可创建<xref:System.IntPtr>从一个对象或整数常量，根据需要。

 托管方法接收<xref:System.IntPtr>此类型的参数应使用<xref:System.IntPtr>类型转换运算符来处理结果。 首先将转换<xref:System.IntPtr>到`int`和测试针对相关的整数常量。 如果没有值匹配，将其转换为所需的类型的对象，然后继续。

 此示例，请参阅<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A>。

## <a name="ole-return-values-passed-as-out-parameters"></a>OLE 返回值传递作为 [out] 参数
 查找具有方法`retval`COM 接口，但在返回值具有`int`返回值和一个附加 [out] 中的数组参数[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]互操作程序集方法原型。 现在应该很清楚这些方法需要特殊处理，因为[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]互操作程序集方法原型有一个比 COM 接口方法的多个参数。

 许多 OLE 活动处理的 COM 接口将 OLE 状态信息发送回调用程序中存储`retval`返回值的接口。 而不是使用相对应的返回值[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]互操作程序集方法将信息发送回调用程序存储在 [out] 一个数组参数。

 这些方法的托管的实现应创建作为 [out] 参数的相同类型的单个元素数组，并将其放在参数中。 数组元素的值应为与相应 COM 相同`retval`。

 调用此类型的接口的托管的方法应请求从 [out] 数组的第一个元素。 可以将此元素处理，就好像`retval`从相应的 COM 接口返回值。

## <a name="see-also"></a>请参阅
 [与非托管代码交互操作](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
