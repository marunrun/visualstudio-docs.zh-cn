---
title: 演练：创建自定义指令处理器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
- walkthroughs [text templates], directive processor
ms.assetid: b8f35a36-14e1-4467-8f5f-e01402af14d5
caps.latest.revision: 76
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 208089e4a9caeea5f8b56cdf694b7aaa602228ec
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659324"
---
# <a name="walkthrough-creating-a-custom-directive-processor"></a>演练：创建自定义指令处理器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指令处理器 * 通过将代码添加到*生成的转换类*来工作。 如果从*文本模板*调用*指令*，则在文本模板中编写的其余代码都可以依赖于指令提供的功能。

 您可以编写自己的自定义指令处理器。 利用它可以自定义文本模板。 若要创建自定义指令处理器，需要创建一个从 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 或 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 继承的类。

 本演练演示以下任务：

- 创建自定义指令处理器

- 注册指令处理器

- 测试指令处理器

## <a name="prerequisites"></a>Prerequisites
 若要完成此演练，您需要：

- Visual Studio 2010

- Visual Studio 2010 SDK

## <a name="creating-a-custom-directive-processor"></a>创建自定义指令处理器
 在本演练中，将创建一个自定义指令处理器。 添加一条自定义指令，该指令读取 XML 文件，将其存储在 <xref:System.Xml.XmlDocument> 变量中，并通过一个属性将其公开。 在“测试指令处理器”一节中，将在文本模板中使用此属性访问 XML 文件。

 自定义指令的调用如下所示：

 `<#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<Your Path>DocFile.xml" #>`

 自定义指令处理器将变量和属性添加到生成转换类。 您编写的指令使用 <xref:System.CodeDom> 类创建引擎添加到生成转换类的代码。 <xref:System.CodeDom> 类使用 Visual C# 或 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 创建代码，具体取决于在 `language` 指令的 `template` 参数中指定的语言。 指令处理器的语言和访问指令处理器的文本模板的语言不必一致。

 指令创建的代码如下所示：

```csharp
private System.Xml.XmlDocument document0Value;

public virtual System.Xml.XmlDocument Document0
{
  get
  {
    if ((this.document0Value == null))
    {
      this.document0Value = XmlReaderHelper.ReadXml(<FileNameParameterValue>);
    }
    return this.document0Value;
  }
}
```

```vb
Private document0Value As System.Xml.XmlDocument

Public Overridable ReadOnly Property Document0() As System.Xml.XmlDocument
    Get
        If (Me.document0Value Is Nothing) Then
            Me.document0Value = XmlReaderHelper.ReadXml(<FileNameParameterValue>)
        End If
        Return Me.document0Value
    End Get
End Property
```

#### <a name="to-create-a-custom-directive-processor"></a>创建自定义指令处理器

1. 在 Visual Studio 中，创建一个名为 CustomDP 的 C# 或 Visual Basic 类库项目。

    > [!NOTE]
    > 如果要在多台计算机上安装指令处理器，最好使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Extension (VSIX) 项目并在扩展中包含一个 .pkgdef 文件。 有关详细信息，请参阅[部署自定义指令处理器](../modeling/deploying-a-custom-directive-processor.md)。

2. 添加对下列程序集的引用：

    - **VisualStudio. TextTemplating. \***

    - **VisualStudio. TextTemplating. \***

