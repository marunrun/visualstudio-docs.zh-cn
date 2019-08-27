---
title: 旧版语言服务中重新格式化代码 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- reformatting code, supporting in language services [managed package framework]
- language services [managed package framework], reformatting code
ms.assetid: 08bb3375-8fef-4f4e-9efa-0d7333bab0eb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 16130191eb6a4d8b6d7703a05aaf3271f8c739f5
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67891125"
---
# <a name="reformatting-code-in-a-legacy-language-service"></a>在旧版语言服务中重新格式化代码

在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]源代码可以重新设置格式的规范化使用缩进和空格。 这可能包括插入或删除空间或在每个行开头的选项卡、 添加新行之间的行，或用制表符或空格与制表符替换空格。

> [!NOTE]
> 插入或删除换行字符可能会影响标记，如断点和书签，但添加或删除空格或选项卡不会影响标记。

用户可以通过选择启动重新格式化操作**选定内容的格式**或**格式的文档**从**高级**菜单上的**编辑**菜单。 插入代码段或特定字符时，也会触发重新格式化操作。 例如，当在 C# 中键入右大括号，匹配的左大括号和右大括号之间的所有内容会自动缩进到适当的级别。

时[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]发送**选定内容的格式**或**文档的格式**命令到语言服务<xref:Microsoft.VisualStudio.Package.ViewFilter>类将调用<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>中的方法<xref:Microsoft.VisualStudio.Package.Source>类。 若要支持的格式设置，必须重写<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>方法并提供您自己的格式代码。

## <a name="enabling-support-for-reformatting"></a>有关重新格式化启用支持

若要支持格式设置`EnableFormatSelection`的参数<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>必须设置为`true`时注册你的 VSPackage。 这将设置<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableFormatSelection%2A>属性设置为`true`。 <xref:Microsoft.VisualStudio.Package.ViewFilter.CanReformat%2A>方法将返回此属性的值。 如果为 true，它将返回<xref:Microsoft.VisualStudio.Package.ViewFilter>类调用<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>。

## <a name="implementing-reformatting"></a>实现重新格式化

若要实现重新格式化，你必须从派生类<xref:Microsoft.VisualStudio.Package.Source>类并重写<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>方法。 <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>对象描述要设置格式的范围和<xref:Microsoft.VisualStudio.Package.EditArray>对象保存在跨度上所做的编辑。 请注意，此范围可以是整个文档。 但是，由于有可能是对范围进行多次更改，应该是可在单个操作中还原所有更改。 若要执行此操作，包装中的所有更改<xref:Microsoft.VisualStudio.Package.CompoundAction>对象 （请参阅本主题中的"使用 CompoundAction 类"部分）。

### <a name="example"></a>示例

下面的示例可确保单个空格之后没有在每个逗号在所选内容，除非逗号后跟一个选项卡，或位于行尾。 删除的行中的最后一个逗号后尾随空格。 请参阅本主题以查看如何从调用此方法中的"使用 CompoundAction 类"部分<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>方法。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{
    class MySource : Source
    {
        private void DoFormatting(EditArray mgr, TextSpan span)
        {
            // Make sure there is one space after every comma unless followed
            // by a tab or comma is at end of line.
            IVsTextLines pBuffer = GetTextLines();
            if (pBuffer != null)
            {
                int    startIndex = span.iStartIndex;
                int    endIndex   = 0;
                string line       = "";
                // Loop over all lines in span
                for (int i = span.iStartLine; i <= span.iEndLine; i++)
                {
                    if (i < span.iEndLine)
                    {
                        pBuffer.GetLengthOfLine(i, out endIndex);
                    }
                    else
                    {
                        endIndex = span.iEndIndex;
                    }
                    pBuffer.GetLineText(i, startIndex, i, endIndex, out line);

                    if (line.Length > 0)
                    {
                        int index = 0;
                        // Loop over all commas in line
                        while ((index = line.IndexOf(',', index)) != -1)
                        {
                            int spaceIndex = index + 1;
                            // Determine how many spaces after comma
                            while (spaceIndex < line.Length && line[spaceIndex] == ' ')
                            {
                                ++spaceIndex;
                            }

                            int      spaceCount      = spaceIndex - (index + 1);
                            string   replacementText = " ";
                            bool     fDoEdit         = true;
                            TextSpan editTextSpan    = new TextSpan();

                            editTextSpan.iStartLine  = i;
                            editTextSpan.iEndLine    = i;
                            editTextSpan.iStartIndex = index + 1;

                            if (spaceIndex == line.Length)
                            {
                                if (spaceCount > 0)
                                {
                                    // Delete spaces after a comma at end of line
                                    editTextSpan.iEndIndex = spaceIndex;
                                    replacementText = "";
                                }
                                else
                                {
                                    // Otherwise, do not add spaces if comma is
                                    // at end of line.
                                    fDoEdit = false;
                                }
                            }
                            else if (spaceCount == 0)
                            {
                                if (spaceIndex < line.Length && line[spaceIndex] == '\t')
                                {
                                    // Do not insert space if a tab follows
                                    // a comma.
                                    fDoEdit = false;
                                }
                                else
                                {
                                    // No space after comma so add a space.
                                    editTextSpan.iEndIndex = index + 1;
                                }
                            }
                            else if (spaceCount > 1)
                            {
                                // More than one space after comma, replace
                                // with a single space.
                                editTextSpan.iEndIndex = spaceIndex;
                            }
                            else
                            {
                                // Single space after a comma and not at end
                                // of the line, leave it alone.
                                fDoEdit = false;
                            }
                            if (fDoEdit)
                            {
                                // Add edit operation
                                mgr.Add(new EditSpan(editTextSpan, replacementText));
                            }
                            index = spaceIndex;
                        }
                    }
                    startIndex = 0; // All subsequent lines start at 0
                }
                // Apply all edits
                mgr.ApplyEdits();
            }
        }
    }
}
```

## <a name="using-the-compoundaction-class"></a>使用 CompoundAction 类

所有重新格式化完成上一段代码应该是可在单个操作中还原。 这可以使用<xref:Microsoft.VisualStudio.Package.CompoundAction>类。 此类包装到单个编辑操作上的文本缓冲区的编辑操作的一组。

### <a name="example"></a>示例

下面是举例说明如何使用<xref:Microsoft.VisualStudio.Package.CompoundAction>类。 请参阅本主题的示例中的"实现支持的格式设置"部分中的示例`DoFormatting`方法。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{
    class MySource : Source
    {
        public override void ReformatSpan(EditArray mgr, TextSpan span)
        {
            string description = "Reformat code";
            CompoundAction ca = new CompoundAction(this, description);
            using (ca)
            {
                ca.FlushEditActions();      // Flush any pending edits
                DoFormatting(mgr, span);    // Format the span
            }
        }
    }
}
```

## <a name="see-also"></a>请参阅

- [旧版语言服务功能](legacy-language-service-features1.md)