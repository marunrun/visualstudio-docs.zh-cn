---
title: 公开项目对象 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project objects, exposing
- extensibility, project objects
ms.assetid: 5bb24967-434a-4ef4-87a0-2f3250c9e22d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 81446fa582524872b03199ae707f658776787961
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708475"
---
# <a name="expose-project-objects"></a>公开项目对象

自定义项目类型可以提供自动化对象，以允许使用自动化接口访问项目。 每个项目类型都需要提供 <xref:EnvDTE.Project> 从访问的标准自动化对象 <xref:EnvDTE.Solution> ，其中包含 IDE 中打开的所有项目的集合。 项目中的每一项都应由 <xref:EnvDTE.ProjectItem> 使用访问的对象公开 `Project.ProjectItems` 。 除了这些标准自动化对象之外，项目还可以选择提供项目特定的自动化对象。

您可以使用或创建自定义根级别的自动化对象，这些对象可从根 DTE 对象进行后期绑定访问 `DTE.<customObjectName>` `DTE.GetObject("<customObjectName>")` 。 例如，Visual C++ 创建一个名为 *VCProjects* 的 c + + 项目特定的项目集合，你可以使用或访问该集合 `DTE.VCProjects` `DTE.GetObject("VCProjects")` 。 你还可以创建一个 `Project.Object` ，它对于项目类型是唯一的，它 `Project.CodeModel` 可以查询其最常派生的对象以及 `ProjectItem` 公开 `ProjectItem.Object` 和的 `ProjectItem.FileCodeModel` 。

这是一种常见的项目约定，可用于公开特定于项目的自定义项目集合。 例如， [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 创建一个 c + + 特定的项目集合，然后可以使用或访问该集合 `DTE.VCProjects` `DTE.GetObject("VCProjects")` 。 你还可以创建一个 `Project.Object` ，它对于项目类型是唯一的，它 `Project.CodeModel` 可以查询其最常派生的对象（即 `ProjectItem` 公开 `ProjectItem.Object` 和的） `ProjectItem.FileCodeModel` 。

## <a name="to-contribute-a-vspackage-specific-object-for-a-project"></a>为项目提供特定于 VSPackage 的对象

1. 将相应的密钥添加到 VSPackage 的 *.pkgdef* 文件。

     例如，以下是 c + + 语言项目的 *.pkgdef* 设置：

    ```
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\Automation]
    "VCProjects"=""
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\AutomationEvents]
    "VCProjectEngineEventsObject"=""
    ```

2. 实现方法中的代码 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> ，如以下示例中所示。

    ```cpp
    STDMETHODIMP CVsPackage::GetAutomationObject(
    /* [in]  */ LPCOLESTR       pszPropName,
    /* [out] */ IDispatch **    ppIDispatch)
    {
    ExpectedPtrRet(pszPropName);
    ExpectedPtrRet(ppIDispatch);
    *ppIDispatch = NULL;

        if (m_fZombie)
            return E_UNEXPECTED;

        if (_wcsicmp(pszPropName, g_wszAutomationProjects) == 0)
        {
            return GetAutomationProjects(ppIDispatch);
        }
        else if (_wcsicmp(pszPropName, g_wszAutomationProjectsEvents) == 0)
        {
            return CAutomationEvents::GetAutomationEvents(ppIDispatch);
        }
        else if (_wcsicmp(pszPropName, g_wszAutomationProjectItemsEvents) == 0)
        {
            return CAutomationEvents::GetAutomationEvents(ppIDispatch);
        }
        return E_INVALIDARG;
    }
    ```

     在代码中， `g_wszAutomationProjects` 是项目集合的名称。 `GetAutomationProjects`方法创建一个对象，该对象实现 `Projects` 接口并返回 `IDispatch` 指向调用对象的指针，如下面的代码示例中所示。

    ```cpp
    HRESULT CVsPackage::GetAutomationProjects(/* [out] */ IDispatch ** ppIDispatch)
    {
        ExpectedPtrRet(ppIDispatch);
        *ppIDispatch = NULL;

        if (!m_srpAutomationProjects)
        {
            HRESULT hr = CACProjects::CreateInstance(&m_srpAutomationProjects);
            IfFailRet(hr);
            ExpectedExprRet(m_srpAutomationProjects != NULL);
        }
        return m_srpAutomationProjects.CopyTo(ppIDispatch);
    }
    ```

     为自动化对象选择唯一的名称。 名称冲突是不可预测的，如果多个项目类型使用相同的名称，则冲突会导致随机引发冲突的对象名称。 应在自动化对象的名称中包含公司名称或其产品名称的某个独特方面。

     `Projects`对于项目自动化模型的其余部分，自定义集合对象是一个便捷入口点。 你的项目对象也可以从 <xref:EnvDTE.Solution> 项目集合进行访问。 创建了为使用者提供集合对象的相应代码和注册表项后 `Projects` ，实现必须为项目模型提供剩余的标准对象。 有关详细信息，请参阅 [项目建模](../../extensibility/internals/project-modeling.md)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