3. 将**Class1**中的代码替换为以下代码。 此代码定义一个继承自 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 类的 CustomDirectiveProcessor 类并实现必需的方法。

    ```csharp
    using System;
    using System.CodeDom;
    using System.CodeDom.Compiler;
    using System.Collections.Generic;
    using System.Globalization;
    using System.IO;
    using System.Text;
    using System.Xml;
    using System.Xml.Serialization;
    using Microsoft.VisualStudio.TextTemplating;

    namespace CustomDP
    {
        public class CustomDirectiveProcessor : DirectiveProcessor
        {
            //this buffer stores the code that is added to the
            //generated transformation class after all the processing is done
            //---------------------------------------------------------------------
            private StringBuilder codeBuffer;

            //Using a Code Dom Provider creates code for the
            //generated transformation class in either Visual Basic or C#.
            //If you want your directive processor to support only one language, you
            //can hard code the code you add to the generated transformation class.
            //In that case, you do not need this field.
            //--------------------------------------------------------------------------
            private CodeDomProvider codeDomProvider;

            //this stores the full contents of the text template that is being processed
            //--------------------------------------------------------------------------
            private String templateContents;

            //These are the errors that occur during processing. The engine passes
            //the errors to the host, and the host can decide how to display them,
            //for example the host can display the errors in the UI
            //or write them to a file.
            //---------------------------------------------------------------------
            private CompilerErrorCollection errorsValue;
            public new CompilerErrorCollection Errors
            {
                get { return errorsValue; }
            }

            //Each time this directive processor is called, it creates a new property.
            //We count how many times we are called, and append "n" to each new
            //property name. The property names are therefore unique.
            //-----------------------------------------------------------------------------
            private int directiveCount = 0;

            public override void Initialize(ITextTemplatingEngineHost host)
            {
                //we do not need to do any initialization work
            }

            public override void StartProcessingRun(CodeDomProvider languageProvider, String templateContents, CompilerErrorCollection errors)
            {
                //the engine has passed us the language of the text template
                //we will use that language to generate code later
                //----------------------------------------------------------
                this.codeDomProvider = languageProvider;
                this.templateContents = templateContents;
                this.errorsValue = errors;

                this.codeBuffer = new StringBuilder();
            }

            //Before calling the ProcessDirective method for a directive, the
            //engine calls this function to see whether the directive is supported.
            //Notice that one directive processor might support many directives.
            //---------------------------------------------------------------------
            public override bool IsDirectiveSupported(string directiveName)
            {
                if (string.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) == 0)
                {
                    return true;
                }
                if (string.Compare(directiveName, "SuperCoolDirective", StringComparison.OrdinalIgnoreCase) == 0)
                {
                    return true;
                }
                return false;
            }

            public override void ProcessDirective(string directiveName, IDictionary<string, string> arguments)
            {
                if (string.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) == 0)
                {
                    string fileName;

                    if (!arguments.TryGetValue("FileName", out fileName))
                    {
                        throw new DirectiveProcessorException("Required argument 'FileName' not specified.");
                    }

                    if (string.IsNullOrEmpty(fileName))
                    {
                        throw new DirectiveProcessorException("Argument 'FileName' is null or empty.");
                    }

                    //Now we add code to the generated transformation class.
                    //This directive supports either Visual Basic or C#, so we must use the
                    //System.CodeDom to create the code.
                    //If a directive supports only one language, you can hard code the code.
                    //--------------------------------------------------------------------------

                    CodeMemberField documentField = new CodeMemberField();

                    documentField.Name = "document" + directiveCount + "Value";
                    documentField.Type = new CodeTypeReference(typeof(XmlDocument));
                    documentField.Attributes = MemberAttributes.Private;

                    CodeMemberProperty documentProperty = new CodeMemberProperty();

                    documentProperty.Name = "Document" + directiveCount;
                    documentProperty.Type = new CodeTypeReference(typeof(XmlDocument));
                    documentProperty.Attributes = MemberAttributes.Public;
                    documentProperty.HasSet = false;
                    documentProperty.HasGet = true;

                    CodeExpression fieldName = new CodeFieldReferenceExpression(new CodeThisReferenceExpression(), documentField.Name);
                    CodeExpression booleanTest = new CodeBinaryOperatorExpression(fieldName, CodeBinaryOperatorType.IdentityEquality, new CodePrimitiveExpression(null));
                    CodeExpression rightSide = new CodeMethodInvokeExpression(new CodeTypeReferenceExpression("XmlReaderHelper"), "ReadXml", new CodePrimitiveExpression(fileName));
                    CodeStatement[] thenSteps = new CodeStatement[] { new CodeAssignStatement(fieldName, rightSide) };

                    CodeConditionStatement ifThen = new CodeConditionStatement(booleanTest, thenSteps);
                    documentProperty.GetStatements.Add(ifThen);

                    CodeStatement s = new CodeMethodReturnStatement(fieldName);
                    documentProperty.GetStatements.Add(s);

                    CodeGeneratorOptions options = new CodeGeneratorOptions();
                    options.BlankLinesBetweenMembers = true;
                    options.IndentString = "    ";
                    options.VerbatimOrder = true;
                    options.BracingStyle = "C";

                    using (StringWriter writer = new StringWriter(codeBuffer, CultureInfo.InvariantCulture))
                    {
                        codeDomProvider.GenerateCodeFromMember(documentField, writer, options);
                        codeDomProvider.GenerateCodeFromMember(documentProperty, writer, options);
                    }

                }//end CoolDirective

                //One directive processor can contain many directives.
                //If you want to support more directives, the code goes here...
                //-----------------------------------------------------------------
                if (string.Compare(directiveName, "supercooldirective", StringComparison.OrdinalIgnoreCase) == 0)
                {
                    //code for SuperCoolDirective goes here...
                }//end SuperCoolDirective

                //Track how many times the processor has been called.
                //-----------------------------------------------------------------
                directiveCount++;

            }//end ProcessDirective

            public override void FinishProcessingRun()
            {
                this.codeDomProvider = null;

                //important: do not do this:
                //the get methods below are called after this method
                //and the get methods can access this field
                //-----------------------------------------------------------------
                //this.codeBuffer = null;
            }

            public override string GetPreInitializationCodeForProcessingRun()
            {
                //Use this method to add code to the start of the
                //Initialize() method of the generated transformation class.
                //We do not need any pre-initialization, so we will just return "".
                //-----------------------------------------------------------------
                //GetPreInitializationCodeForProcessingRun runs before the
                //Initialize() method of the base class.
                //-----------------------------------------------------------------
                return String.Empty;
            }

            public override string GetPostInitializationCodeForProcessingRun()
            {
                //Use this method to add code to the end of the
                //Initialize() method of the generated transformation class.
                //We do not need any post-initialization, so we will just return "".
                //------------------------------------------------------------------
                //GetPostInitializationCodeForProcessingRun runs after the
                //Initialize() method of the base class.
                //-----------------------------------------------------------------
                return String.Empty;
            }

            public override string GetClassCodeForProcessingRun()
            {
                //Return the code to add to the generated transformation class.
                //-----------------------------------------------------------------
                return codeBuffer.ToString();
            }

            public override string[] GetReferencesForProcessingRun()
            {
                //This returns the references that we want to use when
                //compiling the generated transformation class.
                //-----------------------------------------------------------------
                //We need a reference to this assembly to be able to call
                //XmlReaderHelper.ReadXml from the generated transformation class.
                //-----------------------------------------------------------------
                return new string[]
                {
                    "System.Xml",
                    this.GetType().Assembly.Location
                };
            }

            public override string[] GetImportsForProcessingRun()
            {
                //This returns the imports or using statements that we want to
                //add to the generated transformation class.
                //-----------------------------------------------------------------
                //We need CustomDP to be able to call XmlReaderHelper.ReadXml
                //from the generated transformation class.
                //-----------------------------------------------------------------
                return new string[]
                {
                    "System.Xml",
                    "CustomDP"
                };
            }
        }//end class CustomDirectiveProcessor

        //-------------------------------------------------------------------------
        // the code that we are adding to the generated transformation class
        // will call this method
        //-------------------------------------------------------------------------
        public static class XmlReaderHelper
        {
            public static XmlDocument ReadXml(string fileName)
            {
                XmlDocument d = new XmlDocument();

                using (XmlTextReader reader = new XmlTextReader(fileName))
                {
                    try
                    {
                        d.Load(reader);
                    }
                    catch (System.Xml.XmlException e)
                    {
                        throw new DirectiveProcessorException("Unable to read the XML file.", e);
                    }
                }
                return d;
            }
        }//end class XmlReaderHelper
    }//end namespace CustomDP
    ```

    ```vb
    Imports System
    Imports System.CodeDom
    Imports System.CodeDom.Compiler
    Imports System.Collections.Generic
    Imports System.Globalization
    Imports System.IO
    Imports System.Text
    Imports System.Xml
    Imports System.Xml.Serialization
    Imports Microsoft.VisualStudio.TextTemplating

    Namespace CustomDP

        Public Class CustomDirectiveProcessor
        Inherits DirectiveProcessor

            'this buffer stores the code that is added to the
            'generated transformation class after all the processing is done
            '---------------------------------------------------------------
            Private codeBuffer As StringBuilder

            'Using a Code Dom Provider creates code for the
            'generated transformation class in either Visual Basic or C#.
            'If you want your directive processor to support only one language, you
            'can hard code the code you add to the generated transformation class.
            'In that case, you do not need this field.
            '--------------------------------------------------------------------------
            Private codeDomProvider As CodeDomProvider

            'this stores the full contents of the text template that is being processed
            '--------------------------------------------------------------------------
            Private templateContents As String

            'These are the errors that occur during processing. The engine passes
            'the errors to the host, and the host can decide how to display them,
            'for example the host can display the errors in the UI
            'or write them to a file.
            '---------------------------------------------------------------------
            Private errorsValue As CompilerErrorCollection
            Public Shadows ReadOnly Property Errors() As CompilerErrorCollection
                Get
                    Return errorsValue
                End Get
            End Property

            'Each time this directive processor is called, it creates a new property.
            'We count how many times we are called, and append "n" to each new
            'property name. The property names are therefore unique.
            '--------------------------------------------------------------------------
            Private directiveCount As Integer = 0

            Public Overrides Sub Initialize(ByVal host As ITextTemplatingEngineHost)

                'we do not need to do any initialization work
            End Sub

            Public Overrides Sub StartProcessingRun(ByVal languageProvider As CodeDomProvider, ByVal templateContents As String, ByVal errors As CompilerErrorCollection)

                'the engine has passed us the language of the text template
                'we will use that language to generate code later
                '----------------------------------------------------------
                Me.codeDomProvider = languageProvider
                Me.templateContents = templateContents
                Me.errorsValue = errors

                Me.codeBuffer = New StringBuilder()
            End Sub

            'Before calling the ProcessDirective method for a directive, the
            'engine calls this function to see whether the directive is supported.
            'Notice that one directive processor might support many directives.
            '---------------------------------------------------------------------
            Public Overrides Function IsDirectiveSupported(ByVal directiveName As String) As Boolean

                If String.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then
                    Return True
                End If

                If String.Compare(directiveName, "SuperCoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then
                    Return True
                End If

                Return False
            End Function

            Public Overrides Sub ProcessDirective(ByVal directiveName As String, ByVal arguments As IDictionary(Of String, String))

                If String.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then

                    Dim fileName As String

                    If Not (arguments.TryGetValue("FileName", fileName)) Then
                        Throw New DirectiveProcessorException("Required argument 'FileName' not specified.")
                    End If

                    If String.IsNullOrEmpty(fileName) Then
                        Throw New DirectiveProcessorException("Argument 'FileName' is null or empty.")
                    End If

                    'Now we add code to the generated transformation class.
                    'This directive supports either Visual Basic or C#, so we must use the
                    'System.CodeDom to create the code.
                    'If a directive supports only one language, you can hard code the code.
                    '--------------------------------------------------------------------------

                    Dim documentField As CodeMemberField = New CodeMemberField()

                    documentField.Name = "document" & directiveCount & "Value"
                    documentField.Type = New CodeTypeReference(GetType(XmlDocument))
                    documentField.Attributes = MemberAttributes.Private

                    Dim documentProperty As CodeMemberProperty = New CodeMemberProperty()

                    documentProperty.Name = "Document" & directiveCount
                    documentProperty.Type = New CodeTypeReference(GetType(XmlDocument))
                    documentProperty.Attributes = MemberAttributes.Public
                    documentProperty.HasSet = False
                    documentProperty.HasGet = True

                    Dim fieldName As CodeExpression = New CodeFieldReferenceExpression(New CodeThisReferenceExpression(), documentField.Name)
                    Dim booleanTest As CodeExpression = New CodeBinaryOperatorExpression(fieldName, CodeBinaryOperatorType.IdentityEquality, New CodePrimitiveExpression(Nothing))
                    Dim rightSide As CodeExpression = New CodeMethodInvokeExpression(New CodeTypeReferenceExpression("XmlReaderHelper"), "ReadXml", New CodePrimitiveExpression(fileName))
                    Dim thenSteps As CodeStatement() = New CodeStatement() {New CodeAssignStatement(fieldName, rightSide)}

                    Dim ifThen As CodeConditionStatement = New CodeConditionStatement(booleanTest, thenSteps)
                    documentProperty.GetStatements.Add(ifThen)

                    Dim s As CodeStatement = New CodeMethodReturnStatement(fieldName)
                    documentProperty.GetStatements.Add(s)

                    Dim options As CodeGeneratorOptions = New CodeGeneratorOptions()
                    options.BlankLinesBetweenMembers = True
                    options.IndentString = "    "
                    options.VerbatimOrder = True
                    options.BracingStyle = "VB"

                    Using writer As StringWriter = New StringWriter(codeBuffer, CultureInfo.InvariantCulture)

                        codeDomProvider.GenerateCodeFromMember(documentField, writer, options)
                        codeDomProvider.GenerateCodeFromMember(documentProperty, writer, options)
                    End Using

                End If  'CoolDirective

                'One directive processor can contain many directives.
                'If you want to support more directives, the code goes here...
                '-----------------------------------------------------------------
                If String.Compare(directiveName, "supercooldirective", StringComparison.OrdinalIgnoreCase) = 0 Then

                    'code for SuperCoolDirective goes here
                End If 'SuperCoolDirective

                'Track how many times the processor has been called.
                '-----------------------------------------------------------------
                directiveCount += 1
            End Sub 'ProcessDirective

            Public Overrides Sub FinishProcessingRun()

                Me.codeDomProvider = Nothing

                'important: do not do this:
                'the get methods below are called after this method
                'and the get methods can access this field
                '-----------------------------------------------------------------
                'Me.codeBuffer = Nothing
            End Sub

            Public Overrides Function GetPreInitializationCodeForProcessingRun() As String

                'Use this method to add code to the start of the
                'Initialize() method of the generated transformation class.
                'We do not need any pre-initialization, so we will just return "".
                '-----------------------------------------------------------------
                'GetPreInitializationCodeForProcessingRun runs before the
                'Initialize() method of the base class.
                '-----------------------------------------------------------------
                Return String.Empty
            End Function

            Public Overrides Function GetPostInitializationCodeForProcessingRun() As String

                'Use this method to add code to the end of the
                'Initialize() method of the generated transformation class.
                'We do not need any post-initialization, so we will just return "".
                '------------------------------------------------------------------
                'GetPostInitializationCodeForProcessingRun runs after the
                'Initialize() method of the base class.
                '-----------------------------------------------------------------
                Return String.Empty
            End Function

            Public Overrides Function GetClassCodeForProcessingRun() As String

                'Return the code to add to the generated transformation class.
                '-----------------------------------------------------------------
                Return codeBuffer.ToString()
            End Function

            Public Overrides Function GetReferencesForProcessingRun() As String()

                'This returns the references that we want to use when
                'compiling the generated transformation class.
                '-----------------------------------------------------------------
                'We need a reference to this assembly to be able to call
                'XmlReaderHelper.ReadXml from the generated transformation class.
                '-----------------------------------------------------------------
                Return New String() {"System.Xml", Me.GetType().Assembly.Location}
            End Function

            Public Overrides Function GetImportsForProcessingRun() As String()

                'This returns the imports or using statements that we want to
                'add to the generated transformation class.
                '-----------------------------------------------------------------
                'We need CustomDP to be able to call XmlReaderHelper.ReadXml
                'from the generated transformation class.
                '-----------------------------------------------------------------
                Return New String() {"System.Xml", "CustomDP"}
            End Function
        End Class 'CustomDirectiveProcessor

        '--------------------------------------------------------------------------
        ' the code that we are adding to the generated transformation class
        ' will call this method
        '--------------------------------------------------------------------------
        Public Class XmlReaderHelper

            Public Shared Function ReadXml(ByVal fileName As String) As XmlDocument

                Dim d As XmlDocument = New XmlDocument()

                Using reader As XmlTextReader = New XmlTextReader(fileName)

                    Try
                        d.Load(reader)

                    Catch e As System.Xml.XmlException

                        Throw New DirectiveProcessorException("Unable to read the XML file.", e)
                    End Try
                End Using

                Return d
            End Function
        End Class 'XmlReaderHelper

    End Namespace
    ```

