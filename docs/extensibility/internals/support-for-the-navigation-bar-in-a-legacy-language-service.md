---
title: 支持旧语言服务中的导航栏 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Navigation bar, supporting in language services [managed package framework]
- language services [managed package framework], Navigation bar
ms.assetid: 2d301ee6-4523-4b82-aedb-be43f352978e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f86dabb0594b1e33c45808efb387fcbe313e3de3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704862"
---
# <a name="support-for-the-navigation-bar-in-a-legacy-language-service"></a>旧版语言服务中的导航栏支持
编辑器视图顶部的导航栏显示文件中的类型和成员。 类型显示在左侧下拉列表中，成员显示在右侧下拉列表中。 当用户选择类型时，care 将放置在类型的第一行上。 当用户选择成员时，该 care 被放置在成员的定义上。 下拉框将更新以反映 caret 的当前位置。

## <a name="displaying-and-updating-the-navigation-bar"></a>显示和更新导航栏
 要支持导航栏，必须从<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>类派生一个类并实现 方法。 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 为语言服务提供代码窗口时，基<xref:Microsoft.VisualStudio.Package.LanguageService>类实例<xref:Microsoft.VisualStudio.Package.CodeWindowManager>化 ，其中包含表示代码窗口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>的对象。 然后<xref:Microsoft.VisualStudio.Package.CodeWindowManager>为对象指定一个新<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>对象。 该方法<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>获取对象<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>。 如果返回类<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars><xref:Microsoft.VisualStudio.Package.CodeWindowManager>的实例，则调用方法<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>以填充内部列表并将<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>对象传递给[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]下拉栏管理器。 下拉栏管理器反过来调用<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.SetDropdownBar%2A><xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>对象上的方法以建立保存两个下拉栏<xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar>的对象。

 当 care 移动时，<xref:Microsoft.VisualStudio.Package.LanguageService.OnIdle%2A>该方法调用<xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A>方法。 基<xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A>方法调用<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A><xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>类中的方法以更新导航栏的状态。 将一组<xref:Microsoft.VisualStudio.Package.DropDownMember>对象传递给此方法。 每个对象表示下拉列表中的条目。

## <a name="the-contents-of-the-navigation-bar"></a>导航栏的内容
 导航栏通常包含类型列表和成员列表。 类型列表包括当前源文件中可用的所有类型。 类型名称包括完整的命名空间信息。 下面是具有两种类型的 C# 代码的示例：

```csharp
namespace TestLanguagePackage
{
    public class TestLanguageService
    {
        internal struct Token
        {
            int tokenID;
        }
        private Tokens[] tokens;
        private string serviceName;
    }
}
```

 类型列表将显示`TestLanguagePackage.TestLanguageService`和`TestLanguagePackage.TestLanguageService.Tokens`。

 成员列表显示类型列表中选择的类型的可用成员。 使用上面的代码示例，如果`TestLanguagePackage.TestLanguageService`所选类型，成员列表将包含私有成员`tokens`和`serviceName`。 不显示内部`Token`结构。

 您可以实现成员列表，使成员的名称加粗，当该卡托放在其中时。 成员也可以以灰显的文本显示，指示它们不在当前位置的作用域内。

## <a name="enabling-support-for-the-navigation-bar"></a>启用导航栏支持
 要启用对导航栏的支持，必须将属性的`ShowDropdownBarOption`<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>参数设置为`true`。 此参数设置 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> 属性。 要支持导航栏，必须在<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars><xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类上的方法中实现对象。

 在 方法的实现<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>中，如果<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A>属性设置为`true`，则可以返回<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>对象。 如果不返回对象，则不显示导航栏。

 用户可以设置显示导航栏的选项，因此可以在编辑器视图打开时重置此控件。 在进行更改之前，用户必须关闭并重新打开编辑器窗口。

## <a name="implementing-support-for-the-navigation-bar"></a>实现对导航栏的支持
 该方法<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>采用两个列表（每个下拉列表一个）和两个值，表示每个列表中的当前选择。 可以更新列表和选择值，在这种情况下，<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>方法必须返回`true`以指示列表已更改。

 随着类型下拉列表中的选择更改，必须更新成员列表以反映新类型。 成员列表中显示的内容可以是：

- 当前类型的成员列表。

- 源文件中的所有成员都可用，但所有成员不是以灰化文本显示的当前类型。 用户仍可以选择灰显成员，以便它们可用于快速导航，但颜色表示它们不是当前所选类型的一部分。

  <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>该方法的实现通常执行以下步骤：

1. 获取源文件的当前声明列表。

     填充列表的方法有很多种。 一种方法是在<xref:Microsoft.VisualStudio.Package.LanguageService>类的版本中创建一个自定义方法，该方法使用返回所有声明<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>列表的自定义解析原因调用该方法。 另一种方法可能是直接从具有自定义<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>解析原因<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>的方法调用 方法。 第三种方法可能是缓存<xref:Microsoft.VisualStudio.Package.AuthoringScope><xref:Microsoft.VisualStudio.Package.LanguageService>类中最后一个完整分析操作返回的类中的声明，并从 方法中<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>检索该声明。

2. 填充或更新类型列表。

     类型列表的内容可能会在源更改或您选择根据当前位置更改类型的文本样式时更新。 请注意，此位置将传递给<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>方法。

3. 根据当前位置确定要在类型列表中选择的类型。

     您可以搜索步骤 1 中获得的声明，以查找包含当前 caret 位置的类型，然后搜索该类型的类型列表以确定其索引到类型列表中。

4. 根据所选类型填充或更新成员列表。

     成员列表反映 **"成员**"下拉列表中当前显示的内容。 如果源已更改或仅显示所选类型的成员且所选类型已更改，则可能需要更新成员列表的内容。 如果选择显示源文件中的所有成员，则需要更新列表中每个成员的文本样式（如果当前选择的类型已更改）。

5. 根据当前关注位置确定要在成员列表中选择的成员。

     在步骤 1 中获取的声明查找包含当前关注位置的成员，然后搜索成员列表以查找该成员以确定其索引到成员列表中。

6. 如果`true`对列表或任一列表中的选择进行了任何更改，则返回。
