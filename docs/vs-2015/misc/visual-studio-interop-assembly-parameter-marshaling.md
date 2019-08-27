---
title: Visual Studio 互操作程序集参数封送处理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting Visual Studio SDK interop assemblies
- interop assemblies, parameter marshaling
- interop assemblies, troubleshooting
ms.assetid: 89123eae-0fef-46d5-bd36-3d2a166b14e3
caps.latest.revision: 24
manager: jillfra
ms.openlocfilehash: ac95c40b356c542da323a3ea3744827087f2d840
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686927"
---
# <a name="visual-studio-interop-assembly-parameter-marshaling"></a>Visual Studio 互操作程序集参数封送处理
在托管代码中编写 Vspackage 可能需要调用或是由非托管 COM 代码进行调用。 通常情况下，转换，或自动封送，互操作封送处理程序方法自变量。 但是，有时参数无法转换直接的方式。 在这些情况下，互操作程序集方法原型参数用于尽可能接近地匹配 COM 函数参数。 有关详细信息，请参阅[互操作封送处理](https://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)。  
  
## <a name="general-suggestions"></a>常规建议  
  
##### <a name="read-the-reference-documentation"></a>阅读参考文档  
 若要检测的互操作性问题的有效方法是读取每个方法的参考文档。  
  
 每个方法的参考文档包含三个相关部分：  
  
- [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] COM 函数原型。  
  
- 互操作程序集方法原型。  
  
- COM 参数和每个的简短说明的列表。  
  
##### <a name="look-for-differences-between-the-two-prototypes"></a>查找两个原型之间的差异  
 大多数互操作性问题派生的 COM 接口中的特定类型的定义中的相同类型的定义之间的不匹配[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]互操作程序集。 例如，请考虑将传递的功能中的不同`null`[out] 参数中的值。 必须查找两个原型之间的差异，并考虑其后果所传递的数据。  
  
##### <a name="read-the-parameter-definitions"></a>读取的参数定义  
 读取的参数定义。 COM 是比公共语言运行时 (CLR) 有关混合不同类型的单个参数中的数据不太严格。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] COM 接口充分利用这种灵活性。 任何参数都可以传递或需要非标准值或类型的数据，如指针参数中的常量值应这种情况下所述文档中。  
  
### <a name="iunknown-objects-passed-as-type-void"></a>IUnknown 对象传递为类型 void * *  
 [Out] 参数被定义为类型寻找`void **`com 接口，但这指`[``iid_is``]`中[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]互操作程序集方法原型。  
  
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
  
### <a name="optional-out-parameters"></a>[Out] 参数可选  
 查找定义作为 [out] 参数的数据类型 (`int`， `object`，依次类推) 在 COM 接口，但被定义为数组中的相同数据类型[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]互操作程序集方法原型。  
  
 一些 COM 接口，如<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>，将 [out] 参数为可选。 如果对象不是必需的这些 COM 接口返回`null`作为该参数而不是创建的 [out] 对象的值的指针。 这是设计使然。 对于这些接口，`null`指针被假定为 VSPackage 的正确行为的一部分且不会返回错误。  
  
 CLR 不允许为一个 [out] 参数的值，所以`null`，这些接口的设计行为的一部分不是托管代码中直接可用。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]受影响的接口的互操作程序集方法解决此问题通过定义为数组的相关参数，因为 CLR 允许将传递`null`数组。  
  
 这些方法的托管的实现应放置`null`到参数时没有任何要返回的数组。 否则为创建正确类型的一个元素数组并将返回值放在数组中。  
  
 管理从接口使用可选的 [out] 接收信息的方法参数接收参数作为数组。 只需查看该数组的第一个元素的值。 如果不是`null`，就像原始参数将第一个元素。  
  
### <a name="passing-constants-in-pointer-parameters"></a>指针参数中传递常量  
 查找的参数定义为 [in] 指针中的 COM 接口，但定义为<xref:System.IntPtr>中键入[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]互操作程序集方法原型。  
  
 COM 接口传递的特殊值，例如 0、-1 或 – 2，而不是一个对象指针时，会出现类似问题。 与不同[!INCLUDE[vcprvc](../includes/vcprvc-md.md)]，CLR 不允许常量可强制转换为对象。 相反，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]互操作程序集定义作为参数<xref:System.IntPtr>类型。  
  
 这些方法的托管的实现应充分利用这一事实，<xref:System.IntPtr>类具有两`int`和`void *`构造函数可创建<xref:System.IntPtr>从一个对象或整数常量，根据需要。  
  
 托管方法接收<xref:System.IntPtr>此类型的参数应使用<xref:System.IntPtr>类型转换运算符来处理结果。 首先将转换<xref:System.IntPtr>到`int`和测试针对相关的整数常量。 如果没有值匹配，将其转换为所需的类型的对象，然后继续。  
  
 此示例，请参阅<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A>。  
  
### <a name="ole-return-values-passed-as-out-parameters"></a>OLE 返回值传递作为 [out] 参数  
 查找具有方法`retval`COM 接口，但在返回值具有`int`返回值和一个附加 [out] 中的数组参数[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]互操作程序集方法原型。 现在应该很清楚这些方法需要特殊处理，因为[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]互操作程序集方法原型有一个比 COM 接口方法的多个参数。  
  
 许多 OLE 活动处理的 COM 接口将 OLE 状态信息发送回调用程序中存储`retval`返回值的接口。 而不是使用相对应的返回值[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]互操作程序集方法将信息发送回调用程序存储在 [out] 一个数组参数。  
  
 这些方法的托管的实现应创建作为 [out] 参数的相同类型的单个元素数组，并将其放在参数中。 数组元素的值应为与相应 COM 相同`retval`。  
  
 调用此类型的接口的托管的方法应请求从 [out] 数组的第一个元素。 可以将此元素处理，就好像`retval`从相应的 COM 接口返回值。  
  
## <a name="see-also"></a>请参阅  
 [互操作封送处理](https://msdn.microsoft.com/a95fdb76-7c0d-409e-a77e-0349b1ea1490)   
 [互操作封送处理](https://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)   
 [互操作性疑难解答](https://msdn.microsoft.com/library/b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37)   
 [托管的 VSPackage](../misc/managed-vspackages.md)