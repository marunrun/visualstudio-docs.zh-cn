---
title: T4 参数指令 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 1d590387-1d9d-40a5-a72c-65fae7a8bdf3
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3e350b353d90143a0805455b29bfe0a14aad25cb
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63411604"
---
# <a name="t4-parameter-directive"></a>T4 参数指令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在中[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]文本模板`parameter`指令声明在模板代码中从外部上下文从传入的值初始化的属性。 如果您编写代码来调用文本转换，可以设置这些值。  
  
## <a name="using-the-parameter-directive"></a>使用参数指令  
  
```  
<#@ parameter type="Full.TypeName" name="ParameterName" #>  
```  
  
 `parameter`指令声明在模板代码中从外部上下文从传入的值初始化的属性。 如果您编写代码来调用文本转换，可以设置这些值。 传递的值可以是在`Session`字典中，或在<xref:System.Runtime.Remoting.Messaging.CallContext>。  
  
 您可以声明任何可远程处理类型的参数。 也就是说，必须使用声明类型<xref:System.SerializableAttribute>，或它必须派生自<xref:System.MarshalByRefObject>。 这允许参数值传递到在其中处理模板的 AppDomain。  
  
 例如，可以编写文本模板包含以下内容：  
  
```  
<#@ template language="C#" #>  
  
<#@ parameter type="System.Int32" name="TimesToRepeat" #>  
  
<# for (int i = 0; i < TimesToRepeat; i++) { #>  
Line <#= i #>  
<# } #>  
  
```  
  
## <a name="passing-parameter-values-to-a-template"></a>将参数值传递给模板  
 如果你正在编写[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]如菜单命令或事件处理程序的扩展，您可以通过使用文本模板化服务处理模板：  
  
```csharp  
// Get a service provider – how you do this depends on the context:  
IServiceProvider serviceProvider = dte; // or dslDiagram.Store, for example   
// Get the text template service:  
ITextTemplating t4 = serviceProvider.GetService(typeof(STextTemplating)) as ITextTemplating;  
ITextTemplatingSessionHost host = t4 as ITextTemplatingSessionHost;  
// Create a Session in which to pass parameters:  
host.Session = host.CreateSession();  
// Add parameter values to the Session:  
session["TimesToRepeat"] = 5;  
// Process a text template:  
string result = t4.ProcessTemplate("MyTemplateFile.t4",  
  System.IO.File.ReadAllText("MyTemplateFile.t4"));  
  
```  
  
## <a name="passing-values-in-the-call-context"></a>在调用上下文中将值传递  
 您可以或者将值传递中的为逻辑数据<xref:System.Runtime.Remoting.Messaging.CallContext>。  
  
 下面的示例通过使用这两种方法将传递值：  
  
```csharp  
ITextTemplating t4 = this.Store.GetService(typeof(STextTemplating)) as ITextTemplating;  
ITextTemplatingSessionHost host = t4 as ITextTemplatingSessionHost;  
host.Session = host.CreateSession();  
// Pass a value in Session:  
host.Session["p1"] = 32;  
// Pass another value in CallContext:  
System.Runtime.Remoting.Messaging.CallContext.LogicalSetData("p2", "test");  
  
// Process a small template inline:  
string result = t4.ProcessTemplate("",   
   "<#@parameter type=\"System.Int32\" name=\"p1\"#>"  
 + "<#@parameter type=\"System.String\" name=\"p2\"#>"  
 + "Test <#=p1#> <#=p2#>");  
  
// Result value is:  
//     Test 32 test  
  
```  
  
## <a name="passing-values-to-a-run-time-preprocessed-text-template"></a>将值传递到运行时 （预处理过的） 文本模板  
 它不是通常都需要使用`<#@parameter#>`使用运行时 （预处理） 文本模板指令。 相反，你可以定义另一个构造函数或生成的代码，传递参数值可设置属性。 有关详细信息，请参阅[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。  
  
 但是，如果你想要使用`<#@parameter>`在运行时模板中，您可以将值传递给它通过使用会话字典。 例如，假设您已经创建了文件作为名为预处理过的模板`PreTextTemplate1`。 通过使用下面的代码，可以在程序中调用该模板。  
  
```csharp  
PreTextTemplate1 t = new PreTextTemplate1();  
t.Session = new Microsoft.VisualStudio.TextTemplating.TextTemplatingSession();  
t.Session["TimesToRepeat"] = 5;  
// Add other parameter values to t.Session here.  
t.Initialize(); // Must call this to transfer values.  
string resultText = t.TransformText();  
  
```  
  
## <a name="obtaining-arguments-from-texttemplateexe"></a>从 TextTemplate.exe 获取自变量  
  
> [!IMPORTANT]
> `parameter`指令不会检索中设置的值`–a`参数的`TextTransform.exe`实用程序。 若要获取这些值，请设置`hostSpecific="true"`中`template`指令，并使用`this.Host.ResolveParameterValue("","","argName")`。
