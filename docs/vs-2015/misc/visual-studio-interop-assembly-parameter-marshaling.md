---
title: Visual Studio 互操作程序集参数封送 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686927"
---
# <a name="visual-studio-interop-assembly-parameter-marshaling"></a>Visual Studio 互操作程序集参数封送处理
用托管代码编写的 Vspackage 可能必须调用或由非托管 COM 代码调用。 通常，互操作封送拆收器会自动对方法自变量进行转换或封送处理。 但是，有时参数无法直接转换。 在这些情况下，互操作程序集方法原型参数用于与 COM 函数参数尽可能匹配。 有关详细信息，请参阅 [互操作封送处理](https://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)。  
  
## <a name="general-suggestions"></a>一般建议  
  
##### <a name="read-the-reference-documentation"></a>阅读参考文档  
 检测互操作性问题的有效方法是阅读每个方法的参考文档。  
  
 每个方法的参考文档包含三个相关部分：  
  
- [!INCLUDE[vcprvc](../includes/vcprvc-md.md)]COM 函数原型。  
  
- 互操作程序集方法原型。  
  
- COM 参数的列表和每个参数的简短说明。  
  
##### <a name="look-for-differences-between-the-two-prototypes"></a>查找两个原型之间的差异  
 大多数互操作性问题派生自 COM 接口中特定类型的定义与 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 互操作程序集中的相同类型的定义之间的不匹配。 例如，请考虑在 `null` [out] 参数中传递值的功能差异。 您必须查找这两个原型之间的差异，并考虑它们对要传递的数据的影响。  
  
##### <a name="read-the-parameter-definitions"></a>读取参数定义  
 读取参数定义。 与公共语言运行时相比，COM 不是公共语言运行时 (CLR) 在单个参数中混合不同类型的数据。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]COM 接口充分利用这种灵活性。 任何可传递或需要非标准值或数据类型的参数（例如，指针参数中的常量值）都应在文档中进行描述。  
  
### <a name="iunknown-objects-passed-as-type-void"></a>作为 void 类型传递的 IUnknown 对象 * *  
 查找在 `void **` COM 接口中定义为类型但 `[``iid_is``]` 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 互操作程序集方法原型中定义为的类型的 [out] 参数。  
  
 有时，COM 接口会生成一个 `IUnknown` 对象，然后 com 接口会将其作为类型传递 `void **` 。 这些接口尤其重要，因为如果在 IDL 中将变量定义为 [out]，则将 `IUnknown` 通过方法对对象进行引用计数 `AddRef` 。 如果未正确处理对象，则会发生内存泄漏。  
  
> [!NOTE]
> `IUnknown`由 COM 接口创建并在 [out] 变量中返回的对象会导致内存泄漏（如果未显式释放）。  
  
 处理此类对象的托管方法应视为 <xref:System.IntPtr> 指向对象的指针 `IUnknown` ，并调用 <xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> 方法以获取对象。 然后，调用方应将返回值强制转换为任何适当的类型。 当不再需要对象时，调用 <xref:System.Runtime.InteropServices.Marshal.Release%2A> 以释放它。  
  
 下面是调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A> 方法并正确处理对象的一个示例 `IUnknown` ：  
  
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
> 以下方法称为将 `IUnknown` 对象指针作为类型传递 <xref:System.IntPtr> 。 按照此部分中所述处理它们。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.CreateProject%2A>  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>  
  
### <a name="optional-out-parameters"></a>可选的 [out] 参数  
 在 COM 接口的) 中查找定义为 [out] 数据类型 (、等的参数 `int` `object` ，这些参数定义为 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 互操作程序集方法原型中相同数据类型的数组。  
  
 某些 COM 接口（如 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A> ）将 [out] 参数视为可选。 如果对象不是必需的，则这些 COM 接口会将 `null` 指针返回为该参数的值，而不是创建 [out] 对象。 这是设计的结果。 对于这些接口， `null` 将假定指针作为 VSPackage 的正确行为的一部分，并且不会返回错误。  
  
 由于 CLR 不允许使用 [out] 参数的值，因此在 `null` 托管代码中不能直接使用这些接口的设计行为的一部分。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]受影响接口的互操作程序集方法通过将相关参数定义为数组来解决该问题，因为 CLR 允许对 `null` 数组进行传递。  
  
 如果没有要返回的内容，则这些方法的托管实现应将一个 `null` 数组放入参数。 否则，创建一个正确类型的单元素数组，并将返回值放入数组中。  
  
 从具有可选的 [out] 参数的接口接收信息的托管方法接收参数作为数组。 只需检查数组中第一个元素的值。 如果不是，则将 `null` 第一个元素视为原始参数。  
  
### <a name="passing-constants-in-pointer-parameters"></a>在指针参数中传递常量  
 查找在 COM 接口中定义为 [in] 指针但在 <xref:System.IntPtr> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 互操作程序集方法原型中定义为类型的参数。  
  
 当 COM 接口传递特定值（如0、-1 或-2 而不是对象指针）时，会出现类似问题。 与不同 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] ，CLR 不允许将常量强制转换为对象。 相反， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 互操作程序集将参数定义为 <xref:System.IntPtr> 类型。  
  
 这些方法的托管实现应利用这一事实， <xref:System.IntPtr> 该类具有 `int` 和 `void *` 构造函数，可 <xref:System.IntPtr> 根据需要从对象或整数常量创建。  
  
 接收 <xref:System.IntPtr> 此类型的参数的托管方法应使用 <xref:System.IntPtr> 类型转换运算符来处理结果。 首先，将转换 <xref:System.IntPtr> 为 `int` ，并对相关的整数常量进行测试。 如果没有匹配的值，则将其转换为所需类型的对象，然后继续。  
  
 有关这种情况的示例，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A> 。  
  
### <a name="ole-return-values-passed-as-out-parameters"></a>作为 [out] 参数传递的 OLE 返回值  
 查找 `retval` 在 COM 接口中具有返回值的方法，但在 `int` [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 互操作程序集方法原型中具有返回值和附加的 [out] 数组参数。 请注意，这些方法需要特殊处理，因为 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 互操作程序集方法原型的参数比 COM 接口方法多一个。  
  
 许多处理 OLE 活动的 COM 接口会将有关 OLE 状态的信息发送回接口返回值中存储的调用程序 `retval` 。 相应的互操作程序集方法不使用返回值，而是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将信息发回存储在 [out] 数组参数中的调用程序。  
  
 这些方法的托管实现应创建与 [out] 参数类型相同的单元素数组，并将其放入参数中。 数组元素的值应与相应的 COM 相同 `retval` 。  
  
 调用此类型的接口的托管方法应从 [out] 数组中提取第一个元素。 此元素可以视为 `retval` 来自相应 COM 接口的返回值。  
  
## <a name="see-also"></a>另请参阅  
 [互操作封送](https://msdn.microsoft.com/a95fdb76-7c0d-409e-a77e-0349b1ea1490)   
 [互操作封送](https://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)   
 [互操作性疑难解答](https://msdn.microsoft.com/library/b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37)   
 [托管的 VSPackage](../misc/managed-vspackages.md)