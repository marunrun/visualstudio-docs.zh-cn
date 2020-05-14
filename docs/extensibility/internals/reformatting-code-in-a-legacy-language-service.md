---
title: 在旧语言服务中重新格式化代码 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- reformatting code, supporting in language services [managed package framework]
- language services [managed package framework], reformatting code
ms.assetid: 08bb3375-8fef-4f4e-9efa-0d7333bab0eb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dd3e83c7299298b16a6fb3178b189479a80e1728
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705909"
---
# <a name="reformatting-code-in-a-legacy-language-service"></a>在旧版语言服务中重新格式化代码

在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]源代码中可以通过规范化缩进和空格的使用来调整。 这可能包括在每行的开头插入或删除空格或制表符，在行之间添加新行，或者用空格替换空格。

> [!NOTE]
> 插入或删除换行符可能会影响断点和书签等标记，但添加或删除空格或制表符不会影响标记。

用户可以通过从 **"编辑"** 菜单上**的"高级**"菜单中选择 **"格式选择**"或 **"格式文档**"来启动重新格式化操作。 插入代码段或特定字符时，也可以触发重新格式化操作。 例如，在 C# 中键入右大括号时，匹配的打开大括号和右大括号之间的所有内容将自动缩进到适当的级别。

将[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**格式选择**或**格式文档**命令发送到语言服务时，<xref:Microsoft.VisualStudio.Package.ViewFilter>类将调用类中<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A><xref:Microsoft.VisualStudio.Package.Source>的方法。 要支持格式设置，<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>必须重写该方法并提供您自己的格式代码。

## <a name="enabling-support-for-reformatting"></a>启用对重新格式化的支持

要支持格式设置，`EnableFormatSelection`<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>必须在注册 VSPackage 时`true`将 参数设置为 。 这将属性<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableFormatSelection%2A>设置到`true`。 该方法<xref:Microsoft.VisualStudio.Package.ViewFilter.CanReformat%2A>返回此属性的值。 如果返回 true，<xref:Microsoft.VisualStudio.Package.ViewFilter>则类将调用<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>。

## <a name="implementing-reformatting"></a>实现重新格式化

要实现重新格式化，必须从<xref:Microsoft.VisualStudio.Package.Source>类派生一个类并重写<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>方法。 对象<xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>描述要格式化的范围，<xref:Microsoft.VisualStudio.Package.EditArray>并且对象保留在范围上所做的编辑。 请注意，此范围可以是整个文档。 但是，由于对范围可能进行了多次更改，因此所有更改都应在单个操作中可逆。 为此，在<xref:Microsoft.VisualStudio.Package.CompoundAction>对象中包装所有更改（请参阅本主题中的"使用复合操作类"部分）。

### <a name="example"></a>示例

以下示例确保所选内容中的每个逗号之后都有一个空格，除非逗号后跟一个选项卡或位于行尾。 删除行中最后一个逗号之后的尾随空格。 请参阅本主题中的"使用复合操作类"部分，了解如何从<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>方法调用此方法。

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

## <a name="using-the-compoundaction-class"></a>使用复合操作类

在代码部分上完成的所有重新格式化都应在单个操作中可逆。 这可以使用类<xref:Microsoft.VisualStudio.Package.CompoundAction>来完成。 此类将文本缓冲区上的一组编辑操作包装为单个编辑操作。

### <a name="example"></a>示例

下面是如何使用<xref:Microsoft.VisualStudio.Package.CompoundAction>类的示例。 有关`DoFormatting`该方法的示例，请参阅本主题中的"实现格式化支持"部分中的示例。

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
