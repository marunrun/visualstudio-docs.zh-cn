---
title: 项目子类型的初始化序列 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c5594d54c188c2f561dd66229e808e48068ba41a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192657"
---
# <a name="initialization-sequence-of-project-subtypes"></a>项目子类型的初始化序列
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在环境构造一个项目，通过调用基础项目工厂实现的<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>。 项目子类型的构造启动时环境确定项目文件的扩展名的项目类型 GUID 列表不为空。 项目文件扩展名和项目 GUID 指定项目是否是[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]或[!INCLUDE[csprcs](../../includes/csprcs-md.md)]项目类型。 例如，.vbproj 扩展名和 {F184B08F-C81C-45F6-A57F-5ABD9991F28F} 识别[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]项目。  
  
## <a name="environments-initialization-of-project-subtypes"></a>项目子类型的环境的初始化  
 以下过程详细说明了通过多个项目子类型进行聚合的项目系统的初始化序列。  
  
1. 环境调用的基础项目<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>，并在项目分析其项目文件时发现聚合的项目类型 Guid 列表不是`null`。 项目会终止直接创建它的项目。  
  
2. 项目调用`QueryService`上<xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject>服务，以创建项目子类型使用的环境实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A>方法。 在此方法内环境提供对您的实现的递归函数调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>，`M:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject(System.Object)`和<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A>方法时它遍历项目的列表类型，从最外面的项目子类型的 Guid。  
  
    下面详细介绍的初始化步骤。  
  
   1. 环境的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A>方法调用 HrCreateInnerProj '' 与以下函数声明的方法：  
  
       ```  
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
           BOOL *pfCancelled  
       )  
       ```  
  
        当调用此函数是第一次，即最外面的项目子类型，参数`pOuter`并`pOwner`作为传入`null`和该函数将设置最外层项目子类型`IUnknown`到`pOuter`。  
  
   2. 接下来环境调用`HrCreateInnerProj`函数与列表中的第二个项目类型 GUID。 此 GUID 与单步执行向聚合序列中的基础项目的第二个内部项目子类型相对应。  
  
   3. `pOuter`现在会指向`IUnknown`的最外层项目子类型，并`HrCreateInnerProj`调用的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>跟于特定的实现调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>。 在中<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>方法传入控制`IUnknown`的最外层项目子类型， `pOuter`。 需要创建其的聚合项目对象所拥有的项目 （内部项目子类型）。 在中<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>方法实现中指向的指针传递`IUnknown`正在聚合的内部项目。 这两种方法创建的聚合对象，并且您的实现需要遵循 COM 聚合规则，以确保项目子类型不结束存储到其自身的引用计数。  
  
   4. `HrCreateInnerProj` 调用的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>。 在此方法中，项目子类型执行的初始化工作。 例如，可以注册中的解决方案事件<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A>。  
  
   5. `HrCreateInnerProj` 调用，以递归方式直到达到在列表中的最后一个 GUID （基项目）。 对于每个这些调用，重复步骤 c 到 d。 `pOuter` 指向最外面的项目子类型`IUnknown`每个级别的聚合。  
  
   下面的示例详细介绍近似表示形式中的编程过程<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A>作为它的方法实现由环境。 该代码只是一个示例;它不是要编译和所有错误检查为清楚起见已都删除。  
  
## <a name="example"></a>示例  
  
### <a name="code"></a>代码  
  
```  
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
 <xref:Microsoft.VisualStudio.Shell.Flavor>   
 [项目子类型](../../extensibility/internals/project-subtypes.md)
