---
title: 在可视化工作室 SDK 中公开事件 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708488"
---
# <a name="expose-events-in-the-visual-studio-sdk"></a>在可视化工作室 SDK 中公开事件
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]允许您使用自动化来源事件。 我们建议您为项目和项目项源事件。

 事件由自动化使用者从<xref:EnvDTE.DTEClass.Events%2A>对象或<xref:EnvDTE.DTEClass.GetObject%2A>（例如）`GetObject("EventObjectName")`检索。 环境通过使用`IDispatch::Invoke``DISPATCH_METHOD`或`DISPATCH_PROPERTYGET`标志来调用事件。

 以下过程说明如何返回特定于 VSPackage 的事件。

1. 环境开始。

2. 它从注册表读取所有 VSPackages 的**自动化**、**自动化事件**和**自动化属性**键下的所有值名称，并将这些名称存储在表中。

3. 自动化使用者调用，在此示例中，`DTE.Events.AutomationProjectsEvents`或`DTE.Events.AutomationProjectItemsEvents`。

4. 环境在表中查找字符串参数并加载相应的 VSPackage。

5. 环境使用调用中<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>传递的名称调用方法;使用 调用中传递的名称调用 方法。在此示例中，`AutomationProjectsEvents`或`AutomationProjectItemsEvents`。

6. VSPackage 创建具有 方法（如`get_AutomationProjectsEvents`和`get_AutomationProjectItemEvents`，然后返回指向该对象的 IDispatch 指针）的根对象。

7. 环境根据传入自动化调用的名称调用适当的方法。

8. 该方法`get_`创建另一个基于 IDispatch 的事件对象，该`IConnectionPointContainer`对象同时实现`IConnectionPoint`接口和接口，`IDispatchpointer`并将 返回 到该对象。

   要使用自动化公开事件，必须响应<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>并监视添加到注册表中的字符串。 在基本项目示例中，字符串是*BscProjects 事件*和*BscProjectItem 事件*。

## <a name="registry-entries-from-the-basic-project-sample"></a>基本项目示例中的注册表项
 本节显示向注册表添加自动化事件值的位置。

 **[HKEY_LOCAL_MACHINE_SOFTWARE_微软_VisualStudio_8.0_包\\<PkgGUID\>[自动化事件]**

 **自动化项目事件**=`AutomationProjectEvents`返回对象。

 **自动化项目项目事件**=`AutomationProjectItemsEvents`返回对象。

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|默认值 （*）|REG_SZ|未使用|未使用。 您可以使用数据字段进行文档记录。|
|*自动化项目事件*|REG_SZ|事件对象的名称。|只有键名称相关。 您可以使用数据字段进行文档记录。<br /><br /> 此示例来自基本项目示例。|
|*自动化项目项目事件*|REG_SZ|事件对象的名称|只有键名称相关。 您可以使用数据字段进行文档记录。<br /><br /> 此示例来自基本项目示例。|

 当自动化使用者请求任何事件对象时，请创建一个根对象，该对象具有 VSPackage 支持的任何事件的方法。 环境在此对象上调用`get_`适当的方法。 例如，如果`DTE.Events.AutomationProjectsEvents`调用，则调用根`get_AutomationProjectsEvents`对象上的方法。

 ![可视化工作室项目活动](../../extensibility/internals/media/projectevents.gif "ProjectEvents")事件的自动化模型

 类`CProjectEventsContainer`表示*BscProjectsEvents*的源对象，表示`CProjectItemsEventsContainer` *BscProjectItems事件的*源对象。

 在大多数情况下，必须为每个事件请求返回一个新对象，因为大多数事件对象都采用筛选器对象。 触发事件时，请检查此筛选器以验证是否正在调用事件处理程序。

 *自动化事件.h*和*自动化事件.cpp*包含下表中类的声明和实现。

|类|描述|
|-----------|-----------------|
|`CAutomationEvents`|实现从`DTE.Events`对象检索的事件根对象。|
|`CProjectsEventsContainer` 和 `CProjectItemsEventsContainer`|实现触发相应事件的事件源对象。|

 以下代码示例演示如何响应事件对象的请求。

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

 在上面`g_wszAutomationProjects`的代码中，是项目集合 *（FigProjects）*`g_wszAutomationProjectsEvents`的名称 *（FigProjects）* 和`g_wszAutomationProjectItemsEvents`*（FigProject事件*）是从 VSPackage 实现来源的项目事件和项目项目事件的名称。

 从同一中心位置（该对象）`DTE.Events`检索事件对象。 这样，所有事件对象都分组在一起，以便最终用户不必浏览整个对象模型来查找特定事件。 这还允许您提供特定的 VSPackage 对象，而不是要求您为系统范围的事件实现自己的代码。 但是，对于最终用户，他们必须为您的`ProjectItem`接口查找事件，则无法立即从何处检索该事件对象。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
