---
title: 在 Visual Studio SDK 中公开事件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- events [Visual Studio], exposing
- automation [Visual Studio SDK], exposing events
ms.assetid: 70bbc258-c221-44f8-b0d7-94087d83b8fe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 48f1e0ea0dcd07bbc26fc89d5c61a6a5941d4727
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708488"
---
# <a name="expose-events-in-the-visual-studio-sdk"></a>在 Visual Studio SDK 中公开事件
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 允许使用自动化来源事件。 建议你为项目和项目项提供源事件。

 自动使用者从 <xref:EnvDTE.DTEClass.Events%2A> 对象或 (检索事件 <xref:EnvDTE.DTEClass.GetObject%2A> ，例如 `GetObject("EventObjectName")`) 。 环境 `IDispatch::Invoke` 通过使用 `DISPATCH_METHOD` 或 `DISPATCH_PROPERTYGET` 标志返回事件来调用。

 以下过程说明如何返回 VSPackage 特定的事件。

1. 环境启动。

2. 它从注册表中读取所有 Vspackage 的 **Automation**、 **AutomationEvents**和 **automationproperties.livesetting** 键下的所有值名称，并将这些名称存储在表中。

3. 自动化使用者调用，在此示例中为 `DTE.Events.AutomationProjectsEvents` 或 `DTE.Events.AutomationProjectItemsEvents` 。

4. 环境查找表中的字符串参数并加载相应的 VSPackage。

5. 环境 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 通过使用调用中传递的名称（在此示例中为或）调用方法 `AutomationProjectsEvents` `AutomationProjectItemsEvents` 。

6. VSPackage 创建一个具有和等方法的根对象， `get_AutomationProjectsEvents` `get_AutomationProjectItemEvents` 然后返回指向该对象的 IDispatch 指针。

7. 环境根据传递到自动化调用中的名称调用适当的方法。

8. `get_`方法创建另一个基于 IDispatch 的事件对象，该对象实现 `IConnectionPointContainer` 接口和 `IConnectionPoint` 接口，并将返回 `IDispatchpointer` 到对象。

   若要使用自动化公开事件，必须响应 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 并监视添加到注册表中的字符串。 在基本项目示例中，字符串是 *BscProjectsEvents* 和 *BscProjectItemsEvents*。

## <a name="registry-entries-from-the-basic-project-sample"></a>基本项目示例中的注册表项
 本部分介绍将自动化事件值添加到注册表的位置。

 **[HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\VisualStudio\8.0\Packages \\<PkgGUID \> \AutomationEvents]**

 **AutomationProjectEvents** = 返回 `AutomationProjectEvents` 对象。

 **AutomationProjectItemEvents** = 返回 `AutomationProjectItemsEvents` 对象。

|名称|类型|范围|说明|
|----------|----------|-----------|-----------------|
|默认 ( @ ) |REG_SZ|未使用|未使用。 您可以使用数据字段来查看文档。|
|*AutomationProjectsEvents*|REG_SZ|事件对象的名称。|仅密钥名称是相关的。 您可以使用数据字段来查看文档。<br /><br /> 此示例来自基本的项目示例。|
|*AutomationProjectItemEvents*|REG_SZ|事件对象的名称|仅密钥名称是相关的。 您可以使用数据字段来查看文档。<br /><br /> 此示例来自基本的项目示例。|

 当自动化使用者请求你的任何事件对象时，请创建一个根对象，该对象具有适用于你的 VSPackage 支持的任何事件的方法。 环境对此对象调用适当的 `get_` 方法。 例如，如果 `DTE.Events.AutomationProjectsEvents` 调用了，则将 `get_AutomationProjectsEvents` 调用根对象上的方法。

 ![Visual Studio 项目事件](../../extensibility/internals/media/projectevents.gif "ProjectEvents") 事件的自动化模型

 类 `CProjectEventsContainer` 表示 *BscProjectsEvents*的源对象， `CProjectItemsEventsContainer` 表示 *BscProjectItemsEvents*的源对象。

 在大多数情况下，你必须为每个事件请求返回一个新的对象，因为大多数事件对象都带有筛选器对象。 触发事件时，请检查此筛选器以验证是否正在调用事件处理程序。

 *AutomationEvents* 和 *AutomationEvents* 包含下表中的类的声明和实现。

|类|说明|
|-----------|-----------------|
|`CAutomationEvents`|实现从对象检索的事件根对象 `DTE.Events` 。|
|`CProjectsEventsContainer` 和 `CProjectItemsEventsContainer`|实现触发相应事件的事件源对象。|

 下面的代码示例演示如何响应事件对象的请求。

```cpp
STDMETHODIMP CVsPackage::GetAutomationObject(
    /* [in]  */ LPCOLESTR       pszPropName,
    /* [out] */ IDispatch **    ppIDispatch)
{
    ExpectedPtrRet(ppIDispatch);
    *ppIDispatch = NULL;

    if (_wcsicmp(pszPropName, g_wszAutomationProjects) == 0)
        //Is the requested name our Projects object?
    {
        return GetAutomationProjects(ppIDispatch);
        // Gets our Projects object.
    }
    else if (_wcsicmp(pszPropName, g_wszAutomationProjectsEvents) == 0)
        //Is the requested name our ProjectsEvents object?
    {
        return CAutomationEvents::GetAutomationEvents(ppIDispatch);
          // Gets our ProjectEvents object.
    }
    else if (_wcsicmp(pszPropName, g_wszAutomationProjectItemsEvents) == 0)  //Is the requested name our ProjectsItemsEvents object?
    {
        return CAutomationEvents::GetAutomationEvents(ppIDispatch);
          // Gets our ProjectItemsEvents object.
    }
    return E_INVALIDARG;
}
```

 在上面的代码中， `g_wszAutomationProjects` 是项目集合的名称 (*FigProjects*) ， `g_wszAutomationProjectsEvents` (*FigProjectsEvents*) ， `g_wszAutomationProjectItemsEvents` (*FigProjectItemEvents*) 是源自 VSPackage 实现的项目事件和项目项事件的名称。

 从同一中心位置（即对象）检索事件对象 `DTE.Events` 。 这样一来，所有事件对象将组合在一起，这样最终用户便无需浏览整个对象模型即可查找特定的事件。 这还允许你提供特定的 VSPackage 对象，而不是要求你为系统范围内的事件实现你自己的代码。 但对于最终用户，如果用户必须找到接口的事件，则 `ProjectItem` 不会立即明确从该事件对象检索到的位置。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
