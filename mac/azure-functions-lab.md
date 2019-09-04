---
title: 教程：Azure Functions
description: 在 Visual Studio for Mac 中使用 Azure Functions。
author: sayedihashimi
ms.author: sayedha
ms.date: 05/06/2018
ms.technology: vs-ide-install
ms.assetid: 38FD2070-5151-482E-B0A9-993715128736
ms.openlocfilehash: 6bea12b37bc7fe1f608c27cd72e48c7cdc7e13d8
ms.sourcegitcommit: cf8c0fef2b9690595e99ce3802586cdd55fd37c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70108144"
---
# <a name="tutorial-getting-started-with-azure-functions"></a>教程：Azure Functions 入门

在本实验室中，了解如何使用 Visual Studio for Mac 开始生成 Azure Functions。 还将与 Azure 存储表集成，该存储表表示可供 Azure Functions 开发人员使用的众多绑定和触发器之一。

## <a name="objectives"></a>目标

> [!div class="checklist"]
> * 创建和调试本地 Azure Functions
> * 与 Web 和 Azure 存储资源集成
> * 安排涉及多个 Azure Functions 的工作流

## <a name="requirements"></a>要求

- Visual Studio for Mac 7.5 或更高版本。
- Azure 订阅（[https://azure.com/free](https://azure.com/free) 中免费提供）。

## <a name="exercise-1-creating-an-azure-functions-project"></a>练习 1：创建 Azure Functions 项目

1. 启动“Visual Studio for Mac”  。

2. 选择“文件”>“新建解决方案”  。

3. 从“云”>“常规”  类别中，选择“Azure Functions”  模板。 使用 C# 创建托管 Azure Functions 的 .NET 类库。 单击 **“下一步”** 。

    ![Azure Functions 模板选择](media/azure-functions-lab-image1.png)

4. 将“项目名称”  设置为“AzureFunctionsLab”  ，单击“创建”  。

    ![命名和创建 Azure Function 项目](media/azure-functions-lab-image2.png)

5. 展开“Solution Pad”  中的节点。 默认项目模板包括对各种 Azure WebJobs 包以及 Newtonsoft.Json 包的 NuGet 引用。

     此外还有三个文件：- 用于描述主机的全局配置选项的 host.json **和**用于配置服务设置的 local.settings.json  。
        - 项目模板还会创建一个默认 HttpTrigger。 对于本实验室，应从项目中删除 HttpTrigger.cs  文件。

    打开 local.settings.json  。 它默认具有两个空的连接字符串设置。

    ![显示 local.settings.json 文件的 solution pad](media/azure-functions-lab-image3.png)

## <a name="exercise-2-creating-an-azure-storage-account"></a>练习 2：创建 Azure 存储帐户

1. 在 [https://portal.azure.com](https://portal.azure.com) 登录到 Azure 帐户。

1. 在屏幕左侧的“收藏夹”  部分下，选择“存储帐户”  ：

    ![Azure 门户中显示存储帐户项的收藏夹部分](media/azure-functions-lab-image4.png)

1. 选择“添加”  ，创建新的存储帐户：

    ![添加新存储帐户的按钮](media/azure-functions-lab-image5.png)

1. 在“名称”  中输入全局唯一名称，然后在“资源组”  中再次使用该名称。 可将其他所有项保留为其默认值。

    ![新存储帐户的详细信息](media/azure-functions-lab-image6.png)

1. 单击 **“创建”** 。 创建存储帐户可能需要几分钟的时间。 成功创建后，你将收到一条通知。

    ![部署成功通知](media/azure-functions-lab-image7.png)

1. 选择通知中的“转到资源”  按钮。

1. 选择“访问密钥”  选项卡。

    ![访问密钥设置](media/azure-functions-lab-image8.png)

1. 复制第一个连接字符串  。 之后使用此字符串将 Azure 存储与 Azure Functions 集成。

    ![密钥 1 的信息](media/azure-functions-lab-image9.png)

1. 返回 Visual Studio for Mac  ，将完整的连接字符串粘贴在 local.settings.json  中作为 AzureWebJobsStorage  设置。 现在便可在需访问其资源的函数的特性中引用该设置的名称。

    ![含有输入的连接密钥的本地设置文件](media/azure-functions-lab-image10.png)

## <a name="example-3-creating-and-debugging-an-azure-function"></a>示例 3：创建和调试 Azure 函数

1. 现在可以开始添加一些代码。 使用 .NET 类库时，Azure Functions 将作为静态方法进行添加。 在“Solution Pad”中，右键单击“AzureFunctions”项目节点，选择“添加”>“添加函数”    ：

    ![“添加函数”选项](media/azure-functions-lab-image11.png)

1. 在“新建 Azure Functions”对话框中，选择常规 Webhook 模板。 将“名称”  设置为“Add”  ，单击“确定”  创建函数：

    ![“新建 Azure Functions”对话框](media/azure-functions-lab-image12.png)

1. 在新文件的顶部，添加以下 using  指令：

    ```csharp
    using Microsoft.Azure.WebJobs.Extensions.Http;
    using System.Web;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. 删除现有 `Run` 方法，并将以下方法添加到类中作为 Azure Function：

    ```csharp
    [FunctionName("Add")]
    public static int Run(
    [HttpTrigger(AuthorizationLevel.Function, "get", Route = null)]
    HttpRequestMessage req,
    TraceWriter log)
    {
        int x = 1;
        int y = 2;

        return x + y;
    }
    ```

1. 让我们逐部分地了解此方法。

    首先看到的是将此方法标记为 Azure Function 的 FunctionName  特性。 该特性指定函数的公共名称。 特性名称无需与实际方法名称匹配。

    ![FunctionName 特性突出显示的新 Run 方法](media/azure-functions-lab-image13.png)

1. 接下来，需将该方法标记为“公共静态”  方法。 你还会发现，返回值为 int  。除非另行指定 using 方法特性，否则 Azure Function 的任何非无效返回值将以文本形式返回到客户端。 默认情况下，它以 XML  形式返回，但可将其更改为 JSON  （之后将在本实验室中执行此操作）。

    ![方法初始化突出显示的新 Run 方法](media/azure-functions-lab-image14.png)

1. 第一个参数将使用 HttpTrigger  特性进行标记，该特性表示此方法由 HTTP 请求调用。 该特性还指定该方法的授权级别，以及它支持的谓词（此情况下只有“GET”  ）。 也可以选择定义一个“Route”  来替代该方法的路径，并提供一个方法以自动从路径中提取变量。 由于此处“Route”  为 null，所以此方法的路径将默认为 /api/Add  。

    ![参数突出显示的新 Run 方法](media/azure-functions-lab-image15.png)

1. 该方法的最后一个参数是 TraceWriter  ，可使用它记录诊断和错误的消息。

    ![TraceWriter 突出显示的新 Run 方法](media/azure-functions-lab-image16.png)

1. 单击该方法的 return 行的边距，在该行设置一个断点  ：

    ![已在 return 行设置断点](media/azure-functions-lab-image17.png)

1. 按 F5  或选择“运行”>“启动调试”  ，生成并运行调试会话中的项目。 或者，可以单击“运行”  按钮。 所有这些选项都执行相同任务。 此实验室的其余部分引用 F5  ，但可以使用你喜欢的方法。

    ![生成并运行项目](media/azure-functions-lab-image18.png)

1. 运行项目将自动打开终端应用程序。

1. 该项目将根据方法特性和本文稍后将介绍的文件约定经历整个检测 Azure Functions 流程。 在这种情况下，它会检测到一个 Azure Function 并“生成”1 个作业函数。

    ![终端中 Azure Functions 的输出](media/azure-functions-lab-image19.png)

1. 在启动消息的底部，Azure Functions 主机将打印任何 HTTP 触发器 API 的 URL。 应该只有一个。 复制该 URL 并将其粘贴在新的浏览器选项卡中。

    ![Azure Function API URL](media/azure-functions-lab-image20.png)

1. 应立即触发该断点。 已将 Web 请求路由到该函数，现在可以调试该请求。 将鼠标移动到 x  变量上，查看其值。

    ![已触发断点](media/azure-functions-lab-image21.png)

1. 可采用之前添加该断点的方法来删除它（单击边距或选择该行，然后按 F9  ）。

1. 按 F5 继续运行  。

1. 浏览器中将呈现该方法的 XML 结果。 正如预期一样，硬编码加法运算生成了一个合理的总和。 注意，如果只在 Safari 中看到“3”，请转到“Safari”>“首选项”>“高级”  ，勾选“在菜单栏中显示‘开发’菜单”  复选框，再重新加载页面。

1. 在“Visual Studio for Mac”中  ，单击“停止”  按钮，结束调试会话。 若要确保获得新的更改，请记住重启（先停止，然后运行）调试会话。

    ![“停止调试”选项](media/azure-functions-lab-image22.png)

1. 在 Run  方法中，将 x  和 y  定义替换替换为以下代码。 此代码从 URL 的查询字符串中提取值，以便可以根据提供的参数动态执行添加操作。

    ```csharp
    var query = HttpUtility.ParseQueryString(req.RequestUri.Query);

    int x = int.Parse(query["x"]);

    int y = int.Parse(query["y"]);

    return x + y;
    ```

1. 运行该应用程序。

1. 返回到浏览器窗口，将字符串 `/?x=2&y=3` 追加到 URL。 整个 URL 现在应为 `http://localhost:7071/api/Add?x=2&y=3`。 导航到新的 URL。

1. 此时的结果应反映新的参数。 可使用不同的值运行该项目。 注意，由于未进行任何错误检查，因此无效的或缺少的参数将引发错误。

1. 停止调试会话。

## <a name="exercise-4-working-with-functionjson"></a>练习 4：使用 function.json

1. 在之前的练习中，提到了 Visual Studio for Mac 为库中定义的 Azure Function“生成了”一个作业函数。 这是因为 Azure Functions 实际上并未在运行时使用该方法特性，而使用的是编译时文件系统约定来配置 Azure Functions 可供使用的位置及方式。 在“Solution Pad”  中，右键单击项目节点并选择“在查找器中展现”  。

     ![“在查找器中展现”菜单选项](media/azure-functions-lab-image23.png)

1. 向下导航文件系统，直至到达 bin/Debug/netstandard2.0  。 此处应该有一个名为“Add”  的文件夹。 创建此文件夹以与 C# 代码中的函数名称特性对应。 展开 Add 文件夹，会显示一个 function.json  文件。 此文件由运行时使用，用来托管和管理该 Azure Function。 对于其他不支持编译时的语言模型（如 C# 脚本或 JavaScript），必须手动创建和维护这些文件夹。 对于 C# 开发人员，这些文件夹会在构建时自动从特性元数据生成。 右键单击 function.json  ，选择在 Visual Studio 中打开它。

    ![文件目录中的 function.json](media/azure-functions-lab-image24.png)

1. 基于本教程的前几个步骤，你应该对 C# 特性已经有了基本的了解。 鉴于此，此 JSON 应该看起来很熟悉。 但是，还有几个之前的练习中未介绍的项目。 例如，每个 binding  必须设置其 direction  。 正如你所推测的一样，“in”  指示输入参数，而“out”  指示参数是一个返回值（通过 $return  ）或者是该方法的“out”  参数。 此外，还需在程序集内指定 scriptFile  （相对于此最终位置）和 entryPoint  方法（公共和静态）。 在接下来的几个步骤中，使用此模型添加一个自定义函数路径，以便将此文件的内容复制到剪贴板。

    ![visual studio for mac 中打开的 function.json 文件](media/azure-functions-lab-image25.png)

1. 在“Solution Pad”  中，右键单击 AzureFunctionsLab  项目节点，选择“添加”>“新建文件夹”  。 将新文件夹命名为 Adder  。 按照默认约定，此文件夹的名称将定义 API 的路径，例如 api/Adder  。

    ![“新建文件夹”选项](media/azure-functions-lab-image26.png)

1. 右键单击 Adder  文件夹，选择“添加”>“新建文件”  。

    ![“新建文件”选项](media/azure-functions-lab-image27.png)

1. 选择“Web”  类别和“空 JSON 文件”  模板。 将“名称”  设置为“function”  ，单击“新建”  。

    ![“空 json 文件”选项](media/azure-functions-lab-image28.png)

1. 粘贴另一个 function.json  （步骤 3 中）的内容来替代新创建的文件的默认内容。

1. 从 json 文件的顶部删除以下行：

    ```json
    "configurationSource":"attributes",
    "generatedBy":"Microsoft.NET.Sdk.Functions-1.0.13",
    ```

1. 在第一个绑定的末尾（"name": "req"  行之后），添加以下属性。 请记住在上一行中加上一个逗号。 此属性将替代默认根，这样它现在便可从该路径提取 int  参数，并将它们置于名为 x  和 y  的方法参数中。

    ```json
    "direction": "in",
    "route": "Adder/{x:int?}/{y:int?}"
    ```

1. 在第一个绑定下添加另一个绑定。 此绑定处理函数的返回值。 请记住在上一行中加上一个逗号：

    ```json
    {
    "name": "$return",
    "type": "http",
    "direction": "out"
    }
    ```

1. 此外，更新文件底部的 entryPoint  属性，以便使用名为“Add2”  的方法，如下所示。 这是为了说明可将路径 api/Adder...  映射至具有任意名称（此处为“Add2”  ）的适当方法。

    ```json
    "entryPoint": "<project-name>.<function-class-name>.Add2"
    ```

1. 最终的 function.json  文件应如以下 json 所示：

    ```json
    {
    "bindings": [
        {
        "type": "httpTrigger",
        "methods": [
            "get"
        ],
        "authLevel": "function",
        "direction": "in",
        "name": "req",
        "route": "Adder/{x:int?}/{y:int?}"
        },
        {
        "name": "$return",
        "type": "http",
        "direction": "out"
        }
    ],
    "disabled": false,
    "scriptFile": "../bin/AzureFunctionsProject.dll",
    "entryPoint": "AzureFunctionsProject.Add.Add2"
    }
    ```

1. 要使上述所有操作均发挥作用，所需的最后一步是指示 Visual Studio for Mac 在此文件每次更改时都将其复制到输出目录中的相同相对路径中。 选中该文件，从右侧菜单栏中选择“属性”选项卡，然后在“复制到输出目录”  中，选择“如果较新则复制”  ：

    ![Json 文件的“属性”选项](media/azure-functions-lab-image30.png)

1. 在 Add.cs 中  ，将 `Run` 方法（包括特性）替换为以下方法，实现预期的功能。 它与 `Run` 非常类似，只不过它不使用特性，并且对于 x  和 y  具有显式参数。

    ```csharp
    public static int Add2(
        HttpRequestMessage req,
        int x,
        int y,
        TraceWriter log)
    {
        return x + y;
    }
    ```

1. 按 F5  生成并运行项目。

1. 在构建完成并且平台运行时，它将指示为映射至新添加方法的请求提供了第二个路由：

    ![Http 函数的 URL](media/azure-functions-lab-image31.png)

1. 返回浏览器窗口并导航到 http://localhost:7071/api/Adder/3/5  。

1. 此时，该方法将再次运行，从该路径中拉取参数并生成一个总和。

1. 返回到 Visual Studio for Mac  ，并结束调试会话。

## <a name="exercise-5-working-with-azure-storage-tables"></a>练习 5：使用 Azure 存储表

通常，你生成的服务可能比我们目前为止已生成的服务更复杂，并且需要占用大量的时间和/或基础结构来执行。 在这种情况下，你可能会发现在 Azure Functions 提供支持的资源可用时，它在接受已排队等待处理的请求方面很有效。 在其他情况下，需集中存储数据。 通过 Azure 存储表，可以快速做到这一点。

1. 将以下类添加到 Add.cs  。 它应该位于命名空间内、现有类外。

    ```csharp
    public class TableRow : TableEntity
    {
        public int X { get; set; }
        public int Y { get; set; }
        public int Sum { get; set; }
    }
    ```

1. 在 Add  类中，添加以下代码以引入另一个函数。 注意，到目前为止，它是唯一的，因为它不涉及 HTTP 响应。 最后一行返回了新的 TableRow  ，其中填有可使其之后易于检索的一些关键信息（PartitionKey  和 RowKey  ），还返回了其参数和总和。 该方法内的代码还使用 TraceWriter  ，以便更轻松地了解函数何时运行。

    ```csharp
    [FunctionName("Process")]
    [return: Table("Results")]
    public static TableRow Process(
        [HttpTrigger(AuthorizationLevel.Function, "get",
            Route = "Process/{x:int}/{y:int}")]
        HttpRequestMessage req,
        int x,
        int y,
        TraceWriter log)
    {
        log.Info($"Processing {x} + {y}");

        return new TableRow()
        {
            PartitionKey = "sums",
            RowKey = $"{x}_{y}",
            X = x,
            Y = y,
            Sum = x + y
        };
    }
    ```

1. 按 F5  生成并运行项目。

1. 在浏览器选项卡中，导航到 http://localhost:7071/api/Process/4/6  。 这会将另一条消息置于队列中，最终将使另一行添加到表中。

1. 返回到“终端”  ，监视对“4 + 6”  的传入请求。

    ![显示添加请求的终端输出](media/azure-functions-lab-image32.png)

1. 返回到浏览器，刷新对相同 URL 的请求。 此时，将在 Process  方法后看到一个错误。 这是因为该代码尝试使用一个已存在的分区键和行键组合，向 Azure 表存储表添加一行。

    ```
    System.Private.CoreLib: Exception while executing function: Process. Microsoft.Azure.WebJobs.Host: Error while handling parameter $return after function returned:. Microsoft.Azure.WebJobs.Host: The specified entity already exists.
    ```

1. 结束调试会话。

1. 若要解决错误，立即将以下参数添加到 TraceWriter  参数前的方法定义。 此参数指示 Azure Functions 平台尝试从 PartitionKey  上的“Results”  表检索 TableRow  （我们一直将其用于存储结果）。 但是，一个突出的优点是，基于其他 **x** 和 **y** 参数，会为相同方法动态生成 **RowKey**。 如果该行已存在，则在该方法开始时，tableRow  即拥有此行，无需开发人员执行额外的工作。 如果该行不存在，则为 null。 这种高效使开发人员能够专注于重要的业务逻辑而非基础结构。

    ```csharp
    [Table("Results", "sums", "{x}_{y}")]
    TableRow tableRow,
    ```

1. 将以下代码添加到方法的开头。 如果 tableRow  不为 null，则我们已有要请求的操作的结果，并且可立即返回它。 否则，该函数将像以前那样继续运行。 虽然这可能不是返回数据的最可靠方式，但它表明可通过很少的代码跨多个可伸缩层安排非常复杂的操作。

    ```csharp
    if (tableRow != null)
    {
        log.Info($"{x} + {y} already exists");
        return null;
    }
    ```

1. 按 F5  生成并运行项目。

1. 在浏览器选项卡中，刷新 http://localhost:7071/api/Process/4/6  处的 URL。 由于此记录的表行已存在，因此它应立即返回且不能出错。 由于不存在任何 HTTP 输出，因此可在终端中查看输出。

    ![显示表行已存在的终端输出](media/azure-functions-lab-image33.png)

1. 更新该 URL 反映来尚未测试的组合，如 http://localhost:7071/api/Process/5/7  。 注意终端中的消息，它指示未（如预期）找到该表行。

    ![显示新进程的终端输出](media/azure-functions-lab-image34.png)

1. 返回到 Visual Studio for Mac  ，并结束调试会话。

<!--
1. Finally, let's take a look at what it's like to work with multiple input records. Rather than specify a specific **TableRow**, you can request an **IQueryable<TableRow>** using the same attributes, and the runtime will fill it with the appropriate resource you need. Add the code below to create a **List** function that lists all items that currently exist in the Azure table we've been working with. Also note that we're specifying that the MIME type of the response is **application/json**, so the runtime will automatically render as JSON.

    ```csharp
    [FunctionName("List")]
    public static HttpResponseMessage List(
        [HttpTrigger(AuthorizationLevel.Function, "get", Route = null)]
        HttpRequestMessage req,
        [Table("Results", "sums")]
        IQueryable<TableRow> table,
        TraceWriter log)
    {
        return req.CreateResponse(HttpStatusCode.OK, table, "application/json");
    }
    ```
1. Press **F5** to build and run the project.

1. In the browser tab, navigate to **http://localhost:7071/api/List**. This should pull down the list of all items in the Azure table and render it as JSON.

    ![](https://user-images.githubusercontent.com/3944468/29033725-be9d5a5e-7b4a-11e7-8b55-df0a200b6320.png)
-->

## <a name="summary"></a>总结

在本实验室中，你已了解如何使用 Visual Studio for Mac 开始生成 Azure Functions。
