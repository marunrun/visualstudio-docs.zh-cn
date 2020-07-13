---
title: 创建 Web 服务测试
ms.date: 06/30/2020
ms.topic: how-to
helpviewer_keywords:
- Web performance tests, creating Web service tests
- Web services [Visual Studio ALM], creating
- service tests, Web
ms.assetid: fbcd57ee-06ad-4260-8694-09f8e0f93e39
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9934f48e6d5900a418995eb96d357b4ea1ea532f
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814754"
---
# <a name="how-to-create-a-web-service-test"></a>如何：创建 Web 服务测试

可以使用 Web 性能测试对 Web 服务进行测试。 使用“插入请求”和“插入 Web 服务请求”选项，可以在“Web 性能测试编辑器”中自定义各个请求以查找 Web 服务页。 通常，并不在 Web 应用程序中显示这些页。 因此，必须自定义请求才能访问这些页。

>[!NOTE]
> Visual Studio 2019 已弃用 Web 性能和负载测试功能。 对于 Application Insights，多步骤 Web 测试依赖于 Visual Studio webtest 文件。 我们已[宣布](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/)，Visual Studio 2019 将是支持 WebTest 功能的最后一个版本。 尽管我们不会添加任何新功能，但目前仍支持 Visual Studio 2019 中的 WebTest 功能，并且在该产品的支持生命周期内仍将继续提供支持，了解这一点至关重要。 有关多步骤可用性测试的未来情况问题，Azure Monitor 产品团队已提供解决方案，请参阅[此处](https://github.com/MicrosoftDocs/azure-docs/issues/26050#issuecomment-468814101)。

**要求**

Visual Studio Enterprise

## <a name="to-create-a-simple-web-service"></a>创建一个简单的 Web 服务

你可使用自己的 Web 服务进行测试，也可使用 Visual Studio 中包含的基本 Web 服务 (ASMX) 模板。 若要使用此模板创建简单的 Web 服务：

1. 在 Visual Studio 中，使用 ASP.NET Web 应用程序 (.NET Framework) 模板创建一个新项目，并在出现提示时选择“空”模板。 键入名称并创建项目。

1. 在解决方案资源管理器中，右键单击项目节点，选择“添加” > “新项”，然后选择“Web 服务(ASMX)”  。 添加 Web 服务。

1. 打开 WebService1.asmx，用以下代码替换默认的 `HelloWorld` Web 方法。

   ```csharp
   public string HelloWorld(string str)
   {
      return "Hello, " + str;
   }
   ```

## <a name="install-the-load-testing-component"></a>安装负载测试组件

如果尚未安装 Web 性能和负载测试工具组件，则需通过 Visual Studio 安装程序进行安装。

1. 从 Windows 的“开始”菜单打开“Visual Studio 安装程序” 。 在 Visual Studio 中，也可从“新建项目”对话框访问它，或从菜单栏中选择“工具” > “获取工具和功能”访问 。

1. 在“Visual Studio 安装程序”中，选择“单个组件”选项卡，然后向下滚动到“调试和测试”部分  。 选择“Web 性能和负载测试工具”。

   ![Web 性能和负载测试工具组件](media/web-perf-load-testing-tools-component.png)

1. 选择“修改”按钮。

   已安装 Web 性能和负载测试工具组件。

## <a name="create-a-web-test-project"></a>创建 Web 测试项目

Web 测试需要“Web 性能和负载测试项目”项目模板。 本节将创建一个 C# 负载测试项目。 如果愿意，还可创建 Visual Basic 负载测试项目。

::: moniker range="vs-2017"

1. 打开 Visual Studio。

   如果使用的是示例 Web 服务 (ASMX) 模板，可将 Web 测试项目添加到同一解决方案中。

2. 从菜单栏中依次选择“文件”>“新建”>“项目”。

   **“新建项目”** 对话框随即打开。

3. 在“新建项目”对话框中，依次展开“已安装”、“Visual C#”，然后选择“测试”类别   。 选择“Web 性能和负载测试项目”模板。

   ![Web 性能和负载测试项目模板](media/web-perf-load-test-project-template.png)

4. 如果不想使用默认名称，请输入项目名，然后选择“确定”。

::: moniker-end

::: moniker range=">=vs-2019"

1. 打开 Visual Studio。

   如果使用的是示例 Web 服务 (ASMX) 模板，可将 Web 测试项目添加到同一解决方案中。

2. 在“开始”窗口上，选择“创建新项目”。

3. 在“创建新项目”页中，在搜索框中键入“web test”，然后选择适用于 C# 的“Web 性能和负载测试项目\[已弃用]”模板  。 选择“下一步”。

4. 如果不想使用默认名称，请输入项目名，然后选择“创建”。

::: moniker-end

   Visual Studio 将创建项目并在“解决方案资源管理器”中显示文件。 该项目最初包含一个名为 WebTest1.webtest 的 Web 测试文件。

## <a name="to-test-a-web-service"></a>测试 Web 服务

1. 启动 Web 服务，必要时选择“停止”来暂停服务。

1. 在 Web 测试项目中，打开 WebTest1.webtest，这将打开 Web 性能测试编辑器。 在测试编辑器中右键单击“Web 性能测试”，然后选择“添加 Web 服务请求”。

1. 在新请求的“Url”属性中，键入 Web 服务的名称，如 https://localhost:44318/WebService1.asmx。

1. 对于 Web 服务，打开单独的浏览器会话，在“地址”工具栏中键入 .asmx 页面的 URL。 在网页顶部，选择要用于测试和检查 SOAP 消息的方法。 （在示例 Web 服务中，采用 HelloWorld 方法。）打开该方法时，会看到它包含 `SOAPAction`。

1. 在“Web 性能测试编辑器”中，右击请求并选择“添加标题”，以添加新标题 。 在“名称”属性中键入 `SOAPAction`。 在“值”属性中，键入你在 `SOAPAction` 中看到的值，例如 http://tempuri.org/HelloWorld。

1. 在测试编辑器中展开 URL 节点，选择“字符串正文”节点并在“内容类型”属性中输入 `text/xml` 的值 。

1. 返回到步骤 4 中的浏览器，从 Web 服务描述页中选择 SOAP 请求的 XML 部分并将它复制到剪贴板中。

   XML 内容如下例所示：

     ```xml
     <?xml version="1.0" encoding="utf-8"?>
     <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
       <soap:Body>
         <HelloWorld xmlns="http://tempuri.org/">
           <str>string</str>
         </HelloWorld>
       </soap:Body>
     </soap:Envelope>
     ```

1. 返回到 Web 性能测试编辑器，然后选择“字符串正文”属性中的省略号 (…) 。 将剪贴板中的内容粘贴到该属性中。

1. 将 XML 中的所有占位符值替换为有效值，以便测试可以通过。 在上述示例中，用名称替换 `string` 的实例。

1. 右击 Web 服务请求并选择“添加 URL QueryString 参数”。

1. 为查询字符串参数赋予一个名称和值。 在前面的示例中，名称为 `op`，值为 `HelloWorld`。 这标识要执行的 Web 服务操作。

    > [!NOTE]
    > 通过使用 `{{DataSourceName.TableName.ColumnName}}` 语法，可在 SOAP 正文中使用数据绑定，用数据绑定值替换所有占位符值。

1. 运行测试。 在“Web 性能测试结果查看器”的顶部窗格中，选择 Web 服务请求。 在下窗格中，选择“Web 浏览器”选项卡。此时将显示 Web 服务返回的 XML 以及任何操作的结果。

   查找 Web 服务请求的结果。

## <a name="see-also"></a>请参阅

- [为负载测试创建自定义代码和插件](../test/create-custom-code-and-plug-ins-for-load-tests.md)
