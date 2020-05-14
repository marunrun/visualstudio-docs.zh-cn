---
title: 使用可视化工作室交互组件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, interop assemblies
- interop assemblies, Visual Studio
- managed VSPackages, interop assemblies
ms.assetid: 1043eb95-4f0d-4861-be21-2a25395b3b3c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5926b2cce217565c889c7ef2eeef877691101ed6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704135"
---
# <a name="using-visual-studio-interop-assemblies"></a>使用 Visual Studio 互操作程序集
可视化工作室互通程序集允许托管应用程序访问提供可视化工作室可扩展性的 COM 接口。 直 COM 接口与其互通版本之间存在一些差异。 例如，HRESULT 通常表示为 int 值，需要以与异常相同的方式处理，并且参数（尤其是出参数）的处理方式不同。

## <a name="handling-hresults-returned-to-managed-code-from-com"></a>处理从 COM 返回到托管代码的 HRESULT
 当从托管代码调用 COM 接口时，请检查 HRESULT 值并根据需要引发异常。 <xref:Microsoft.VisualStudio.ErrorHandler> 类包含 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 方法，该方法根据传递给它的 HRESULT 值引发 COM 异常。

 默认情况下，每次向 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 传递值小于零的 HRESULT 时，它都会引发异常。 如果此类 HRESULT 是可接受的值，不应引发异常，那么，应在测试完其他 HRESULT 的值后，将这些值传递给 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A>。 如果所测试的 HRESULT 与显式传递到 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 的任何 HRESULT 值匹配，则不会引发异常。

