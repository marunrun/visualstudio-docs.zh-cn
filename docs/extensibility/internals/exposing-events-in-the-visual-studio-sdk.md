---
title: Visual Studio SDK 中公开事件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- events [Visual Studio], exposing
- automation [Visual Studio SDK], exposing events
ms.assetid: 70bbc258-c221-44f8-b0d7-94087d83b8fe
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 29fd9df90f58807ab3d48e077dcfa02d75eff837
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352600"
---
# <a name="expose-events-in-the-visual-studio-sdk"></a>公开 Visual Studio SDK 中的事件
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 允许使用自动化源事件。 我们建议源项目和项目项的事件。

 通过从自动化使用者中检索事件<xref:EnvDTE.DTEClass.Events%2A>对象或<xref:EnvDTE.DTEClass.GetObject%2A>(例如， `GetObject("EventObjectName")`)。 环境调用`IDispatch::Invoke`通过使用`DISPATCH_METHOD`或`DISPATCH_PROPERTYGET`标志返回事件。

 以下过程说明如何返回特定于 VSPackage 的事件。

1. 环境将开始。

2. 它从注册表中读取下的所有值名称**自动化**， **AutomationEvents**，并**AutomationProperties**的所有 Vspackage 和那些名称中的存储密钥表。

3. 自动化使用者调用，在此示例中，`DTE.Events.AutomationProjectsEvents`或`DTE.Events.AutomationProjectItemsEvents`。

4. 在环境表中查找的字符串参数并加载相应的 VSPackage。

5. 环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>方法使用传递的调用中; 在此示例中，名称`AutomationProjectsEvents`或`AutomationProjectItemsEvents`。

6. VSPackage 创建根对象，如具有方法`get_AutomationProjectsEvents`和`get_AutomationProjectItemEvents`，然后返回到该对象的 IDispatch 指针。

7. 环境调用适当的方法基于传递到自动化调用的名称。

8. `get_`方法创建同时实现的另一种基于 IDispatch 的事件对象`IConnectionPointContainer`接口并`IConnectionPoint`接口，并返回`IDispatchpointer`到对象。

   若要通过使用自动化来公开一个事件，您必须响应<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>和向注册表添加的字符串的监视。 在基本项目示例中，字符串是*BscProjectsEvents*并*BscProjectItemsEvents*。

## <a name="registry-entries-from-the-basic-project-sample"></a>从基本项目示例的注册表项
 本部分演示向注册表添加自动化事件值的位置。

 **[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Packages\\<PkgGUID\>\AutomationEvents]**

 **AutomationProjectEvents** = 返回`AutomationProjectEvents`对象。

 **AutomationProjectItemEvents** = 返回`AutomationProjectItemsEvents`对象。

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|默认值 (@)|REG_SZ|未使用|未使用。 数据字段可用于文档。|
|*AutomationProjectsEvents*|REG_SZ|事件对象的名称。|只有密钥的名称为相关。 数据字段可用于文档。<br /><br /> 此示例来自基本项目示例。|
|*AutomationProjectItemEvents*|REG_SZ|事件对象的名称|只有密钥的名称为相关。 数据字段可用于文档。<br /><br /> 此示例来自基本项目示例。|

 当由自动化使用者请求的任何事件对象时，创建具有你的 VSPackage 支持的任何事件的方法的根对象。 环境调用相应`get_`对此对象的方法。 例如，如果`DTE.Events.AutomationProjectsEvents`调用时，`get_AutomationProjectsEvents`调用根对象上的方法。

 ![Visual Studio 项目事件](../../extensibility/internals/media/projectevents.gif "ProjectEvents")事件的自动化模型

 该类`CProjectEventsContainer`表示的源对象*BscProjectsEvents*，和`CProjectItemsEventsContainer`表示的源对象*BscProjectItemsEvents*。

 在大多数情况下，您必须返回的每个事件请求一个新的对象，因为大多数事件对象执行的筛选器对象。 当触发事件时，检查此筛选器来验证正在调用的事件处理程序。

 *AutomationEvents.h*并*AutomationEvents.cpp*包含声明和下表中的类的实现。

|类|描述|
|-----------|-----------------|
|`CAutomationEvents`|实现一个事件根对象，检索从`DTE.Events`对象。|
|`CProjectsEventsContainer` 和 `CProjectItemsEventsContainer`|实现激发相应事件的事件源对象。|

 下面的代码示例演示如何针对事件对象的请求响应。

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

 在上面的代码，`g_wszAutomationProjects`是你的项目集合的名称 (*FigProjects*)， `g_wszAutomationProjectsEvents` (*FigProjectsEvents*) 和`g_wszAutomationProjectItemsEvents`(*FigProjectItemEvents*) 都是项目事件的名称和项目项源自 VSPackage 实现的事件。

 从同一个中心位置，检索事件对象`DTE.Events`对象。 这样一来，所有事件对象都组合在一起，以便最终用户无需浏览整个对象模型以查找特定事件。 这还允许你提供特定的 VSPackage 对象，而不是要求您实现您自己的系统级事件的代码。 但是，为最终用户，用户必须找到的事件在`ProjectItem`接口，它不是立即清除从中检索事件对象。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