4. 对于 "仅 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]"，打开 "**项目**" 菜单，然后单击 " **CustomDP 属性**"。 在 "**应用程序**" 选项卡上的 "**根命名空间**" 中，删除默认值 `CustomDP`。

5. 在“文件”菜单上，单击“全部保存”。

6. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

### <a name="build-the-project"></a>生成项目
 生成项目。 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

## <a name="registering-the-directive-processor"></a>注册指令处理器
 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的文本模板调用指令之前，必须为指令处理器添加注册表项。

> [!NOTE]
> 如果要在多台计算机上安装指令处理器，最好定义一个 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Extension (VSIX)，其中包含一个 .pkgdef 文件和您的程序集。 有关详细信息，请参阅[部署自定义指令处理器](../modeling/deploying-a-custom-directive-processor.md)。

 指令处理器的项在注册表的以下位置：

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\*.0\TextTemplating\DirectiveProcessors
```

 对于 64 位系统，注册表位置为：

```
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VisualStudio\*.0\TextTemplating\DirectiveProcessors
```

 在本节中，将在注册表中的该位置为自定义指令处理器添加一个项。

> [!CAUTION]
> 注册表编辑不当可能会严重损坏系统。 更改注册表之前，应备份计算机中的所有重要数据。

#### <a name="to-add-a-registry-key-for-the-directive-processor"></a>为指令处理器添加注册表项

1. 使用 "开始" 菜单或命令行运行 `regedit` 命令。

2. 浏览到位置**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio \\ \* .0 \ TextTemplating\DirectiveProcessors**，并单击节点。

    在64位系统上，使用**HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VisualStudio \\ \*。 0 \ TextTemplating\DirectiveProcessors**

3. 添加名为 CustomDirectiveProcessor 的新项。

   > [!NOTE]
   > 这是将在自定义指令的 Processor 字段中使用的名称。 此名称不必与指令名称、指令处理器类名称或指令处理器命名空间一致。

4. 添加名为 Class 的新字符串值，该新字符串名称的值为 CustomDP.CustomDirectiveProcessor。

5. 添加名为 CodeBase 的新字符串值，它的值等于在本演练前面创建的 CustomDP.dll 的路径。

    例如，路径可能类似于 `C:\UserFiles\CustomDP\bin\Debug\CustomDP.dll`。

    注册表项应具有以下值：

   |   “属性”    |  键入  |                                   数据                                   |
   |-----------|--------|--------------------------------------------------------------------------|
   | (默认) | REG_SZ |                             (未设置值)                              |
   |   实例   | REG_SZ |                    CustomDP.CustomDirectiveProcessor                     |
   | CodeBase  | REG_SZ | <strong>\<Path 到解决方案 ></strong>CustomDP\bin\Debug\CustomDP.dll |

    如果已将程序集放置在 GAC 中，则值应如下所示：

   |   “属性”    |  键入  |               数据                |
   |-----------|--------|-----------------------------------|
   | (默认) | REG_SZ |          (未设置值)          |
   |   实例   | REG_SZ | CustomDP.CustomDirectiveProcessor |
   | Assembly  | REG_SZ |           CustomDP.dll            |

6. 重新启动 Visual Studio。

## <a name="testing-the-directive-processor"></a>测试指令处理器
 若要测试指令处理器，需要编写一个调用它的文本模板。

 在本示例中，文本模板调用指令并传入包含类文件文档的 XML 文件的名称。 有关详细信息，请参阅[XML 文档注释](https://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199)。

 然后，文本模板使用该指令创建的 <xref:System.Xml.XmlDocument> 属性导航到 XML 并输出文档注释。

#### <a name="to-create-an-xml-file-for-use-in-testing-the-directive-processor"></a>创建供测试指令处理器使用的 XML 文件

1. 使用任意文本编辑器（例如记事本）创建名为 `DocFile.xml` 的文本文件。

    > [!NOTE]
    > 可以在任意位置（如 C:\Test\DocFile.xml）创建此文件。

2. 向文本文件中添加以下内容：

    ```
    <?xml version="1.0"?>
    <doc>
        <assembly>
            <name>xmlsample</name>
        </assembly>
        <members>
            <member name="T:SomeClass">
                <summary>Class level summary documentation goes here.</summary>
                <remarks>Longer comments can be associated with a type or member through the remarks tag</remarks>
            </member>
            <member name="F:SomeClass.m_Name">
                <summary>Store for the name property</summary>
            </member>
            <member name="M:SomeClass.#ctor">
                <summary>The class constructor.</summary>
            </member>
            <member name="M:SomeClass.SomeMethod(System.String)">
                <summary>Description for SomeMethod.</summary>
                <param name="s">Parameter description for s goes here</param>
                <seealso cref="T:System.String">You can use the cref attribute on any tag to reference a type or member and the compiler will check that the reference exists.</seealso>
            </member>
            <member name="M:SomeClass.SomeOtherMethod">
                <summary>Some other method.</summary>
                <returns>Return results are described through the returns tag.</returns>
                <seealso cref="M:SomeClass.SomeMethod(System.String)">Notice the use of the cref attribute to reference a specific method</seealso>
            </member>
            <member name="M:SomeClass.Main(System.String[])">
                <summary>The entry point for the application.</summary>
                <param name="args">A list of command line arguments</param>
            </member>
            <member name="P:SomeClass.Name">
                <summary>Name property</summary>
                <value>A value tag is used to describe the property value</value>
            </member>
        </members>
    </doc>
    ```

3. 保存并关闭文件。

#### <a name="to-create-a-text-template-to-test-the-directive-processor"></a>创建文本模板测试指令处理器

1. 在 Visual Studio 中，创建一个名为 TemplateTest 的 C# 或 Visual Basic 类库项目。

2. 添加名为 TestDP.tt 的新文本模板文件。

3. 确保将 TestDP.tt 的 "**自定义工具**" 属性设置为 `TextTemplatingFileGenerator`。

4. 将 TestDP.tt 的内容更改为以下文本。

    > [!NOTE]
    > 请确保将字符串 < `YOUR PATH>` 替换为 Docfile.xml 文件的路径。

     文本模板的语言不必与指令处理器的语言一致。

    ```csharp
    <#@ assembly name="System.Xml" #>
    <#@ template debug="true" #>
    <#@ output extension=".txt" #>

    <#  //This will call the custom directive processor. #>
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>

    <#  //Uncomment this line if you want to see the generated transformation class. #>
    <#  //System.Diagnostics.Debugger.Break(); #>

    <#  //This will use the results of the directive processor. #>
    <#  //The directive processor has read the XML and stored it in Document0. #>
    <#
        XmlNode node = Document0.DocumentElement.SelectSingleNode("members");

        foreach (XmlNode member in node.ChildNodes)
        {
            XmlNode name = member.Attributes.GetNamedItem("name");
            WriteLine("{0,7}:  {1}", "Name", name.Value);

            foreach (XmlNode comment in member.ChildNodes)
            {
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText);
            }
            WriteLine("");
        }
    #>

    <#  //You can call the directive processor again and pass it a different file. #>
    <# //@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\<Your Second File>" #>

    <#  //To use the results of the second directive call, use Document1. #>
    <#
        //XmlNode node2 = Document1.DocumentElement.SelectSingleNode("members");

        //...
    #>
    ```

    ```vb
    <#@ assembly name="System.Xml" #>
    <#@ template debug="true" language="vb" #>
    <#@ output extension=".txt" #>

    <#  'This will call the custom directive processor. #>
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>

    <#  'Uncomment this line if you want to see the generated transformation class. #>
    <#  'System.Diagnostics.Debugger.Break() #>

    <#  'This will use the results of the directive processor. #>
    <#  'The directive processor has read the XML and stored it in Document0. #>
    <#
        Dim node as XmlNode = Document0.DocumentElement.SelectSingleNode("members")

        Dim member As XmlNode
        For Each member In node.ChildNodes

            Dim name As XmlNode = member.Attributes.GetNamedItem("name")
            WriteLine("{0,7}:  {1}", "Name", name.Value)

            Dim comment As XmlNode
            For Each comment In member.ChildNodes
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText)
            Next

            WriteLine("")
        Next
    #>

    <#  'You can call the directive processor again and pass it a different file. #>
    <# '@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFileTwo.xml" #>

    <#  'To use the results of the second directive call, use Document1. #>
    <#
        'node = Document1.DocumentElement.SelectSingleNode("members")

        '...
    #>
    ```

    > [!NOTE]
    > 在本示例中，`Processor` 参数的值为 `CustomDirectiveProcessor`。 `Processor` 参数的值必须与处理器的注册表项的名称一致。

5. 在“文件”菜单上，单击“全部保存”。

#### <a name="to-test-the-directive-processor"></a>测试指令处理器

1. 在**解决方案资源管理器**中，右键单击 TestDP.tt，然后单击 "**运行自定义工具**"。

     对于 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 用户，默认情况下，Testdp.txt 可能不会出现在**解决方案资源管理器**中。 若要显示分配给项目的所有文件，请打开 "**项目**" 菜单，然后单击 "**显示所有文件**"。

2. 在**解决方案资源管理器**中，展开 "testdp.txt" 节点，然后双击 "testdp.txt" 以在编辑器中将其打开。

     此时将显示生成的文本输出。 输出应如下所示：

    ```
       Name:  T:SomeClass
    summary:  Class level summary documentation goes here.
    remarks:  Longer comments can be associated with a type or member through the remarks tag

       Name:  F:SomeClass.m_Name
    summary:  Store for the name property

       Name:  M:SomeClass.#ctor
    summary:  The class constructor.

       Name:  M:SomeClass.SomeMethod(System.String)
    summary:  Description for SomeMethod.
      param:  Parameter description for s goes here
    seealso:  You can use the cref attribute on any tag to reference a type or member and the compiler will check that the reference exists.

       Name:  M:SomeClass.SomeOtherMethod
    summary:  Some other method.
    returns:  Return results are described through the returns tag.
    seealso:  Notice the use of the cref attribute to reference a specific method

       Name:  M:SomeClass.Main(System.String[])
    summary:  The entry point for the application.
      param:  A list of command line arguments

       Name:  P:SomeClass.Name
    summary:  Name property
      value:  A value tag is used to describe the property value
    ```

## <a name="adding-html-to-generated-text"></a>向生成的文本添加 HTML
 测试自定义指令处理器后，可能要向生成的文本添加一些 HTML。

#### <a name="to-add-html-to-the-generated-text"></a>向生成的文本添加 HTML

1. 用下面的代码替换 TestDP.tt 中的代码。 HTML 为突出显示状态。 请确保将字符串 `YOUR PATH` 替换为 Docfile.xml 文件的路径。

    > [!NOTE]
    > 其他打开的 \< # 和 close # > 标记与 HTML 标记中的语句代码分开。

    ```csharp
    <#@ assembly name="System.Xml" #>
    <#@ template debug="true" #>
    <#@ output extension=".htm" #>

    <#  //this will call the custom directive processor #>
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>

    <#  //uncomment this line if you want to see the generated transformation class #>
    <#  //System.Diagnostics.Debugger.Break(); #>

    <html><body>

    <#  //this will use the results of the directive processor #>
    <#  //the directive processor has read the XML and stored it in Document0#>
    <#
        XmlNode node = Document0.DocumentElement.SelectSingleNode("members");

        foreach (XmlNode member in node.ChildNodes)
        {
    #>
    <h3>
    <#
            XmlNode name = member.Attributes.GetNamedItem("name");
            WriteLine("{0,7}:  {1}", "Name", name.Value);
    #>
    </h3>
    <#
            foreach (XmlNode comment in member.ChildNodes)
            {
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText);
    #>
    <br/>
    <#
            }
        }
    #>
    </body></html>
    ```

    ```vb
    <#@ assembly name="System.Xml" #>
    <#@ template debug="true" language="vb" #>
    <#@ output extension=".htm" #>

    <#  'this will call the custom directive processor #>
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>

    <#  'uncomment this line if you want to see the generated transformation class #>
    <#  'System.Diagnostics.Debugger.Break() #>

    <html><body>

    <#  'this will use the results of the directive processor #>
    <#  'the directive processor has read the XML and stored it in Document0#>
    <#
        Dim node as XmlNode = Document0.DocumentElement.SelectSingleNode("members")

        Dim member As XmlNode
        For Each member In node.ChildNodes
    #>
    <h3>
    <#
            Dim name As XmlNode = member.Attributes.GetNamedItem("name")
            WriteLine("{0,7}:  {1}", "Name", name.Value)
    #>
    </h3>
    <#
            Dim comment As XmlNode
            For Each comment In member.ChildNodes
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText)
    #>
    <br/>
    <#
            Next
        Next
    #>
    </body></html>
    ```

2. 在 "**文件**" 菜单上，单击 "**保存 testdp.txt**"。

3. 若要在浏览器中查看输出，请在**解决方案资源管理器**中右键单击 testdp.txt，然后单击 "**在浏览器中查看**"。

     输出应与原始文本相同，只是应用了 HTML 格式。 每个项名称都应显示为粗体。