> [!NOTE]
> <xref:Microsoft.VisualStudio.VSConstants>类<xref:Microsoft.VisualStudio.VSConstants.S_OK>包含公共 H结果的常量，例如 ， 和<xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL>和[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]H结果， 和<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA> <xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>。 <xref:Microsoft.VisualStudio.VSConstants> 还提供 <xref:Microsoft.VisualStudio.ErrorHandler.Succeeded%2A> 和 <xref:Microsoft.VisualStudio.ErrorHandler.Failed%2A> 方法，分别对应于 COM 中的 SUCCEEDED 宏和 FAILED 宏。

 例如，在以下函数调用中，<xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> 是可接受的返回值，而其他所有小于零的 HRESULT 均表示错误。

 [!code-vb[VSSDKHRESULTInformation#1](../../extensibility/internals/codesnippet/VisualBasic/using-visual-studio-interop-assemblies_1.vb)]
 [!code-csharp[VSSDKHRESULTInformation#1](../../extensibility/internals/codesnippet/CSharp/using-visual-studio-interop-assemblies_1.cs)]

 如果有多个可接受的返回值，只需在调用 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 时将其他 HRESULT 值追加到列表中。

 [!code-vb[VSSDKHRESULTInformation#2](../../extensibility/internals/codesnippet/VisualBasic/using-visual-studio-interop-assemblies_2.vb)]
 [!code-csharp[VSSDKHRESULTInformation#2](../../extensibility/internals/codesnippet/CSharp/using-visual-studio-interop-assemblies_2.cs)]

## <a name="returning-hresults-to-com-from-managed-code"></a>从托管代码将 HRESULT 返回到 COM
 如果没有发生异常，托管代码会向调用它的 COM 函数返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK>。 COM 互操作支持托管代码中强类型化的常见异常。 例如，收到不可接受的 `null` 参数的方法会引发 <xref:System.ArgumentNullException>。

 如果不确定要引发哪个异常，但知道要返回到 COM 的 HRESULT，则可以使用 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 方法引发相应的异常。 即使是非标准错误（例如 <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>），也同样可行。 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 会尝试将传递给它的 HRESULT 映射到强类型化的异常。 如果无法映射，它会改为引发一般的 COM 异常。 最终结果是，从托管代码传递到 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 的 HRESULT 返回到调用它的 COM 函数中。

> [!NOTE]
> 异常会降低性能，它用于指示程序的异常状况。 对于所发生的状况，通常应以内联方式处理，而不是引发异常。

## <a name="iunknown-parameters-passed-as-type-void"></a>I 未知参数传递为类型无效*
 查找在 COM 接口中定义为类型的`void **`[out] 参数，但在`[``iid_is``]`[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]内部程序集方法原型中定义为类型。

 有时，COM 接口生成对象`IUnknown`，然后 COM 接口将其传递为类型`void **`。 这些接口尤其重要，因为如果变量在 IDL 中定义为 [out]，则`IUnknown`使用`AddRef`方法对对象进行引用计数。 如果对象处理不正确，则会发生内存泄漏。

> [!NOTE]
> 由`IUnknown`COM 接口创建并在 [out] 变量中返回的对象如果未显式释放，则会导致内存泄漏。

 处理此类对象的托管方法应视为<xref:System.IntPtr>指向`IUnknown`对象的指针，并调用<xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A>方法以获取该对象。 然后，调用方应将返回值转换为任何合适的类型。 当不再需要该对象时，调用<xref:System.Runtime.InteropServices.Marshal.Release%2A>以释放它。

 下面是调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>该方法并正确处理`IUnknown`对象的示例：

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
> 已知以下方法将对象指针传递`IUnknown`为类型<xref:System.IntPtr>。 如本节所述处理它们。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.CreateProject%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>

## <a name="optional-out-parameters"></a>可选 [出] 参数
 在 COM 接口中查找定义为 [out] 数据类型`int`（、`object`等） 的参数，但在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]内部程序集方法原型中定义为相同数据类型的数组。

 某些 COM 接口（<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>如 ）将 [out] 参数视为可选参数。 如果不需要对象，这些 COM 接口将`null`指针作为该参数的值返回，而不是创建 [out] 对象。 这是设计的结果。 对于这些接口，`null`指针被假定为 VSPackage 正确行为的一部分，并且不会返回任何错误。

 由于 CLR 不允许 [out] 参数的值是`null`，这些接口的设计行为的一部分不能直接在托管代码中可用。 受影响[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]接口的互操作程序集方法通过将相关参数定义为数组来解决此问题，因为 CLR 允许传递`null`数组。

 当没有返回时，这些方法的托管实现`null`应将数组放入参数中。 否则，创建正确类型的单元素数组，并将返回值放在数组中。

 从具有可选 [out] 参数的接口接收信息的托管方法将参数作为数组接收。 只需检查数组的第一个元素的值。 如果不是`null`，则将第一个元素视为原始参数。

## <a name="passing-constants-in-pointer-parameters"></a>在指针参数中传递常量
 在 COM 接口中查找定义为 [in] 指针，但在内部操作程序集方法原型中定义为<xref:System.IntPtr>类型的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]参数。

 当 COM 接口传递特殊值（如 0、-1 或 -2）而不是对象指针时，也会出现类似的问题。 与[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]不同，CLR 不允许将常量转换为对象。 相反，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]互操作程序集将参数定义为类型<xref:System.IntPtr>。

 这些方法的托管<xref:System.IntPtr>实现应利用类具有和`int``void *`构造函数这一事实，以便根据需要从对象或整数常量<xref:System.IntPtr>创建 。

 接收<xref:System.IntPtr>此类型参数的托管方法应使用<xref:System.IntPtr>类型转换运算符来处理结果。 首先将<xref:System.IntPtr>转换为`int`，并针对相关的整数常量进行测试。 如果没有值匹配，请将其转换为所需类型的对象并继续。

 有关此示例，请参阅<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A>。

## <a name="ole-return-values-passed-as-out-parameters"></a>作为 [out] 参数传递的 OLE 返回值
 查找在 COM 接口`retval`中具有返回值但`int`[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]具有返回值并在内部分声程序集方法原型中具有附加 [out] 数组参数的方法。 应该清楚的是，这些方法需要特殊处理，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]因为内部程序集方法原型比 COM 接口方法多一个参数。

 处理 OLE 活动的许多 COM 接口将有关 OLE 状态的信息发送回存储在接口`retval`返回值中的调用程序。 相应的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]内部程序集方法不使用返回值，而是将信息发送回存储在 [out] 数组参数中的调用程序。

 这些方法的托管实现应创建与 [out] 参数类型相同的单元素数组，并将其放入参数中。 数组元素的值应与相应的 COM`retval`相同。

 调用此类型接口的托管方法应从 [out] 数组中提取第一个元素。 可以将此元素视为来自相应 COM 接口`retval`的返回值。

## <a name="see-also"></a>请参阅
- [与非托管代码交互操作](/dotnet/framework/interop/index)
