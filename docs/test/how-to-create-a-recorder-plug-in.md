---
title: 创建适用于 Web 性能测试的记录器插件
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, recorder plug-in
ms.assetid: 6fe13be1-aeb5-4927-9bff-35950e194da9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5e32faa4525edc79da3d759d67ad2b5676f38fc2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589135"
---
# <a name="how-to-create-a-recorder-plug-in"></a>如何：创建记录器插件

通过 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin>，可以修改记录的 Web 性能测试。 应在“Web 性能测试记录器”工具栏中选择“停止”之后，但在“Web 性能测试编辑器”中保存和显示测试之前执行此修改   。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

记录器插件使你可对动态参数执行自己的自定义关联。 通过内置的关联功能，Web 性能测试会在测试完成时或在使用 Web 性能测试编辑器工具栏上的“将动态参数提升为 Web 测试参数”时，在 Web 记录中检测动态参数   。 但是，内置的检测功能并不是总能找到所有动态参数。 例如，该功能找不到通常会在 5 到 30 分钟之间更改其值的会话 ID。 因此，必须手动执行关联过程。

通过 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin>，您可以为自己的自定义插件编写代码。 在“Web 性能测试编辑器”中保存和显示 Web 性能测试之前，此插件可以多种方式执行关联或修改该 Web 性能测试。 因此，如果您确定必须为许多记录关联特定动态变量，则可自动执行此过程。

可以使用记录器插件的某些其他方法可用于在 Web 性能测试中添加提取和验证规则、添加上下文参数或将注释转换为事务。

下面的过程介绍如何为记录器插件创建基本代码、部署插件和执行插件。 这些过程之后的示例代码演示如何使用 Visual C# 创建自定义动态参数关联记录器插件。

## <a name="create-a-recorder-plug-in"></a>创建记录器插件

### <a name="to-create-a-recorder-plug-in"></a>创建记录器插件

1. 打开包含 Web 性能和负载测试项目以及要为之创建记录器插件的 Web 性能测试的解决方案。

2. 将新的“类库”项目添加到该解决方案中  。

3. 在解决方案资源管理器的新类库项目文件夹中，右键单击“引用”文件夹，然后选择“添加引用”    。

    > [!TIP]
    > 新类库项目文件夹的一个示例为“RecorderPlugins”  。

     随即显示“添加引用”对话框  。

4. 选择“.NET”选项卡  。

5. 向下滚动并选择“Microsoft.VisualStudio.QualityTools.WebTestFramework”，然后选择“确定”   。

     将“Microsoft.VisualStudio.QualityTools.WebTestFramework”添加到解决方案资源管理器的“引用”文件夹中    。

6. 为记录器插件编写代码。 首先，创建一个从 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin> 派生的新公共类。

7. 重写 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin.PostWebTestRecording*> 方法。

    ```csharp
    public class Class1 : WebTestRecorderPlugin
        {
            public override void PostWebTestRecording(object sender, PostWebTestRecordingEventArgs e)
            {
                base.PostWebTestRecording(sender, e);
            }
        }
    ```

     事件自变量将为你提供两个要使用的对象：记录的结果和记录的 Web 性能测试。 这样便可以循环访问结果以查找特定值，然后跳转到 Web 性能测试中的同一请求以进行修改。 当要添加上下文参数或参数化 URL 的某些部分时，还可以修改 Web 性能测试。

    > [!NOTE]
    > 如果确实要修改 Web 性能测试，则还需要将 <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostWebTestRecordingEventArgs.RecordedWebTestModified*> 属性设置为 true：`e.RecordedWebTestModified = true;`

8. 根据希望记录器插件在 Web 记录发生后执行的操作来添加更多代码。 例如，可以添加代码来处理自定义关联，如以下示例所示。 还可以为将注释转换为事务或向 Web 性能测试添加验证规则等操作创建记录器插件。

9. 在“生成”菜单上，选择“生成 \<类库项目名称>”   。

接下来，部署记录器插件以使其向 Visual Studio 注册。

### <a name="deploy-the-recorder-plug-in"></a>部署记录器插件

编译记录器插件后，将生成的 DLL 置于以下两个位置之一：

- %ProgramFiles(x86)%\Microsoft Visual Studio\\[version]\\[edition]\Common7\IDE\PrivateAssemblies\WebTestPlugins 

- %USERPROFILE%\Documents\Visual Studio [version]\WebTestPlugins 

> [!WARNING]
> 在将记录器插件复制到以上两个位置之一后，必须重新启动 Visual Studio，以便注册记录器插件。

### <a name="execute-the-recorder-plug-in"></a>执行记录器插件

1. 创建新的 Web 性能测试。

     随即显示“启用 WebTestRecordPlugins”对话框  。

2. 选中记录器插件对应的复选框，然后选择“确定”  。

     在 Web 性能测试完成记录后，将执行新记录器插件。

    > [!WARNING]
    > 在运行使用插件的 Web 性能测试或负载测试时，可能会出现与下类似的错误：
    >
    > **请求失败：\<插件> 事件中的异常：无法加载文件或程序集 '\<"Plug-in name".dll file>, Version=\<n.n.n.n>, Culture=neutral, PublicKeyToken=null' 或其依赖项之一。系统找不到指定的文件。**
    >
    > 如果对任何插件进行代码更改并创建新 DLL 版本 (Version=0.0.0.0)，则会引发这种情况，但插件仍会引用原来的插件版本  。 若要更正此问题，请执行以下步骤：
    >
    > 1. 在 Web 性能和负载测试项目中，将看到引用警告。 移除和重新添加对插件 DLL 的引用。
    > 2. 从测试或适当位置移除插件，然后再重新添加。

