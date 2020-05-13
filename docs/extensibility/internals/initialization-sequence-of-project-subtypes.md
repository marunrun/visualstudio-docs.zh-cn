---
title: 项目子类型的初始化序列 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707635"
---
# <a name="initialization-sequence-of-project-subtypes"></a>项目子类型的初始化序列
环境通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>的基础项目工厂实现来构造项目。 当环境确定项目文件扩展名的项目类型 GUID 列表不为空时，项目子类型的构造将开始。 项目文件扩展名和项目 GUID 指定项目是[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]或[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]项目类型。 例如，.vbproj 扩展和 [F184B08F-C81C-45F6-A57F-5ABD9991F28F] 标识[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]项目。

## <a name="environments-initialization-of-project-subtypes"></a>环境对项目子类型的初始化
 以下过程详细介绍了由多个项目子类型聚合的项目系统的初始化序列。

1. 环境调用基础项目的<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>，当项目解析其项目文件时，它发现聚合项目类型 GUIDs 列表不是`null`。 项目停止直接创建其项目。

2. 项目调用`QueryService`<xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject>服务使用环境实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A>的方法创建项目子类型。 在此方法中，环境在遍走项目类型 GUID 的列表时，<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>从<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>最<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A>外层的项目子类型开始，对 的 实现和方法进行递归函数调用。

     下面详细介绍了初始化步骤。

    1. 该方法的环境实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A>调用具有以下函数声明`HrCreateInnerProj`的方法：

         \<代码内容持有者>0</CodeContentPlaceHolder>

         首次`pOuter`调用此函数时，即对于最外层的项目子类型，参数和`pOwner`参数以 as 和 将`null`最外层项目子类型`IUnknown`设置为`pOuter`。

    2. 接下来，环境调用`HrCreateInnerProj`函数，列表中的第二个项目类型 GUID。 此 GUID 对应于聚合序列中向基项目步进的第二个内部项目子类型。

    3. `pOuter`现在指向`IUnknown`最外层项目子类型的 ， 并`HrCreateInnerProj`调用 的<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>实现，然后调用 您的<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>实现 。 在<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>方法中，您通过控制`IUnknown`最外层的项目子类型 。 `pOuter` 拥有的项目（内部项目子类型）需要在此处创建其聚合项目对象。 在方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>实现中，您将指针传递给要聚合`IUnknown`的内部项目的指针。 这两种方法创建聚合对象，您的实现需要遵循 COM 聚合规则，以确保项目子类型最终不会包含对自身的引用计数。

    4. `HrCreateInnerProj`调用 的<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>实现 。 在此方法中，项目子类型执行其初始化工作。 例如，您可以在 中<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A>注册解决方案事件。

    5. `HrCreateInnerProj`递归调用，直到到达列表中的最后一个 GUID（基础项目）。 对于每个调用，重复步骤（c 到 d）。 `pOuter`指向每个聚合级别的最外层项目`IUnknown`子类型。

## <a name="example"></a>示例

下面的示例详细介绍了<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A>由环境实现的方法的近似表示形式中的编程过程。 代码只是一个示例;它不打算编译，并且所有错误检查都被删除，以便清楚。

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
