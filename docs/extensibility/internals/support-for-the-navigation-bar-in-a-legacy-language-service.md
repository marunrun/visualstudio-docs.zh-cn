---
title: 旧版语言服务中的导航栏支持 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Navigation bar, supporting in language services [managed package framework]
- language services [managed package framework], Navigation bar
ms.assetid: 2d301ee6-4523-4b82-aedb-be43f352978e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cccfd98bdd126c69baeddaf5151c7ece3f6ec331
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309785"
---
# <a name="support-for-the-navigation-bar-in-a-legacy-language-service"></a>旧版语言服务中的导航栏支持
在的编辑器视图顶部的导航栏显示文件中的类型和成员。 在左侧的下拉列表中显示类型和成员显示在右侧下拉列表。 当用户选择一种类型时，该类型的第一行放置插入符号。 当用户选择成员时，将插入符号放置在上成员的定义。 下拉列表框会更新以反映当前插入符号的位置。

## <a name="displaying-and-updating-the-navigation-bar"></a>显示和更新的导航栏
 若要支持的导航栏，您必须从派生类<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>类，实现<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>方法。 语言服务时提供的代码窗口中，基<xref:Microsoft.VisualStudio.Package.LanguageService>类实例化<xref:Microsoft.VisualStudio.Package.CodeWindowManager>，其中包含<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>对象，表示代码窗口。 <xref:Microsoft.VisualStudio.Package.CodeWindowManager>对象然后提供一个新<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>对象。 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>方法获取<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>对象。 如果返回的实例，你<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>类，<xref:Microsoft.VisualStudio.Package.CodeWindowManager>调用你<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>方法来填充内部列出，并将传递您<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>对象传递给[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]管理器栏的下拉列表。 下拉列表条形管理器中，依次调用<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.SetDropdownBar%2A>方法在你<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>对象建立<xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar>对象，它包含两个下拉条。

 当插入符号移动时，<xref:Microsoft.VisualStudio.Package.LanguageService.OnIdle%2A>方法调用<xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A>方法。 基<xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A>方法调用<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>中的方法在<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>类来更新导航栏的状态。 通过一系列<xref:Microsoft.VisualStudio.Package.DropDownMember>给此方法的对象。 每个对象表示下拉列表中的条目。

## <a name="the-contents-of-the-navigation-bar"></a>导航栏中的内容
 在导航栏通常包含一组类型和成员的列表。 类型的列表包括当前源文件中的所有可用的类型。 类型名称包括完整的命名空间信息。 以下是两种类型的 C# 代码示例：

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

 成员列表显示在类型列表中选择的类型的可用成员。 如果使用上面的代码示例`TestLanguagePackage.TestLanguageService`是所选的类型成员列表将包含私有成员`tokens`和`serviceName`。 内部结构`Token`不会显示。

 您可以实现以使成员的名称时将插入符号放置在它变为加粗的成员列表。 成员也可以显示中灰显文本，指示它们并不在当前放置插入符号的作用域内。

## <a name="enabling-support-for-the-navigation-bar"></a>启用对导航栏的支持
 若要启用对导航栏的支持，必须设置`ShowDropdownBarOption`的参数<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>属性为`true`。 此参数设置 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> 属性。 若要支持的导航栏，则必须实现<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>中的对象<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>方法<xref:Microsoft.VisualStudio.Package.LanguageService>类。

 中的实现<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>方法中，如果<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A>属性设置为`true`，可以返回<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>对象。 如果未返回对象，不会显示在导航栏。

 因此可以为此控件要重置编辑器视图处于打开状态时，用户，可以设置显示导航栏的选项。 用户必须关闭并重新打开编辑器窗口，更改发生之前。

## <a name="implementing-support-for-the-navigation-bar"></a>实现对导航栏的支持
 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>方法采用两个列表 （一个用于每个下拉列表） 和两个值表示当前选定内容的每个列表中。 列表和选择值可以更新，在这种情况下<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>方法必须返回`true`以指示已更改的列表。

 当所选内容更改类型下拉列表中时，必须更新成员列表以反映新的类型。 在成员列表中显示的内容可以是：

- 当前类型的成员的列表。

- 所有可用的成员源中的文件，但与不在当前类型的所有成员显示在灰显文本。 用户仍可以选择灰显成员，因此它们可以用于快速导航栏中，但颜色来表示它们不是当前所选类型的一部分。

  实现<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>方法通常执行以下步骤：

1. 获取当前声明的源文件的列表。

     有多种方法来填充的列表。 一种方法是在你的版本上创建自定义方法<xref:Microsoft.VisualStudio.Package.LanguageService>类，该类调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法使用自定义分析原因返回的所有声明的列表。 另一种方法可能是通过调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法直接从<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>，原因是自定义分析的方法。 第三种方法可能是缓存中的声明<xref:Microsoft.VisualStudio.Package.AuthoringScope>类中的最后一个完整分析操作返回<xref:Microsoft.VisualStudio.Package.LanguageService>类，并检索从<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>方法。

2. 填充或更新的类型的列表。

     类型列表的内容可能会更新源发生更改时，或如果已选择要更改基于当前插入符号位置的类型的文本样式。 请注意，此位置传递到<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>方法。

3. 确定要基于当前插入符号位置的类型列表中选择的类型。

     您可以在步骤 1 以查找包含当前插入符号位置的类型中搜索获得的声明，然后搜索以确定其索引的类型列表到该类型的类型列表。

4. 填充或更新基于所选类型的成员的列表。

     成员列表中当前显示的内容将反映**成员**下拉列表。 成员列表的内容可能需要更新如果源已更改，或如果您要显示只有所选类型的成员，并且所选的类型已更改。 如果您选择显示源代码文件中的所有成员，在列表中每个成员的文本样式将需要更新如果当前所选的类型已更改。

5. 确定要在基于当前插入符号位置的成员列表中选择的成员。

     搜索获得的声明在步骤 1 中的成员，其中包含当前插入符号位置，然后搜索该成员以确定其索引到成员列表中的成员列表。

6. 返回`true`如果为列表或任一列表中的选择进行了任何更改。