## <a name="example"></a>示例

此示例演示如何创建自定义的 Web 性能测试记录器插件以执行自定义动态参数关联。

> [!NOTE]
> 示例代码的完整列表位于本主题底部。

### <a name="iterate-through-the-result-to-find-first-page-with-reportsession"></a>循环访问结果以查找包含 ReportSession 的第一页

此部分代码示例循环访问每个记录的对象，并在响应正文中搜索 ReportSession。

```csharp
foreach (WebTestResultUnit unit in e.RecordedWebTestResult.Children)
 {
     WebTestResultPage page = unit as WebTestResultPage;
     if (page != null)
     {
         if (!foundId)
         {
             int indexOfReportSession = page.RequestResult.Response.BodyString.IndexOf("ReportSession");
             if (indexOfReportSession > -1)
             {
```

### <a name="add-an-extraction-rule"></a>添加提取规则

找到响应后，需要添加提取规则。 此部分示例代码使用 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRuleReference> 类创建提取规则，然后在 Web 性能测试中查找要向其添加提取规则的正确请求。 每个结果对象都会添加一个名为“DeclarativeWebTestItemId”的新属性，代码中正在使用该属性从 Web 性能测试中获取正确请求。

```csharp
ExtractionRuleReference ruleReference = new ExtractionRuleReference();
     ruleReference.Type = typeof(ExtractText);
     ruleReference.ContextParameterName = "SessionId";
     ruleReference.Properties.Add(new PluginOrRuleProperty("EndsWith", "&ControlID="));
     ruleReference.Properties.Add(new PluginOrRuleProperty("HtmlDecode", "True"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("IgnoreCase", "True"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("Index", "0"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("Required", "True"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("StartsWith", "ReportSession="));
     ruleReference.Properties.Add(new PluginOrRuleProperty("UseRegularExpression", "False"));

     WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
     if (requestInWebTest != null)
     {
         requestInWebTest.ExtractionRuleReferences.Add(ruleReference);
         e.RecordedWebTestModified = true;
     }
```

### <a name="replace-query-string-parameters"></a>替换查询字符串参数

现在，代码将查找以 ReportSession 作为名称的所有查询字符串参数并将其值更改为 {{SessionId}}，如此部分代码示例所示：

```csharp
WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
if (requestInWebTest != null)
{
    foreach (QueryStringParameter param in requestInWebTest.QueryStringParameters)
    {
         if (param.Name.Equals("ReportSession"))
         {
             param.Value = "{{SessionId}}";
         }
     }
 }
```

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.TestTools.WebTesting;
using Microsoft.VisualStudio.TestTools.WebTesting.Rules;

namespace RecorderPlugin
{
    [DisplayName("Correlate ReportSession")]
    [Description("Adds extraction rule for Report Session and binds this to querystring parameters that use ReportSession")]
    public class CorrelateSessionId : WebTestRecorderPlugin
    {
        public override void PostWebTestRecording(object sender, PostWebTestRecordingEventArgs e)
        {
            //first find the session id
            bool foundId = false;
            foreach (WebTestResultUnit unit in e.RecordedWebTestResult.Children)
            {
                WebTestResultPage page = unit as WebTestResultPage;
                if (page != null)
                {
                    if (!foundId)
                    {
                        int indexOfReportSession = page.RequestResult.Response.BodyString.IndexOf("ReportSession");
                        if (indexOfReportSession > -1)
                        {
                            //add an extraction rule to this request
                            // Get the corresponding request in the Declarative Web performance test
                            ExtractionRuleReference ruleReference = new ExtractionRuleReference();

                            ruleReference.Type = typeof(ExtractText);
                            ruleReference.ContextParameterName = "SessionId";
                            ruleReference.Properties.Add(new PluginOrRuleProperty("EndsWith", "&ControlID="));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("HtmlDecode", "True"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("IgnoreCase", "True"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("Index", "0"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("Required", "True"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("StartsWith", "ReportSession="));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("UseRegularExpression", "False"));

                            WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
                            if (requestInWebTest != null)
                            {
                                requestInWebTest.ExtractionRuleReferences.Add(ruleReference);
                                e.RecordedWebTestModified = true;
                            }
                            foundId = true;

                        }
                    }
                    else
                    {
                        //now update query string parameters
                        WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
                        if (requestInWebTest != null)
                        {
                            foreach (QueryStringParameter param in requestInWebTest.QueryStringParameters)
                            {
                                if (param.Name.Equals("ReportSession"))
                                {
                                    param.Value = "{{SessionId}}";
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin.PostWebTestRecording*>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRuleReference>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin.PostWebTestRecording*>
- [为负载测试创建自定义代码和插件](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [生成和运行编码的 Web 性能测试](../test/generate-and-run-a-coded-web-performance-test.md)
