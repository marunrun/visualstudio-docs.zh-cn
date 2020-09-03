---
title: 项目子类型的初始化序列 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 05a3c312f61dd2b2c63c3f38ef8bac2203b326db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707635"
---
# <a name="initialization-sequence-of-project-subtypes"></a>项目子类型的初始化序列
环境通过调用的基本项目工厂实现来构造项目 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> 。 当环境确定项目文件扩展名的项目类型 GUID 列表不为空时，将开始构造项目子类型。 项目文件扩展名和项目 GUID 指定项目是否为 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 或 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目类型。 例如，.vbproj extension 和 {F184B08F-C81C-45F6-A57F-5ABD9991F28F} 标识 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目。

## <a name="environments-initialization-of-project-subtypes"></a>环境初始化项目子类型
 下面的过程详细说明了由多个项目子类型聚合的项目系统的初始化顺序。

1. 环境调用基本项目的，而 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> 项目分析其项目文件，而该项目文件发现聚合项目类型 guid 列表不是 `null` 。 项目将直接停止创建其项目。

2. 项目 `QueryService` 在服务上调用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> ，以使用该方法的环境实现创建项目子类型 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> 。 在此方法中，环境在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> 遍历项目类型 guid （从最外面的项目子类型开始）的列表时对的实现和方法进行递归函数调用。

     下面详细介绍了初始化步骤。

    1. 环境的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> 方法实现 `HrCreateInnerProj` 通过以下函数声明调用方法：

         \<CodeContentPlaceHolder>0</CodeContentPlaceHolder>

         当首次调用此函数时（即，对于最外面的项目子类型），参数 `pOuter` 和 `pOwner` 作为传入， `null` 并且函数将最外面的项目子类型设置 `IUnknown` 为 `pOuter` 。

    2. 接下来，环境调用 `HrCreateInnerProj` 函数，该函数具有列表中的第二个项目类型 GUID。 此 GUID 对应于第二个内部项目子类型单步执行到聚合序列中的基础项目。

    3. `pOuter`现在指向 `IUnknown` 最外面的项目子类型的，然后调用的实现，然后调用的实现 `HrCreateInnerProj` <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> 。 在中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> ，可以在 `IUnknown` 最外面的项目子类型的控制中传递 `pOuter` 。 所拥有的项目 (内部项目子类型) 需要在此创建其聚合项目对象。 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> 方法实现中，传递到要 `IUnknown` 聚合的内部项目的的指针。 这两种方法创建聚合对象，而您的实现需要遵循 COM 聚合规则，以确保项目子类型不会在其自身上保持引用计数。

    4. `HrCreateInnerProj` 调用的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> 。 在此方法中，项目子类型执行其初始化工作。 例如，你可以在中注册解决方案事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> 。

    5. `HrCreateInnerProj` 将以递归方式调用，直到到达列表中的基本项目)  (。 对于每个调用，将重复步骤 c 到 d。 `pOuter` 指向每个聚合级别的最外面的项目子类型 `IUnknown` 。

## <a name="example"></a>示例

下面的示例详细介绍了方法在环境实现时的近似表示形式的编程过程 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> 。 此代码只是一个示例;它不会进行编译，并且为了清楚起见，删除了所有错误检查。

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

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Flavor>
- [项目子类型](../../extensibility/internals/project-subtypes.md)
