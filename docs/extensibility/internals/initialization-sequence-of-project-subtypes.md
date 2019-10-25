---
title: 项目子类型的初始化序列 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 678f704c73a39cdf2130d36fcfb1a74925dd89d1
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72726879"
---
# <a name="initialization-sequence-of-project-subtypes"></a>项目子类型的初始化序列
环境通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> 的基本项目工厂实现来构造项目。 当环境确定项目文件扩展名的项目类型 GUID 列表不为空时，将开始构造项目子类型。 项目文件扩展名和项目 GUID 指定项目是否是 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 或 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目类型。 例如，.vbproj extension 和 {F184B08F-C81C-45F6-A57F-5ABD9991F28F} 标识 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目。

## <a name="environments-initialization-of-project-subtypes"></a>环境初始化项目子类型
 下面的过程详细说明了由多个项目子类型聚合的项目系统的初始化顺序。

1. 环境调用基本项目的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>，而项目分析它的项目文件时，它发现不 `null` 聚合项目类型 Guid 列表。 项目将直接停止创建其项目。

2. 项目调用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> 服务 `QueryService`，以使用环境的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> 方法实现创建项目子类型。 在此方法中，环境在遍历项目类型 Guid （从最外面的项目子类型开始）的列表时对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>、<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> 方法的实现执行递归函数调用。

     下面详细介绍了初始化步骤。

    1. 环境的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> 方法的实现将调用具有以下函数声明的 `HrCreateInnerProj` 方法：

         \<CodeContentPlaceHolder > 0 </CodeContentPlaceHolder>

         当第一次调用此函数时（即，对于最外面的项目子类型），`pOuter` 和 `pOwner` 的参数将作为 `null` 传入，并且函数会将最外面的项目子类型 `IUnknown` 设置为 `pOuter`。

    2. 接下来，环境调用 `HrCreateInnerProj` 函数，该函数具有列表中的第二个项目类型 GUID。 此 GUID 对应于第二个内部项目子类型单步执行到聚合序列中的基础项目。

    3. @No__t_0 现在指向最外面的项目子类型的 `IUnknown`，`HrCreateInnerProj` 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> 的实现，然后调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> 的实现。 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> 方法中，你在 `IUnknown` 最外面的项目子类型的控制中，`pOuter`。 所拥有的项目（内部项目子类型）需要在此处创建其聚合项目对象。 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> 方法实现中，传递指向正在聚合的内部项目的 `IUnknown` 的指针。 这两种方法创建聚合对象，而您的实现需要遵循 COM 聚合规则，以确保项目子类型不会在其自身上保持引用计数。

    4. `HrCreateInnerProj` 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> 的实现。 在此方法中，项目子类型执行其初始化工作。 例如，可以在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> 中注册解决方案事件。

    5. `HrCreateInnerProj` 将以递归方式调用，直到达到列表中的最后一个 GUID （基本项目）。 对于每个调用，将重复步骤 c 到 d。 `pOuter` 指向每个聚合级别 `IUnknown` 的最外面的项目子类型。

## <a name="example"></a>示例

下面的示例详细说明了在环境实现时，<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> 方法的近似表示形式中的编程进程。 此代码只是一个示例;它不会进行编译，并且为了清楚起见，删除了所有错误检查。

```cpp
HRESULT CreateAggregateProject
(
    LPCOLESTR lpstrGuids,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    REFIID iidProject,
    void **ppvProject)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpunkProj;
    CComPtr<IVsAggregatableProject> srpAggProject;
    CComBSTR bstrGuids = lpstrGuids;
    BOOL fCanceled = FALSE;
    *ppvProject = NULL;

    HrCreateInnerProj(
         bstrGuids, NULL, NULL, pszFilename, pszLocation,
         pszName, grfCreateFlags, &srpunkProj, &fCanceled);
    srpunkProj->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggProject));
    srpAggProject->OnAggregationComplete();
    srpunkProj->QueryInterface(iidProject, ppvProject);
}

HRESULT HrCreateInnerProj
(
    WCHAR *pwszGuids,
    IUnknown *pOuter,
    IVsAggregatableProject *pOwner,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    IUnknown **ppInner,
    BOOL *pfCanceled
)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpInner;
    CComPtr<IVsAggregatableProject> srpAggInner;
    CComPtr<IVsProjectFactory> srpProjectFactory;
    CComPtr<IVsAggregatableProjectFactory> srpAggPF;
    GUID guid = GUID_NULL;
    WCHAR *pwszNextGuids = wcschr(pwszGuids, L';');
    WCHAR wszText[_MAX_PATH+150] = L"";

    if (pwszNextGuids)
    {
        *pwszNextGuids++ = 0;
    }

    CLSIDFromString(pwszGuids, &guid);
    GetProjectTypeMgr()->HrGetProjectFactoryOfGuid(
        guid, &srpProjectFactory);
    srpProjectFactory->QueryInterface(
        IID_IVsAggregatableProjectFactory,
        (void **)&srpAggPF);
    srpAggPF->PreCreateForOuter(pOuter, &srpInner);
    srpInner->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggInner);

    if (pOwner)
    {
        IfFailGo(pOwner->SetInnerProject(srpInner));
    }

    if (pwszNextGuids)
    {
        CComPtr<IUnknown> srpNextInner;
        HrCreateInnerProj(
            pwszNextGuids, pOuter ? pOuter : srpInner,
            srpAggInner, pszFilename, pszLocation, pszName,
            grfCreateFlags, &srpNextInner, pfCanceled);
    }

    return srpAggInner->InitializeForOuter(
        pszFilename, pszLocation, pszName, grfCreateFlags,
        IID_IUnknown, (void **)ppInner, pfCanceled);
}
```

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Flavor>
- [项目子类型](../../extensibility/internals/project-subtypes.md)