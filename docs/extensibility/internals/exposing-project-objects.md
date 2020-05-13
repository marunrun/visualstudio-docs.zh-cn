---
title: 公开项目对象 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708475"
---
# <a name="expose-project-objects"></a>公开项目对象

自定义项目类型可以提供自动化对象，以便允许使用自动化接口访问项目。 每个项目类型都应提供从<xref:EnvDTE.Project><xref:EnvDTE.Solution>访问的标准自动化对象，该对象包含 IDE 中打开的所有项目的集合。 项目中的每个项都应被访问<xref:EnvDTE.ProjectItem>`Project.ProjectItems`的对象公开。 除了这些标准自动化对象之外，项目还可以选择提供特定于项目的自动化对象。

您可以创建自定义根级自动化对象，可以使用 或`DTE.<customObjectName>``DTE.GetObject("<customObjectName>")`从根 DTE 对象访问后期绑定对象。 例如，Visual C++创建一个名为*VCProjects*的项目C++项目集合，您可以使用`DTE.VCProjects`或`DTE.GetObject("VCProjects")`进行访问。 还可以创建一个`Project.Object`对于项目类型是唯一的`Project.CodeModel`，可以查询其最派生的对象 ， 以及 公开`ProjectItem``ProjectItem.Object`和`ProjectItem.FileCodeModel`的 。

它是项目公开自定义、特定于项目的项目集合的常见约定。 例如，[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]创建C++特定的项目集合，然后可以使用`DTE.VCProjects`或`DTE.GetObject("VCProjects")`进行访问。 还可以创建一个`Project.Object`对于项目类型是唯一的`Project.CodeModel`，可以查询其最派生的对象 ， 公开`ProjectItem``ProjectItem.Object`的 和 。 `ProjectItem.FileCodeModel`

## <a name="to-contribute-a-vspackage-specific-object-for-a-project"></a>为项目贡献特定于 VSPackage 的对象

1. 将适当的键添加到 VSPackage 的 *.pkgdef*文件。

     例如，以下是C++语言项目的 *.pkgdef*设置：

    ```
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\Automation]
    "VCProjects"=""
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\AutomationEvents]
    "VCProjectEngineEventsObject"=""
    ```

2. 在方法中实现代码<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>，如以下示例所示。

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

     在代码中，`g_wszAutomationProjects`是项目集合的名称。 该方法`GetAutomationProjects`创建一个实现`Projects`接口并返回指向调用对象的`IDispatch`指针的对象，如下代码示例所示。

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

     为自动化对象选择唯一名称。 名称冲突不可预测，如果多个项目类型使用相同的名称，冲突会导致任意抛出冲突的对象名称。 您应该在自动化对象的名称中包括公司名称或其产品名称的某些独特方面。

     自定义`Projects`集合对象是项目自动化模型其余部分的方便入口点。 项目对象还可以从<xref:EnvDTE.Solution>项目集合访问。 创建向使用者提供`Projects`集合对象的相应代码和注册表项后，实现必须为项目模型提供剩余的标准对象。 有关详细信息，请参阅[项目建模](../../extensibility/internals/project-modeling.md)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
