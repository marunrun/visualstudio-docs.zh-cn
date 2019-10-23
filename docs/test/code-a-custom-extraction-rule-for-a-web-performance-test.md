---
title: 为 Web 性能测试编码自定义提取规则
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- extraction rules
- Web performance tests, creating custom extraction rules
- extraction rules, creating custom
ms.assetid: 6bcc5712-6cc6-4f59-8933-6e8078318c45
dev_langs:
- CSharp
- VB
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9aeb80d348e31de0934d515754c59346fac3c2ea
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665265"
---
# <a name="code-a-custom-extraction-rule-for-a-web-performance-test"></a>为 Web 性能测试编码自定义提取规则

可以创建自己的提取规则。 若要执行此操作，需从提取规则类派生出自己的规则。 从 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule> 基类派生提取规则。

> [!NOTE]
> 还可以创建自定义验证规则。 有关详细信息，请参阅[为负载测试创建自定义代码和插件](../test/create-custom-code-and-plug-ins-for-load-tests.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-create-a-custom-extraction-rule"></a>创建自定义提取规则

1. 打开一个包含 Web 性能测试的测试项目。

2. （可选）创建一个单独的类库项目来存储您的提取规则。

    > [!IMPORTANT]
    > 你可以在测试所在的项目中创建类。 但是，如果你希望重用规则，则最好创建一个单独的类库项目来存储规则。 如果创建单独的项目，则必须完成本过程中的可选步骤。

3. （可选）在该类库项目中，添加一个对 Microsoft.VisualStudio.QualityTools.WebTestFramework dll 的引用。

4. 创建一个从 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule> 类派生的类。 实现 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract*> 和 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.RuleName*> 成员。

5. （可选）生成新的类库项目。

6. （可选）在测试项目中添加一个对包含自定义提取规则的类库项目的引用。

7. 在测试项目中的“Web 性能测试编辑器”中打开一个 Web 性能测试  。

8. 若要添加自定义提取规则，请右键单击某个 Web 性能测试请求并选择“添加提取规则”。 

     出现“添加提取规则”对话框。  将在“选择规则”列表中看到自定义验证规则以及预定义的验证规则。  选择自定义提取规则，然后选择“确定”。 

9. 运行该 Web 性能测试。

## <a name="example"></a>示例

下面的代码演示如何实现自定义提取规则。 该提取规则从指定的输入字段中提取值。 基于该示例来创建您自己的自定义提取规则。

```csharp
using System;
using System.Collections.Generic;
using Microsoft.VisualStudio.TestTools.WebTesting;
using System.Globalization;

namespace ClassLibrary2
{
    //-------------------------------------------------------------------------
    // This class creates a custom extraction rule named "Custom Extract Input"
    // The user of the rule specifies the name of an input field, and the
    // rule attempts to extract the value of that input field.
    //-------------------------------------------------------------------------
    public class CustomExtractInput : ExtractionRule
    {
        /// Specify a name for use in the user interface.
        /// The user sees this name in the Add Extraction dialog box.
        //---------------------------------------------------------------------
        public override string RuleName
        {
            get { return "Custom Extract Input"; }
        }

        /// Specify a description for use in the user interface.
        /// The user sees this description in the Add Extraction dialog box.
        //---------------------------------------------------------------------
        public override string RuleDescription
        {
            get { return "Extracts the value from a specified input field"; }
        }

        // The name of the desired input field
        private string NameValue;
        public string Name
        {
            get { return NameValue; }
            set { NameValue = value; }
        }

        // The Extract method.  The parameter e contains the web performance test context.
        //---------------------------------------------------------------------
        public override void Extract(object sender, ExtractionEventArgs e)
        {
            if (e.Response.HtmlDocument != null)
            {
                foreach (HtmlTag tag in e.Response.HtmlDocument.GetFilteredHtmlTags(new string[] { "input" }))
                {
                    if (String.Equals(tag.GetAttributeValueAsString("name"), Name, StringComparison.InvariantCultureIgnoreCase))
                    {
                        string formFieldValue = tag.GetAttributeValueAsString("value");
                        if (formFieldValue == null)
                        {
                            formFieldValue = String.Empty;
                        }

                        // add the extracted value to the web performance test context
                        e.WebTest.Context.Add(this.ContextParameterName, formFieldValue);
                        e.Success = true;
                        return;
                    }
                }
            }
            // If the extraction fails, set the error text that the user sees
            e.Success = false;
            e.Message = String.Format(CultureInfo.CurrentCulture, "Not Found: {0}", Name);
        }
    }
}
```

```vb
Imports System
Imports System.Collections.Generic
Imports Microsoft.VisualStudio.TestTools.WebTesting
Imports System.Globalization

Namespace ClassLibrary2

    '-------------------------------------------------------------------------
    ' This class creates a custom extraction rule named "Custom Extract Input"
    ' The user of the rule specifies the name of an input field, and the
    ' rule attempts to extract the value of that input field.
    '-------------------------------------------------------------------------
    Public Class CustomExtractInput
        Inherits ExtractionRule

        ' Specify a name for use in the user interface.
        ' The user sees this name in the Add Extraction dialog box.
        '---------------------------------------------------------------------
        Public Overrides ReadOnly Property RuleName() As String
            Get
                Return "Custom Extract Input"
            End Get
        End Property

        ' Specify a description for use in the user interface.
        ' The user sees this description in the Add Extraction dialog box.
        '---------------------------------------------------------------------
        Public Overrides ReadOnly Property RuleDescription() As String
            Get
                Return "Extracts the value from a specified input field"
            End Get
        End Property

        ' The name of the desired input field
        Private NameValue As String
        Public Property Name() As String
            Get
                Return NameValue
            End Get
            Set(ByVal value As String)
                NameValue = value
            End Set
        End Property

        ' The Extract method.  The parameter e contains the web performance test context.
        '---------------------------------------------------------------------
        Public Overrides Sub Extract(ByVal sender As Object, ByVal e As ExtractionEventArgs)

            If Not e.Response.HtmlDocument Is Nothing Then

                For Each tag As HtmlTag In e.Response.HtmlDocument.GetFilteredHtmlTags(New String() {"input"})

                    If String.Equals(tag.GetAttributeValueAsString("name"), Name, StringComparison.InvariantCultureIgnoreCase) Then

                        Dim formFieldValue As String = tag.GetAttributeValueAsString("value")
                        If formFieldValue Is Nothing Then

                            formFieldValue = String.Empty
                        End If

                        ' add the extracted value to the web performance test context
                        e.WebTest.Context.Add(Me.ContextParameterName, formFieldValue)
                        e.Success = True
                        Return
                    End If
                Next
            End If
            ' If the extraction fails, set the error text that the user sees
            e.Success = False
            e.Message = String.Format(CultureInfo.CurrentCulture, "Not Found: {0}", Name)
        End Sub
    End Class
End Namespace
```

<xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract*> 方法中包含了提取规则的核心功能。 前面示例中的 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract*> 方法接受 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionEventArgs> 参数，该参数用于提供此提取规则涵盖范围内的请求生成的响应。 该响应包含一个 <xref:Microsoft.VisualStudio.TestTools.WebTesting.HtmlDocument>，其中包含了响应中的所有标记。 输入标记会从 <xref:Microsoft.VisualStudio.TestTools.WebTesting.HtmlDocument> 筛选排除掉。 会对每个输入标记的 `name` 特性进行检查，以确定其值是否与用户所提供的 `Name` 属性的值相等。 如果找到具有此匹配特性的标记，便会尝试提取 `value` 特性所包含的值（如果存在 value 特性的话）。 如果该值存在，则会提取标记的名称和值，并将它们添加到 Web 性能测试上下文中。 提取规则通过。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractAttributeValue>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractFormField>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractHttpHeader>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractRegularExpression>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractText>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractHiddenFields>
- [为 Web 性能测试编码自定义验证规则](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)