---
title: 旧版语言服务中对导航栏的支持 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80704862"
---
# <a name="support-for-the-navigation-bar-in-a-legacy-language-service"></a>旧版语言服务中的导航栏支持
编辑器视图顶部的导航栏显示文件中的类型和成员。 类型显示在左侧的下拉框中，成员显示在右侧下拉框中。 当用户选择某一类型时，插入符号会置于该类型的第一行。 当用户选择某个成员时，插入符号会被放置在该成员的定义上。 下拉框会进行更新，以反映插入符号的当前位置。

## <a name="displaying-and-updating-the-navigation-bar"></a>显示和更新导航栏
 若要支持导航栏，你必须从类派生一个类 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 并实现 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 方法。 向语言服务提供代码窗口时，基类将 <xref:Microsoft.VisualStudio.Package.LanguageService> 实例化 <xref:Microsoft.VisualStudio.Package.CodeWindowManager> ，其中包含 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> 表示代码窗口的对象。 <xref:Microsoft.VisualStudio.Package.CodeWindowManager>然后，为对象提供新的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 对象。 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>方法获取一个 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 对象。 如果返回类的实例 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> ，则会 <xref:Microsoft.VisualStudio.Package.CodeWindowManager> 调用 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 方法来填充内部列表，并将 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 对象传递给 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 下拉列表管理器。 下拉栏管理器反过来调用 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.SetDropdownBar%2A> 对象上的方法 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 来建立 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar> 包含两个下拉栏的对象。

 当插入符号移动时， <xref:Microsoft.VisualStudio.Package.LanguageService.OnIdle%2A> 方法将调用 <xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A> 方法。 基 <xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A> 方法调用 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 类中的方法 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 来更新导航栏的状态。 <xref:Microsoft.VisualStudio.Package.DropDownMember>向此方法传递一组对象。 每个对象都表示下拉中的一个条目。

## <a name="the-contents-of-the-navigation-bar"></a>导航栏的内容
 导航栏通常包含类型列表和成员列表。 类型列表包括当前源文件中所有可用的类型。 类型名称包括完整的命名空间信息。 下面是一个具有两种类型的 c # 代码示例：

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

 "类型" 列表将显示 `TestLanguagePackage.TestLanguageService` 和 `TestLanguagePackage.TestLanguageService.Tokens` 。

 "成员" 列表显示在 "类型" 列表中选择的类型的可用成员。 使用上述代码示例时，如果 `TestLanguagePackage.TestLanguageService` 是所选的类型，则 "成员" 列表将包含私有成员 `tokens` 和 `serviceName` 。 `Token`不显示内部结构。

 您可以实现成员列表，以便在将插入符号放置在它的位置时，将成员的名称设置为粗体。 成员还可以显示为灰色的文本，指示它们不在当前插入符号的范围内。

## <a name="enabling-support-for-the-navigation-bar"></a>启用对导航栏的支持
 若要启用对导航栏的支持，您必须将 `ShowDropdownBarOption` 属性的参数设置 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 为 `true` 。 此参数设置 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> 属性。 若要支持导航栏，您必须 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 在类的方法中实现对象 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> 。

 在方法的实现中 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> ，如果 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> 属性设置为 `true` ，则可以返回 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 对象。 如果不返回对象，则不会显示导航栏。

 用户可以设置用于显示导航栏的选项，因此在编辑器视图处于打开状态时，可以重置此控件。 在发生更改之前，用户必须关闭并重新打开编辑器窗口。

## <a name="implementing-support-for-the-navigation-bar"></a>实现对导航栏的支持
 此 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 方法采用两个列表，每个下拉)  (一个列表，两个值表示每个列表中的当前选定内容。 可以更新列表和选择值，在这种情况下，该 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 方法必须返回 `true` 以指示列表已更改。

 在 "类型" 下拉列表中选择 "更改" 时，必须更新 "成员" 列表以反映新的类型。 "成员" 列表中显示的内容可以是：

- 当前类型的成员列表。

- 源文件中所有可用的成员，但对于不在当前类型中的所有成员，将以灰色文本显示。 用户仍可以选择灰显的成员，以便它们可用于快速导航，但颜色指示它们不是当前所选类型的一部分。

  方法的实现 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 通常会执行以下步骤：

1. 获取源文件的当前声明的列表。

     可以通过多种方式来填充列表。 一种方法是在类的版本上创建一个自定义方法 <xref:Microsoft.VisualStudio.Package.LanguageService> ，该方法调用方法，该方法 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 具有一个返回所有声明的列表的自定义分析原因。 另一种方法可能是 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 从方法中直接调用方法 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> ，自定义分析原因。 第三种方法可能是缓存类中 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 最后一个完整分析操作返回的类中的声明 <xref:Microsoft.VisualStudio.Package.LanguageService> ，并从方法中检索该声明 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 。

2. 填充或更新类型列表。

     如果源已更改，或者如果已选择基于当前插入符号位置更改类型的文本样式，则可能会更新类型列表的内容。 请注意，此位置将传递给 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 方法。

3. 根据当前的插入符号位置，确定要在 "类型" 列表中选择的类型。

     您可以搜索在步骤1中获取的声明，查找包含当前插入符号位置的类型，然后在 "类型" 列表中搜索该类型以确定其索引到 "类型" 列表中。

4. 基于所选类型填充或更新成员列表。

     成员列表反映了 " **成员** " 下拉列表中当前显示的内容。 如果源已更改，或者仅显示所选类型的成员，并且所选类型已更改，则可能需要更新 members 列表的内容。 如果选择显示源文件中的所有成员，则在当前选定的类型发生更改的情况下，需要更新列表中每个成员的文本样式。

5. 根据当前的插入符号位置，确定要在 "成员" 列表中选择的成员。

     在步骤1中为包含当前插入符号位置的成员搜索在步骤1中获得的声明，然后在 "成员列表" 中搜索该成员，以确定它在成员列表中的索引。

6. 如果对列表 `true` 或任一列表中的选择进行了任何更改，则返回。
