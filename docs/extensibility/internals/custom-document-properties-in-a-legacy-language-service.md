---
title: 在旧版语言服务中的自定义文档属性 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom document properties, language services [managed package framework]
- document properties, custom
- language services [managed package framework], custom document properties
ms.assetid: cc714a67-b33e-4440-9203-3c90f648bd9c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8422e35e5241cf1cef30d0ba4a1fe7815323d091
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312894"
---
# <a name="custom-document-properties-in-a-legacy-language-service"></a>在旧版语言服务中自定义文档属性
文档属性可以显示在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**属性**窗口。 编程语言通常没有与单个源代码文件相关联的属性。 但是，XML 支持会影响编码、 架构和样式表的文档属性。

## <a name="discussion"></a>讨论
 如果你的语言需要自定义文档属性，您必须从派生类<xref:Microsoft.VisualStudio.Package.DocumentProperties>类，并在派生类上实现必要的属性。

 此外，文档属性通常存储在源代码文件本身。 这需要分析从源文件中显示的属性信息的语言服务**属性**窗口以及当更改时，文档属性中更新的源文件**属性**窗口。

## <a name="customize-the-documentproperties-class"></a>自定义 DocumentProperties 类
 若要支持自定义文档属性，您必须从派生类<xref:Microsoft.VisualStudio.Package.DocumentProperties>类，并添加所需的所有属性。 此外应提供组织他们中的用户属性**属性**窗口中显示。 如果属性只能具有`get`访问器，它显示为只读的中**属性**窗口。 如果属性同时具有`get`并`set`访问器，该属性还可以更新在**属性**窗口。

### <a name="example"></a>示例
 下面是示例类派生自<xref:Microsoft.VisualStudio.Package.DocumentProperties>，显示两个属性`Filename`和`Description`。 更新某个属性是、 上的自定义方法<xref:Microsoft.VisualStudio.Package.LanguageService>类调用以写入到的源文件的属性。

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    class TestDocumentProperties : DocumentProperties
    {
        private string m_filename;
        private string m_description;

        public TestDocumentProperties(CodeWindowManager mgr)
            : base(mgr)
        {
        }

        // Helper function to initialize this property without
        // going through the FileName property (which does a lot
        // more than we need when the filename is set).
        public void SetFileName(string filename)
        {
            m_filename = filename;
        }

        // Helper function to initialize this property without
        // going through the Description property (which does a lot
        // more than we need when the description is set).
        public void SetDescription(string description)
        {
            m_description = description;
        }

        ////////////////////////////////////////////////////////////
        // The document properties

        [CategoryAttribute("General")]
        [DescriptionAttribute("Name of the file")]
        [DisplayNameAttribute("Filename")]
        public string FileName
        {
            get { return m_filename; }
            set
            {
               if (value != m_filename)
               {
                    m_filename = value;
                    SetPropertyValue("Filename", m_filename);
               }
            }
        }

        [CategoryAttribute("General")]
        [DescriptionAttribute("Description of the file")]
        [DisplayNameAttribute("Description")]
        public string Description
        {
            get { return m_description; }
            set
            {
                if (value != m_description)
                {
                    m_description = value;
                    SetPropertyValue("Description", m_description);
                }
            }
        }

        ///////////////////////////////////////////////////////////
        // Private methods.

        private void SetPropertyValue(string propertyName, string propertyValue)
        {
            Source src = this.GetSource();
            if (src != null)
            {
                TestLanguageService service = src.LanguageService as TestLanguageService;
                if (service != null)
                {
                    // Set the property in to the source file.
                    service.SetPropertyValue(src, propertyName, propertyValue);
                }
            }
        }
    }
}
```

## <a name="instantiate-the-custom-documentproperties-class"></a>实例化自定义的 DocumentProperties 类
 若要实例化您的自定义文档属性类，必须重写<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A>方法在你的版本中<xref:Microsoft.VisualStudio.Package.LanguageService>类以返回的单个实例在<xref:Microsoft.VisualStudio.Package.DocumentProperties>类。

### <a name="example"></a>示例

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    class TestLanguageService : LanguageService
    {
        private TestDocumentProperties m_documentProperties;

        public override DocumentProperties CreateDocumentProperties(CodeWindowManager mgr)
        {
            if (m_documentProperties == null)
            {
                m_documentProperties = new TestDocumentProperties(mgr);
            }
            return m_documentProperties;
        }
    }
}
```

## <a name="properties-in-the-source-file"></a>源代码文件中的属性
 由于文档属性通常特定于源代码文件，值存储在源代码文件本身中。 这需要支持的语言分析器或扫描程序来定义这些属性。 例如，XML 文档的属性存储在根节点上。 根节点上的值被修改时**属性**窗口值发生更改，并在编辑器中更新的根节点。

### <a name="example"></a>示例
 此示例中存储的属性`Filename`和`Description`中的源文件的前两行，特殊注释标头中作为嵌入：

