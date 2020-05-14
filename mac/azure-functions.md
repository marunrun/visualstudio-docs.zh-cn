---
title: Azure Functions 简介
description: 在 Visual Studio for Mac 中使用 Azure Functions。
author: sayedihashimi
ms.author: sayedha
ms.date: 04/02/2019
ms.technology: vs-ide-install
ms.assetid: 25CD47A4-5B32-4734-8EF3-E24A02AABF29
ms.openlocfilehash: dac6a1c53cea8982a75c7b12661c98f2feb37f83
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "73189662"
---
# <a name="introduction-to-azure-functions"></a>Azure Functions 简介

Azure functions 是一种在云中创建和运行事件驱动的代码片段（函数）的方法，无需显式预配或管理基础结构。 有关 Azure Functions 的详细信息，请参阅 [Azure Functions 文档](/azure/azure-functions/)。

## <a name="requirements"></a>要求

Azure Function 工具包含在 Visual Studio for Mac 7.5 和更高版本中  。

若要创建和部署函数，还需要 Azure 订阅。 如果你没有 Azure 帐户，可以立即免费注册并接收 12 个月的免费热门服务、200 美元的免费额度和 25 个以上的永久免费服务 -> [https://azure.com/free](https://azure.com/free/dotnet)。

## <a name="creating-your-first-azure-functions-project"></a>创建第一个 Azure Functions 项目

1. 在 Visual Studio for Mac 中，选择“文件”>“新建解决方案”  。
2. 从“新建项目”对话框，选择“云”>“常规”下的 Azure Functions 模板并单击“下一步”   ：

    ![显示 Azure functions 选项的“新建项目”对话框](media/azure-functions-image1.png)

3. 选择要使用的初始 Azure Functions 模板，输入函数名称，然后单击“下一步”  。

    ![“新建项目”对话框显示 Azure Functions 模板](media/azure-functions-image2.png)

    > [!TIP]
    > 虽然已尽可能地将捆绑的 Azure Functions 运行时和模板 (CLI) 保持最新，但它们难免会过时。 创建新的 Functions 项目时，Visual Studio for Mac 将检查 CLI 的更新并发出通知，如下图所示。 只需单击按钮即可下载更新的模板。
    > ![显示 Azure Functions 更新可用的“新建项目”对话框](media/azure-functions-update.png)

    根据所选函数类型，下一页会提示输入详细信息，例如访问权限，如下图所示：

    ![“新建项目”对话框显示其他选项](media/azure-functions-image3.png)

    有关不同类型的 Azure Functions 模板以及配置每个模板所需的绑定属性的详细信息，请参阅[可用函数模板](#available-function-templates)部分。 在此示例中，使用了一个访问权限设置为匿名的 HTTP 触发器。

4. 设置参数后，选择项目的位置，然后单击“创建”  。

Visual Studio for Mac 使用包含的默认函数创建 .NET Standard 项目。 它还包括对各种 AzureWebJobs 包以及 Newtonsoft.Json 包的 NuGet 引用   。

![显示模板中的全新 Azure 函数的 Visual Studio for Mac 编辑器](media/azure-functions-newproj.png)

新项目包含以下文件：

* **your-function-name.cs** - 该类包含所选函数的 Boilerplate 代码。 其中包含一个带有函数名称的 FunctionName 属性和一个用于指定由什么来触发函数的触发器属性  （例如 HTTP 请求）。 有关函数方法的详细信息，请参阅 [Azure Functions C# 开发人员参考](/azure/azure-functions/functions-dotnet-class-library)一文。
* **host.json** - 该文件介绍 Functions 主机的全局配置选项。 有关示例文件和该文件的可用设置的信息，请参阅 [Azure Functions 的 host.json 引用](/azure/azure-functions/functions-host-json)。
* **local.settings.json** - 该文件包含用于在本地运行函数的所有设置。 这些设置由 Azure Functions 核心工具使用。 有关详细信息，请参阅“Azure Functions 核心工具”一文中的[本地设置文件](/azure/azure-functions/functions-run-local#local-settings-file)。

在 Visual Studio for Mac 中创建新的 Azure Functions 项目后，可以从本地计算机测试默认 HTTP 触发的函数。

## <a name="testing-the-function-locally"></a>在本地测试函数

使用 Visual Studio for Mac 中的 Azure Functions，可以在本地开发计算机上测试和调试函数。

1. 若要在本地测试函数，请按 Visual Studio for Mac 中的“运行”按钮  ：

    ![在 Visual Studio for Mac 中启动调试按钮](media/azure-functions-run.png)

1. 运行项目可启动 Azure Function 上的本地调试并打开一个新的终端窗口，如下图中所示：

    ![显示函数输出的终端窗口](media/azure-functions-terminal.png)

    从输出中复制 URL。

3. 将 HTTP 请求的 URL 粘贴到浏览器的地址栏。 将查询字符串 `?name=<yourname>` 添加到 URL 的末尾并执行请求。 下图显示了浏览器中由函数返回的本地 GET 请求的响应：

    ![浏览器中的 http 请求](media/azure-functions-httpreq.png)

## <a name="adding-another-function-to-your-project"></a>将另一个函数添加到项目中

函数模板使用户可以使用最常见的触发器和模板快速创建新函数。 若要创建另一种类型的函数，请执行以下操作：

1. 若要添加新函数，右键单击项目名称并选择“添加”>“添加函数...”  ：

    ![用于添加新函数的上下文操作](media/azure-functions-addnew.png)

2. 从“新建 Azure 函数”对话框选择所需的函数  ：

    ![“新建 Azure 函数”对话框](media/azure-functions-image4.png)

    [可用函数模板](#available-function-templates)部分提供 Azure 函数模板列表。

可使用上述过程向函数应用项目添加更多函数。 项目中的各函数可具有不同的触发器，但一个函数只能有一个触发器。 有关详细信息，请参阅 [Azure Functions 触发器和绑定概念](/azure/azure-functions/functions-triggers-bindings)。

## <a name="publish-to-azure"></a>发布到 Azure

1. 右键单击项目名，然后选择“发布”>“发布到 Azure”  ：![发布到 Azure 菜单选项](media/azure-functions-image5.png)
2. 如果已将 Azure 帐户连接到 Visual Studio for Mac，则会显示可用应用服务的列表。 如果尚未登录，系统将提示登录。
3. 从“发布到 Azure 应用服务”对话框，可选择现有应用服务，也可通过单击“新建”来创建新服务   。
4. 在“创建新的应用服务”对话框中，输入设置  ：![发布到 Azure 菜单选项](media/azure-functions-image7.png)

    |设置  |描述  |
    |---------|---------|
    |**应用服务名称**|用于标识新函数应用的全局唯一名称。|
    |**订阅**|要使用的 Azure 订阅。|
    |**[资源组](/azure/azure-resource-manager/resource-group-overview)**|要在其中创建函数应用的资源组的名称。 选择“+”以创建新的资源组  。|
    |**[服务计划](/azure/azure-functions/functions-scale)**|选择现有计划或创建自定义计划。 在附近的区域或函数访问的其他服务附近选择一个位置。|

5. 单击“下一步”创建存储帐户  。 Functions 运行时需要 Azure 存储帐户。 单击“自定义”以创建通用存储帐户，或使用现有帐户  ：

    ![发布到 Azure 菜单选项](media/azure-functions-image8.png)

6. 单击“创建”以使用这些设置在 Azure 中创建函数应用和相关资源，并部署函数项目代码  。

7. 在发布期间，系统可能会提示“在 Azure 上更新 Functions 版本”。 单击“是”  ：

    ![发布到 Azure 菜单选项](media/azure-functions-image12.png)

## <a name="function-app-settings"></a>函数应用设置

在 local.settings.json 中添加的任何设置也必须添加到 Azure 中的函数应用中。 发布项目时，不会自动上传这些设置。

若要访问应用设置，请转到 Azure 门户，网址为 [https://ms.portal.azure.com/](https://ms.portal.azure.com/)。 在“Function App”下，选择“函数应用”并突出显示函数名称   ：

![Azure Functions 菜单](media/azure-functions-image9.png)

在“概述”选项卡中，选择“配置的功能”下的“应用程序设置”    ：

![通过 Azure Functions 的选项卡](media/azure-functions-image10.png)

在此处，可为函数应用设置“应用程序设置”，可在其中添加新的应用程序设置或修改现有应用程序设置：

![Azure 门户的应用程序设置区域](media/azure-functions-image11.png)

可能需要设置的一个重要设置是 `FUNCTIONS_EXTENSION_VERSION`。 从 Visual Studio for Mac 发布时，此值应设置为“beta 版本”  。

## <a name="available-function-templates"></a>可用的函数模板

- **GitHub 触发器** - 对 GitHub 存储库中发生的事件作出响应。 有关详细信息，请参阅[关于 GitHub 的 Azure Functions 文章](/azure/azure-functions/functions-create-github-webhook-triggered-function)
  - GitHub 快速注释 - 此函数在其收到一个问题或拉取请求的 GitHub Webhook 时运行并添加注释。
  - GitHub WebHook - 此函数在其收到 GitHub Webhook 请求时运行。

- **HTTP** - 使用 HTTP 请求触发代码的执行。 可用于以下 HTTP 触发器的显式模板：
  - Http 触发器
  - Http GET CRUD
  - Http POST CRUD
  - 带有参数的 Http 触发器

- **计时器** - 按照预定义计划执行清除或其他批处理任务。 此模板采用两个字段：Name 和 schedule（一个具有 6 个字段的 CRON 表达式）。 有关详细信息，请参阅[关于时间的 Azure functions 文章](/azure/azure-functions/functions-create-scheduled-function)

- **队列触发器** - 这是在消息到达 Azure Storage 队列时会对消息进行响应的函数。 除函数名称之外，此模板还采用一个路径（将从中读取消息的队列名称）和存储帐户连接（包含存储帐户连接字符串的应用设置名称）   。 有关详细信息，请参阅[关于队列存储的 Azure functions 文章](/azure/azure-functions/functions-create-storage-queue-triggered-function)。

- **Blob 触发器** - 在 Azure 存储 Blob 添加到容器时对其进行处理。 除了函数名称，此模板还采用路径和连接属性。 路径属性是触发器将监视的存储帐户中的路径。 连接帐户是包含存储帐户连接字符串的应用设置的名称。 有关详细信息，请参阅 [Azure Functions Blob 存储](/azure/azure-functions/functions-create-storage-blob-triggered-function)一文。

- **泛型 WebHook** - 这是一个简单函数，每当从支持 Webhook 的任何服务接收请求时，都会运行此函数。 有关详细信息，请参阅[有关泛型 Webhook 的 Azure Functions 文章](/azure/azure-functions/functions-create-generic-webhook-triggered-function)。

- **Durable 函数业务流程** – Durable 函数可使用户在无服务器环境中编写有状态函数。 此扩展管理状态、检查点以及为用户重启。 有关详细信息，请参阅关于 [Durable 函数](/azure/azure-functions/durable-functions-overview)的 Azure Functions 指南。

- **图像大小调整工具** - 此函数在每次向容器添加 blob 时都会创建已调整大小的图像。 该模板针对触发器、小图像输出和中等图像输出使用路径和连接字符串。

- **SAS 令牌** - 此函数为给定 Azure 存储容器和 blob 名称生成 SAS 令牌。 除了函数名称，此模板还采用路径和连接属性。 路径属性是触发器将监视的存储帐户中的路径。 连接帐户是包含存储帐户连接字符串的应用设置的名称。 还需设置“访问权限”  。 授权级别控制函数是否需要 API 密钥以及要使用的密钥；函数使用功能键；管理员使用主密钥。 有关详细信息，请参阅[用于生成 SAS 令牌 的 C# Azure Function](https://github.com/Azure-Samples/functions-dotnet-sas-token/) 示例。
