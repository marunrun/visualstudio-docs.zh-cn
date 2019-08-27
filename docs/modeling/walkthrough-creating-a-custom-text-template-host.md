---
title: 演练：创建自定义文本模板宿主
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [text templates], custom host
- text templates, custom host walkthrough
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
dev_langs:
- CSharp
- VB
ms.openlocfilehash: b9d2447d07d9faabb5fc7eabddafc328756056ca
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68870661"
---
# <a name="walkthrough-create-a-custom-text-template-host"></a>演练：创建自定义文本模板主机

*文本模板宿主*提供了一个环境, 该环境允许*文本模板转换引擎*运行。 宿主负责管理引擎与文件系统的交互。 需要文件或程序集的引擎或*指令处理器*可以从主机请求资源。 然后，宿主可以搜索目录和全局程序集缓存，以查找请求的资源。 有关详细信息, 请参阅[文本模板转换过程](../modeling/the-text-template-transformation-process.md)。

如果要在 Visual Studio 外部使用*文本模板转换*功能, 或者希望将该功能集成到自定义工具中, 则可以编写自定义主机。 若要创建自定义主机, 你必须创建一个继承自[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))的类。 有关各个方法的文档, 请参阅[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))。

> [!WARNING]
> 如果你正在编写 Visual Studio 扩展或包, 请考虑使用文本模板化服务而不是创建你自己的主机。 有关详细信息, 请参阅[在 VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。

本演练阐释了以下任务：

- 创建自定义文本模板宿主。

- 测试自定义主机。

## <a name="prerequisites"></a>系统必备

若要完成本演练，您必须具有：

- Visual Studio 2010 或更高版本

- Visual Studio SDK

## <a name="create-a-custom-text-template-host"></a>创建自定义文本模板主机

在本演练中，您将在可从命令行调用的可执行应用程序中创建自定义宿主。 该应用程序接受文本模板文件作为参数，读取该模板，调用引擎转换模板，并在命令提示符窗口中显示发生的所有错误。

1. 在 Visual Studio 中，新建一个名为 CustomHost 的 Visual Basic 或 C# 控制台应用程序。

2. 添加对下列程序集的引用：

   - **Microsoft.VisualStudio.TextTemplating.\*.0**

   - **VisualStudio. TextTemplating 和更高版本**

3. 用下面的代码替换 Program.cs 或 Module1.vb 文件中的代码：

   ```csharp
   using System;
   using System.IO;
   using System.CodeDom.Compiler;
   using System.Collections.Generic;
   using System.Text;
   using Microsoft.VisualStudio.TextTemplating;

   namespace CustomHost
   {
       //The text template transformation engine is responsible for running
       //the transformation process.
       //The host is responsible for all input and output, locating files,
       //and anything else related to the external environment.
       //-------------------------------------------------------------------------
       class CustomCmdLineHost : ITextTemplatingEngineHost
       {
           //the path and file name of the text template that is being processed
           //---------------------------------------------------------------------
           internal string TemplateFileValue;
           public string TemplateFile
           {
               get { return TemplateFileValue; }
           }
           //This will be the extension of the generated text output file.
           //The host can provide a default by setting the value of the field here.
           //The engine can change this value based on the optional output directive
           //if the user specifies it in the text template.
           //---------------------------------------------------------------------
           private string fileExtensionValue = ".txt";
           public string FileExtension
           {
               get { return fileExtensionValue; }
           }
           //This will be the encoding of the generated text output file.
           //The host can provide a default by setting the value of the field here.
           //The engine can change this value based on the optional output directive
           //if the user specifies it in the text template.
           //---------------------------------------------------------------------
           private Encoding fileEncodingValue = Encoding.UTF8;
           public Encoding FileEncoding
           {
               get { return fileEncodingValue; }
           }
           //These are the errors that occur when the engine processes a template.
           //The engine passes the errors to the host when it is done processing,
           //and the host can decide how to display them. For example, the host
           //can display the errors in the UI or write them to a file.
           //---------------------------------------------------------------------
           private CompilerErrorCollection errorsValue;
           public CompilerErrorCollection Errors
           {
               get { return errorsValue; }
           }
           //The host can provide standard assembly references.
           //The engine will use these references when compiling and
           //executing the generated transformation class.
           //--------------------------------------------------------------
           public IList<string> StandardAssemblyReferences
           {
               get
               {
                   return new string[]
                   {
                       //If this host searches standard paths and the GAC,
                       //we can specify the assembly name like this.
                       //---------------------------------------------------------
                       //"System"

                       //Because this host only resolves assemblies from the
                       //fully qualified path and name of the assembly,
                       //this is a quick way to get the code to give us the
                       //fully qualified path and name of the System assembly.
                       //---------------------------------------------------------
                       typeof(System.Uri).Assembly.Location
                   };
               }
           }
           //The host can provide standard imports or using statements.
           //The engine will add these statements to the generated
           //transformation class.
           //--------------------------------------------------------------
           public IList<string> StandardImports
           {
               get
               {
                   return new string[]
                   {
                       "System"
                   };
               }
           }
           //The engine calls this method based on the optional include directive
           //if the user has specified it in the text template.
           //This method can be called 0, 1, or more times.
           //---------------------------------------------------------------------
           //The included text is returned in the context parameter.
           //If the host searches the registry for the location of include files,
           //or if the host searches multiple locations by default, the host can
           //return the final path of the include file in the location parameter.
           //---------------------------------------------------------------------
           public bool LoadIncludeText(string requestFileName, out string content, out string location)
           {
               content = System.String.Empty;
               location = System.String.Empty;

               //If the argument is the fully qualified path of an existing file,
               //then we are done.
               //----------------------------------------------------------------
               if (File.Exists(requestFileName))
               {
                   content = File.ReadAllText(requestFileName);
                   return true;
               }
               //This can be customized to search specific paths for the file.
               //This can be customized to accept paths to search as command line
               //arguments.
               //----------------------------------------------------------------
               else
               {
                   return false;
               }
           }
           //Called by the Engine to enquire about
           //the processing options you require.
           //If you recognize that option, return an
           //appropriate value.
           //Otherwise, pass back NULL.
           //--------------------------------------------------------------------
           public object GetHostOption(string optionName)
           {
           object returnObject;
           switch (optionName)
           {
           case "CacheAssemblies":
                       returnObject = true;
        break;
           default:
           returnObject = null;
           break;
           }
           return returnObject;
           }
           //The engine calls this method to resolve assembly references used in
           //the generated transformation class project and for the optional
           //assembly directive if the user has specified it in the text template.
           //This method can be called 0, 1, or more times.
           //---------------------------------------------------------------------
           public string ResolveAssemblyReference(string assemblyReference)
           {
               //If the argument is the fully qualified path of an existing file,
               //then we are done. (This does not do any work.)
               //----------------------------------------------------------------
               if (File.Exists(assemblyReference))
               {
                   return assemblyReference;
               }
               //Maybe the assembly is in the same folder as the text template that
               //called the directive.
               //----------------------------------------------------------------
               string candidate = Path.Combine(Path.GetDirectoryName(this.TemplateFile), assemblyReference);
               if (File.Exists(candidate))
               {
                   return candidate;
               }
               //This can be customized to search specific paths for the file
               //or to search the GAC.
               //----------------------------------------------------------------
               //This can be customized to accept paths to search as command line
               //arguments.
               //----------------------------------------------------------------
               //If we cannot do better, return the original file name.
               return "";
           }
           //The engine calls this method based on the directives the user has
           //specified in the text template.
           //This method can be called 0, 1, or more times.
           //---------------------------------------------------------------------
           public Type ResolveDirectiveProcessor(string processorName)
           {
               //This host will not resolve any specific processors.
               //Check the processor name, and if it is the name of a processor the
               //host wants to support, return the type of the processor.
               //---------------------------------------------------------------------
               if (string.Compare(processorName, "XYZ", StringComparison.OrdinalIgnoreCase) == 0)
               {
                   //return typeof();
               }
               //This can be customized to search specific paths for the file
               //or to search the GAC
               //If the directive processor cannot be found, throw an error.
               throw new Exception("Directive Processor not found");
           }
           //A directive processor can call this method if a file name does not
           //have a path.
           //The host can attempt to provide path information by searching
           //specific paths for the file and returning the file and path if found.
           //This method can be called 0, 1, or more times.
           //---------------------------------------------------------------------
           public string ResolvePath(string fileName)
           {
               if (fileName == null)
               {
                   throw new ArgumentNullException("the file name cannot be null");
               }
               //If the argument is the fully qualified path of an existing file,
               //then we are done
               //----------------------------------------------------------------
               if (File.Exists(fileName))
               {
                   return fileName;
               }
               //Maybe the file is in the same folder as the text template that
               //called the directive.
               //----------------------------------------------------------------
               string candidate = Path.Combine(Path.GetDirectoryName(this.TemplateFile), fileName);
               if (File.Exists(candidate))
               {
                   return candidate;
               }
               //Look more places.
               //----------------------------------------------------------------
               //More code can go here...
               //If we cannot do better, return the original file name.
               return fileName;
           }
           //If a call to a directive in a text template does not provide a value
           //for a required parameter, the directive processor can try to get it
           //from the host by calling this method.
           //This method can be called 0, 1, or more times.
           //---------------------------------------------------------------------
           public string ResolveParameterValue(string directiveId, string processorName, string parameterName)
           {
               if (directiveId == null)
               {
                   throw new ArgumentNullException("the directiveId cannot be null");
               }
               if (processorName == null)
               {
                   throw new ArgumentNullException("the processorName cannot be null");
               }
               if (parameterName == null)
               {
                   throw new ArgumentNullException("the parameterName cannot be null");
               }
               //Code to provide "hard-coded" parameter values goes here.
               //This code depends on the directive processors this host will interact with.
               //If we cannot do better, return the empty string.
               return String.Empty;
           }
           //The engine calls this method to change the extension of the
           //generated text output file based on the optional output directive
           //if the user specifies it in the text template.
           //---------------------------------------------------------------------
           public void SetFileExtension(string extension)
           {
               //The parameter extension has a '.' in front of it already.
               //--------------------------------------------------------
               fileExtensionValue = extension;
           }
           //The engine calls this method to change the encoding of the
           //generated text output file based on the optional output directive
           //if the user specifies it in the text template.
           //----------------------------------------------------------------------
           public void SetOutputEncoding(System.Text.Encoding encoding, bool fromOutputDirective)
           {
               fileEncodingValue = encoding;
           }
           //The engine calls this method when it is done processing a text
           //template to pass any errors that occurred to the host.
           //The host can decide how to display them.
           //---------------------------------------------------------------------
           public void LogErrors(CompilerErrorCollection errors)
           {
               errorsValue = errors;
           }
           //This is the application domain that is used to compile and run
           //the generated transformation class to create the generated text output.
           //----------------------------------------------------------------------
           public AppDomain ProvideTemplatingAppDomain(string content)
           {
               //This host will provide a new application domain each time the
               //engine processes a text template.
               //-------------------------------------------------------------
               return AppDomain.CreateDomain("Generation App Domain");
               //This could be changed to return the current appdomain, but new
               //assemblies are loaded into this AppDomain on a regular basis.
               //If the AppDomain lasts too long, it will grow indefintely,
               //which might be regarded as a leak.
               //This could be customized to cache the application domain for
               //a certain number of text template generations (for example, 10).
               //This could be customized based on the contents of the text
               //template, which are provided as a parameter for that purpose.
           }
       }
       //This will accept the path of a text template as an argument.
       //It will create an instance of the custom host and an instance of the
       //text templating transformation engine, and will transform the
       //template to create the generated text output file.
       //-------------------------------------------------------------------------
       class Program
       {
           static void Main(string[] args)
           {
               try
               {
                   ProcessTemplate(args);
               }
               catch (Exception ex)
               {
                   Console.WriteLine(ex.Message);
               }
           }
           static void ProcessTemplate(string[] args)
           {
               string templateFileName = null;
               if (args.Length == 0)
               {
                   throw new System.Exception("you must provide a text template file path");
               }
               templateFileName = args[0];
               if (templateFileName == null)
               {
                   throw new ArgumentNullException("the file name cannot be null");
               }
               if (!File.Exists(templateFileName))
               {
                   throw new FileNotFoundException("the file cannot be found");
               }
               CustomCmdLineHost host = new CustomCmdLineHost();
               Engine engine = new Engine();
               host.TemplateFileValue = templateFileName;
               //Read the text template.
               string input = File.ReadAllText(templateFileName);
               //Transform the text template.
               string output = engine.ProcessTemplate(input, host);
               string outputFileName = Path.GetFileNameWithoutExtension(templateFileName);
               outputFileName = Path.Combine(Path.GetDirectoryName(templateFileName), outputFileName);
               outputFileName = outputFileName + "1" + host.FileExtension;
               File.WriteAllText(outputFileName, output, host.FileEncoding);

               foreach (CompilerError error in host.Errors)
               {
                   Console.WriteLine(error.ToString());
               }
           }
       }
   }
   ```

   ```vb
   Imports System
   Imports System.IO
   Imports System.CodeDom.Compiler
   Imports System.Collections.Generic
   Imports System.Text
   Imports Microsoft.VisualStudio.TextTemplating

   Namespace CustomHost
       'The text template transformation engine is responsible for running
       'the transformation process.
       'The host is responsible for all input and output, locating files,
       'and anything else related to the external environment.
       '-------------------------------------------------------------------------
       Public Class CustomCmdLineHost
           Implements ITextTemplatingEngineHost

           'the path and file name of the text template that is being processed
           '---------------------------------------------------------------------
           Friend TemplateFileValue As String
           Public ReadOnly Property TemplateFile() As String Implements ITextTemplatingEngineHost.TemplateFile
               Get
                   Return TemplateFileValue
               End Get
           End Property
           'This will be the extension of the generated text output file.
           'The host can provide a default by setting the value of the field here.
           'The engine can change this based on the optional output directive
           'if the user specifies it in the text template.
           '---------------------------------------------------------------------
           Private fileExtensionValue As String = ".txt"
           Public ReadOnly Property FileExtension() As String
               Get
                   Return fileExtensionValue
               End Get
           End Property
           'This will be the encoding of the generated text output file.
           'The host can provide a default by setting the value of the field here.
           'The engine can change this value based on the optional output directive
           'if the user specifies it in the text template.
           '---------------------------------------------------------------------
           Private fileEncodingValue As Encoding = Encoding.UTF8
           Public ReadOnly Property fileEncoding() As Encoding
               Get
                   Return fileEncodingValue
               End Get
           End Property
           'These are the errors that occur when the engine processes a template.
           'The engine passes the errors to the host when it is done processing,
           'and the host can decide how to display them. For example, the host
           'can display the errors in the UI or write them to a file.
           '---------------------------------------------------------------------
           Private errorsValue As CompilerErrorCollection
           Public ReadOnly Property Errors() As CompilerErrorCollection
               Get
                   Return errorsValue
               End Get
           End Property
           'The host can provide standard assembly references.
           'The engine will use these references when compiling and
           'executing the generated transformation class.
           '--------------------------------------------------------------
           Public ReadOnly Property StandardAssemblyReferences() As IList(Of String) Implements ITextTemplatingEngineHost.StandardAssemblyReferences
               Get
                   'If this host searches standard paths and the GAC,
                   'we can specify the assembly name like this.
                   '---------------------------------------------------------
                   'Return New String() {"System"}
                   'Because this host only resolves assemblies from the
                   'fully qualified path and name of the assembly,
                   'this is a quick way to get the code to give us the
                   'fully qualified path and name of the System assembly.
                   '---------------------------------------------------------
                   Return New String() {(New System.UriBuilder()).GetType().Assembly.Location}
               End Get
           End Property
           'The host can provide standard imports or imports statements.
           'The engine will add these statements to the generated
           'transformation class.
           '--------------------------------------------------------------
           Public ReadOnly Property StandardImports() As IList(Of String) Implements ITextTemplatingEngineHost.StandardImports
               Get
                   Return New String() {"System"}
               End Get
           End Property
           ' Called by the Engine to enquire about
           ' the processing options you require.
           ' If you recognize that option, return an
           ' appropriate value.
           ' Otherwise, pass back NULL.
           '--------------------------------------------------------------------
           Public Function GetHostOption(ByVal optionName As String) As Object Implements ITextTemplatingEngineHost.GetHostOption
               Dim returnObject As Object
               Select Case optionName
                   Case "CacheAssemblies"
                       returnObject = True
                   Case Else
                       returnObject = False
               End Select
               Return returnObject
           End Function
           'The engine calls this method based on the optional include directive
           'if the user has specified it in the text template.
           'This method can be called 0, 1, or more times.
           '---------------------------------------------------------------------
           'The included text is returned in the context parameter.
           'If the host searches the registry for the location of include files
           'or if the host searches multiple locations by default, the host can
           'return the final path of the include file in the location parameter.
           '---------------------------------------------------------------------
           Public Function LoadIncludeText(ByVal requestFileName As String, ByRef content As String, ByRef location As String) As Boolean Implements ITextTemplatingEngineHost.LoadIncludeText
               content = System.String.Empty
               location = System.String.Empty
               'If the argument is the fully qualified path of an existing file,
               'then we are done.
               '----------------------------------------------------------------
               If File.Exists(requestFileName) Then
                   content = File.ReadAllText(requestFileName)
                   Return True
               'This can be customized to search specific paths for the file.
               'This can be customized to accept paths to search as command line
               'arguments.
               '----------------------------------------------------------------
               Else
                   Return False
               End If
           End Function
           'The engine calls this method to resolve assembly references used in
           'the generated transformation class project and for the optional
           'assembly directive if the user has specified it in the text template.
           'This method can be called 0, 1, or more times.
           '---------------------------------------------------------------------
           Public Function ResolveAssemblyReference(ByVal assemblyReference As String) As String Implements ITextTemplatingEngineHost.ResolveAssemblyReference
               'If the argument is the fully qualified path of an existing file,
               'then we are done. (This does not do any work.)
               '----------------------------------------------------------------
               If File.Exists(assemblyReference) Then
                   Return assemblyReference
               End If
               'Maybe the assembly is in the same folder as the text template that
               'called the directive.
               '----------------------------------------------------------------
               Dim candidate As String = Path.Combine(Path.GetDirectoryName(Me.TemplateFile), assemblyReference)
               If File.Exists(candidate) Then
                   Return candidate
               End If
               'This can be customized to search specific paths for the file,
               'or to search the GAC.
               '----------------------------------------------------------------
               'This can be customized to accept paths to search as command line
               'arguments.
               '----------------------------------------------------------------
               'If we cannot do better, return the original file name.
               Return ""
           End Function
           'The engine calls this method based on the directives the user has
           'specified in the text template.
           'This method can be called 0, 1, or more times.
           '---------------------------------------------------------------------
           Public Function ResolveDirectiveProcessor(ByVal processorName As String) As System.Type Implements ITextTemplatingEngineHost.ResolveDirectiveProcessor
               'This host will not resolve any specific processors.
               'Check the processor name, and if it is the name of a processor the
               'host wants to support, return the type of the processor.
               '---------------------------------------------------------------------
               If String.Compare(processorName, "XYZ", StringComparison.InvariantCultureIgnoreCase) = 0 Then
                   'return typeof()
               End If
               'This can be customized to search specific paths for the file,
               'or to search the GAC.
               'If the directive processor cannot be found, throw an error.
               Throw New Exception("Directive Processor not found")
           End Function
           'A directive processor can call this method if a file name does not
           'have a path.
           'The host can attempt to provide path information by searching
           'specific paths for the file and returning the file and path if found.
           'This method can be called 0, 1, or more times.
           '---------------------------------------------------------------------
           Public Function ResolvePath(ByVal fileName As String) As String Implements ITextTemplatingEngineHost.ResolvePath
               If fileName Is Nothing Then
                   Throw New ArgumentNullException("the file name cannot be null")
               End If
               'If the argument is the fully qualified path of an existing file,
               'then we are done.
               '----------------------------------------------------------------
               If File.Exists(fileName) Then
                   Return fileName
               End If
               'Maybe the file is in the same folder as the text template that
               'called the directive.
               '----------------------------------------------------------------
               Dim candidate As String = Path.Combine(Path.GetDirectoryName(Me.TemplateFile), fileName)
               If File.Exists(candidate) Then
                   Return candidate
               End If
               'Look more places.
               '----------------------------------------------------------------
               'More code can go here...
               'If we cannot do better, return the original file name
               Return fileName
           End Function
           'If a call to a directive in a text template does not provide a value
           'for a required parameter, the directive processor can try to get it
           'from the host by calling this method.
           'This method can be called 0, 1, or more times.
           '---------------------------------------------------------------------
           Public Function ResolveParameterValue(ByVal directiveId As String, ByVal processorName As String, ByVal parameterName As String) As String Implements ITextTemplatingEngineHost.ResolveParameterValue
               If directiveId Is Nothing Then
                   Throw New ArgumentNullException("the directiveId cannot be null")
               End If
               If processorName Is Nothing Then
                   Throw New ArgumentNullException("the processorName cannot be null")
               End If
               If parameterName Is Nothing Then
                   Throw New ArgumentNullException("the parameterName cannot be null")
               End If
               'Code to provide "hard-coded" parameter values goes here.
               'This code depends on the directive processors this host will interact with.
               'If we cannot do better, return the empty string.
               Return String.Empty
           End Function
           'The engine calls this method to change the extension of the
           'generated text output file based on the optional output directive
           'if the user specifies it in the text template.
           '---------------------------------------------------------------------
           Public Sub SetFileExtension(ByVal extension As String) Implements ITextTemplatingEngineHost.SetFileExtension
               'The parameter extension has a '.' in front of it already.
               '--------------------------------------------------------
               fileExtensionValue = extension
           End Sub
           'The engine calls this method to change the encoding of the
           'generated text output file based on the optional output directive
           'if the user specifies it in the text template.
           '---------------------------------------------------------------------
           Public Sub SetOutputEncoding(ByVal encoding As System.Text.Encoding, ByVal fromOutputDirective As Boolean) Implements ITextTemplatingEngineHost.SetOutputEncoding
               fileEncodingValue = encoding
           End Sub
           'The engine calls this method when it is done processing a text
           'template to pass any errors that occurred to the host.
           'The host can decide how to display them.
           '---------------------------------------------------------------------
           Public Sub LogErrors(ByVal errors As System.CodeDom.Compiler.CompilerErrorCollection) Implements ITextTemplatingEngineHost.LogErrors
               errorsValue = errors
           End Sub
           'This is the application domain that is used to compile and run
           'the generated transformation class to create the generated text output.
           '----------------------------------------------------------------------
           Public Function ProvideTemplatingAppDomain(ByVal content As String) As System.AppDomain Implements ITextTemplatingEngineHost.ProvideTemplatingAppDomain
               'This host will provide a new application domain each time the
               'engine processes a text template.
               '-------------------------------------------------------------
               Return AppDomain.CreateDomain("Generation App Domain")
               'This could be changed to return the current appdomain, but new
               'assemblies are loaded into this AppDomain on a regular basis.
               'If the AppDomain lasts too long, it will grow indefintely,
               'which might be regarded as a leak.
               'This could be customized to cache the application domain for
               'a certain number of text template generations (for example, 10).
               'This could be customized based on the contents of the text
               'template, which are provided as a parameter for that purpose.
           End Function
       End Class 'CustomCmdLineHost
       'This will accept the path of a text template as an argument.
       'It will create an instance of the custom host and an instance of the
       'text templating transformation engine. It will also transform the
       'template to create the generated text output file.
       '-------------------------------------------------------------------------
       Class Program
           Shared Sub Main(ByVal args As String())
               Try
                   ProcessTemplate(args)
               Catch ex As Exception
                   Console.WriteLine(ex.Message)
               End Try
           End Sub
           Shared Sub ProcessTemplate(ByVal args As String())
               Dim templateFileName As String = ""
               If args.Length = 0 Then
                   Throw New System.Exception("you must provide a text template file path")
               End If
               templateFileName = args(0)
               If templateFileName Is Nothing Then
                   Throw New ArgumentNullException("the file name cannot be null")
               End If
               If Not File.Exists(templateFileName) Then
                   Throw New FileNotFoundException("the file cannot be found")
               End If
               Dim host As CustomCmdLineHost = New CustomCmdLineHost()
               Dim engine As Engine = New Engine()
               host.TemplateFileValue = templateFileName
               'Read the text template.
               Dim input As String = File.ReadAllText(templateFileName)
               'Transform the text template.
               Dim output As String = engine.ProcessTemplate(input, host)
               Dim outputFileName As String = Path.GetFileNameWithoutExtension(templateFileName)
               outputFileName = Path.Combine(Path.GetDirectoryName(templateFileName), outputFileName)
               outputFileName = outputFileName & "1" & host.FileExtension
               File.WriteAllText(outputFileName, output, host.fileEncoding)
               Dim e As CompilerError
               For Each e In host.Errors
                   Console.WriteLine(e.ToString())
               Next
           End Sub 'ProcessTemplate
       End Class 'Program
   End Namespace
   ```

4. 仅[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]对于, 打开 "**项目**" 菜单, 然后单击 " **CustomHost 属性**"。 在 "**启动对象**" 列表中, 单击 " **CustomHost**"。

5. 在“文件” 菜单上，单击“全部保存”。

6. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

## <a name="test-the-custom-host"></a>测试自定义主机

若要测试自定义主机，你需要编写一个文本模板，然后运行自定义主机，将文本模板的名称传递给它并验证模板转换。

### <a name="to-create-a-text-template-to-test-the-custom-host"></a>创建文本模板测试自定义主机

1. 创建一个文本文件, 并将其`TestTemplate.tt`命名为。

     可以使用任何文本编辑器（例如记事本）来创建文件。

2. 将以下内容添加到文件中：

    > [!NOTE]
    > 文本模板的编程语言不必与自定义宿主的编程语言一致。

    ```csharp
    Text Template Host Test

    <#@ template debug="true" #>

    <# //Uncomment this line to test that the host allows the engine to set the extension. #>
    <# //@ output extension=".htm" #>

    <# //Uncomment this line if you want to debug the generated transformation class. #>
    <# //System.Diagnostics.Debugger.Break(); #>

    <# for (int i=0; i<3; i++)
       {
           WriteLine("This is a test");
       }
    #>
    ```

    ```vb
    Text Template Host Test

    <#@ template debug="true" language="VB"#>

    <# 'Uncomment this line to test that the host allows the engine to set the extension. #>
    <# '@ output extension=".htm" #>

    <# 'Uncomment this line if you want to debug the generated transformation class. #>
    <# 'System.Diagnostics.Debugger.Break() #>

    <# Dim i As Integer
       For i = 0 To 2

           WriteLine("This is a test")
       Next
    #>

    ```

3. 保存并关闭文件。

### <a name="to-test-the-custom-host"></a>测试自定义主机

1. 打开“命令提示符”窗口。

2. 为自定义宿主键入可执行文件的路径，但暂不要按 Enter。

     例如，键入：

     `<YOUR PATH>CustomHost\bin\Debug\CustomHost.exe`

    > [!NOTE]
    > 您可以在**Windows 资源管理器**中浏览到文件 CustomHost, 然后将该文件拖入命令提示符窗口, 而不是键入地址。

3. 键入一个空格。

4. 键入文本模板文件的路径，然后按 Enter。

     例如，键入：

     `C:\<YOUR PATH>TestTemplate.tt`

    > [!NOTE]
    > 您可以在**Windows 资源管理器**中浏览到文件 TestTemplate.tt, 然后将该文件拖入命令提示符窗口, 而不是键入地址。

     自定义宿主应用程序运行并完成文本模板转换过程。

5. 在**Windows 资源管理器**中, 浏览到包含文件 TestTemplate.tt 的文件夹。

     该文件夹还包含文件 TestTemplate1.txt。

6. 打开此文件可以查看文本模板转换的结果。

     此时将显示生成的文本输出，如下所示：

    ```
    Text Template Host Test

    This is a test
    This is a test
    This is a test
    ```

## <a name="next-steps"></a>后续步骤

在本演练中，你创建了一个支持基本转换功能的文本模板转换主机。 您可以对该宿主进行扩展，以支持可调用自定义或生成的指令处理器的文本模板。 有关详细信息，请参见[演练：将主机连接到生成的指令处理器](../modeling/walkthrough-connecting-a-host-to-a-generated-directive-processor.md)。

## <a name="see-also"></a>请参阅

- [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))