```
//!Filename = file.testext
//!Description = A sample file
```

 此示例演示从获取和设置文档属性的源文件的前两行如何如果用户直接修改源文件的属性将更新所需的两种方法。 `SetPropertyValue`方法显示以下是相同的示例中其中一个名为从`TestDocumentProperties`类，如中所示*自定义 DocumentProperties 类*部分。

 此示例使用扫描程序以确定前两行中的令牌的类型。 此示例是仅供说明用途。 这种情况的更典型方法是分析源文件为所谓的分析树，树的每个节点包含特定标记有关的信息。 根节点将包含文档属性。

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    // TokenType.Comment is the last item in that enumeration.
    public enum TestTokenTypes
    {
        DocPropertyLine = TokenType.Comment + 1,
        DocPropertyName,
        DocPropertyAssign,
        DocPropertyValue
    }

    class TestLanguageService : LanguageService
    {
        // Search this many lines from the beginning for properties.
        private static int maxLinesToSearch = 2;

        private TestDocumentProperties m_documentProperties;

        // Called whenever a full parsing operation has completed.
        public override void OnParseComplete(ParseRequest req)
        {
            if (m_documentProperties != null)
            {
                Source src = GetSource(req.View);
                if (src != null)
                {
                    string value = GetPropertyValue(src, "Filename");
                    m_documentProperties.SetFileName(value);

                    value = GetPropertyValue(src, "Description");
                    m_documentProperties.SetDescription(value);

                    // Update the Properties Window.
                    m_documentProperties.Refresh();
                }
            }
        }

        // Retrieves the specified property value from the given source.
        public string GetPropertyValue(Source src, string propertyName)
        {
            string propertyValue = "";

            if (src != null)
            {
                IVsTextColorState colorState = src.ColorState;
                if (colorState != null)
                {
                    string      line;
                    TokenInfo[] lineInfo = null;
                    int         i;

                    for (i = 0; i < maxLinesToSearch; i++)
                    {
                        line     = src.GetLine(i);
                        lineInfo = src.GetColorizer().GetLineInfo(
                                                        src.GetTextLines(),
                                                        i,
                                                        colorState);
                        if (lineInfo == null)
                        {
                            continue;
                        }
                        if (lineInfo[0].Type != (TokenType)TestTokenTypes.DocPropertyLine)
                        {
                            // Not a property line.
                            continue;
                        }
                        TokenInfo valueInfo = new TokenInfo();
                        int tokenIndex = -1;
                        for (tokenIndex = 0;
                             tokenIndex < lineInfo.Length;
                             tokenIndex++)
                        {
                            if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyName)
                            {
                                break;
                            }
                        }
                        if (tokenIndex >= lineInfo.Length)
                        {
                            // No property name on the line.
                            continue;
                        }
                        string name = src.GetText(i,
                                                  lineInfo[tokenIndex].StartIndex,
                                                  i,
                                                  lineInfo[tokenIndex].EndIndex + 1);
                        if (name != null)
                        {
                            if (String.Compare(name, propertyName, true) == 0)
                            {
                                for ( ;
                                     tokenIndex < lineInfo.Length;
                                     tokenIndex++)
                                {
                                    if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyValue)
                                    {
                                        break;
                                    }
                                }
                                if (tokenIndex < lineInfo.Length)
                                {
                                    propertyValue = src.GetText(i,
                                                          lineInfo[tokenIndex].StartIndex,
                                                          i,
                                                          lineInfo[tokenIndex].EndIndex + 1);
                                }
                                break;
                            }
                        }
                    }
                }
            }
            return propertyValue;
        }

        // Sets the specified property into the given source file.
        // Called from the TestDocumentProperties class.
        public void SetPropertyValue(Source src, string propertyName, string propertyValue)
        {
            string newLine;

            if (propertyName == null || propertyName == "")
            {
                // No property name, so nothing to do
                return;
            }
            if (propertyValue == null)
            {
                propertyValue = "";
            }
            // This is the line to be inserted.
            newLine = String.Format("//!{0} = {1}", propertyName, propertyValue);

            // First, find the line on which the property belongs.
            // If line is found, replace it.
            // Otherwise, insert the line at the beginning of the file.
            if (src != null)
            {
                IVsTextColorState colorState = src.ColorState;
                if (colorState != null)
                {
                    int         lineNumber = -1;
                    string      line;
                    TokenInfo[] lineInfo   = null;
                    int         i;

                    for (i = 0; i < maxLinesToSearch; i++)
                    {
                        line     = src.GetLine(i);
                        lineInfo = src.GetColorizer().GetLineInfo(
                                                        src.GetTextLines(),
                                                        i,
                                                        colorState);
                        if (lineInfo == null)
                        {
                            continue;
                        }
                        if (lineInfo[0].Type != (TokenType)TestTokenTypes.DocPropertyLine)
                        {
                            // Not a property line
                            continue;
                        }
                        TokenInfo valueInfo = new TokenInfo();
                        int tokenIndex = -1;
                        for (tokenIndex = 0;
                             tokenIndex < lineInfo.Length;
                             tokenIndex++)
                        {
                            if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyName)
                            {
                                break;
                            }
                        }
                        if (tokenIndex >= lineInfo.Length)
                        {
                            // No property name on the line.
                            continue;
                        }
                        string name = src.GetText(i,
                                                  lineInfo[tokenIndex].StartIndex,
                                                  i,
                                                  lineInfo[tokenIndex].EndIndex + 1);
                        if (name != null)
                        {
                            if (String.Compare(name, propertyName, true) == 0)
                            {
                                lineNumber = i;
                                break;
                            }
                        }
                    }

                    // Set up an undo context that also handles the insert/replace.
                    EditArray editArray = new EditArray(src,
                                                        true,
                                                        "Update Property");
                    if (editArray != null)
                    {
                        TextSpan span = new TextSpan();
                        if (lineNumber != -1)
                        {
                            // Replace line.
                            int lineLength = 0;
                            src.GetTextLines().GetLengthOfLine(lineNumber,
                                                               out lineLength);
                            span.iStartLine  = lineNumber;
                            span.iStartIndex = 0;
                            span.iEndLine    = lineNumber;
                            span.iEndIndex   = lineLength;
                        }
                        else
                        {
                            // Insert new line.
                            span.iStartLine  = 0;
                            span.iStartIndex = 0;
                            span.iEndLine    = 0;
                            span.iEndIndex   = 0;
                            newLine += "\n";
                        }
                        editArray.Add(new EditSpan(span, newLine));
                        editArray.ApplyEdits();
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)