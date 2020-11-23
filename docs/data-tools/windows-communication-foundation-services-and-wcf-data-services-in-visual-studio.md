---
title: Windows Communication Foundation 和 WCF Data Services
description: 在 Visual Studio 中探索 Windows Communication Foundation (WCF) 服务和 WCF Data Services，这样就可以创建分布式应用程序了。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- services, WCF Data
- WCF services, binding to
- WCF services, asynchronous service methods
- service references [Visual Studio]
- WCF Data Services
- asynchronous calls
- service references [Visual Studio], type sharing
- endpoints [WCF]
- asynchronous service methods
- service references [Visual Studio] endpoints
- WCF services, type sharing
- Windows Communication Foundation, in Visual Studio
- services, WCF
- WCF service, Visual Studio
- data services, WCF
- services, in Visual Studio
- data binding [Visual Studio], WCF
- service endpoints [Visual Studio]
- service references [Visual Studio], asynchronous calls
- services, Windows Communication Foundation
- type sharing in WCF services
- WCF services, endpoints
- service method, called asynchronously[Visual Studio]
ms.assetid: d56f12cb-e139-4fec-b3e4-488383356642
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 983ff598003a4f966b5173dc9ae78dd9aaa16580
ms.sourcegitcommit: 72a49c10a872ab45ec6c6d7c4ac7521be84526ff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "94997896"
---
# <a name="windows-communication-foundation-services-and-wcf-data-services-in-visual-studio"></a>Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务

Visual Studio 提供了很多工具，它们可与 Windows Communication Foundation (WCF) 和 WCF Data Services 这类用于创建分散式应用程序的 Microsoft 技术结合使用。 本主题从 Visual Studio 的角度来介绍这些服务。 有关完整文档，请参阅 [WCF Data Services 4.5](/dotnet/framework/data/wcf/index)。

## <a name="what-is-wcf"></a>什么是 WCF？

Windows Communication Foundation (WCF) 是一种统一框架，用于构建安全、可靠、可交易且可互操作的分散式应用程序。 它取代了较旧的进程间通信技术，例如 ASMX Web 服务、.NET 远程处理、企业服务 (DCOM) 和 MSMQ。 WCF 将所有这些技术的功能汇集在一个统一的编程模型下。 这简化了开发分散式应用程序的体验。

### <a name="what-are-wcf-data-services"></a>什么是 WCF Data Services

WCF Data Services 是开放数据 (OData) 协议标准的实现。  通过 WCF Data Services，可以一组 REST API 的形式公开表格数据，从而能够使用标准 HTTP 谓词（如 GET、POST、PUT 或 DELETE）返回数据。 在服务器端，[ASP.NET Web API](https://dotnet.microsoft.com/apps/aspnet/apis) 取代了 WCF Data Services 来创建新的 OData 服务。 对于在 Visual Studio 的 .NET 应用程序中使用 OData 服务（访问“项目” > “添加服务引用”）而言，WCF Data Services 客户端库仍然是一个不错的选择 。 有关详细信息，请参阅 [WCF Data Services 4.5](/dotnet/framework/data/wcf)。

### <a name="wcf-programming-model"></a>WCF 编程模型

WCF 编程模型基于 WCF 服务和 WCF 客户端这两个实体之间的通信。 编程模型封装在 .NET 中的 <xref:System.ServiceModel> 命名空间中。

### <a name="wcf-service"></a>WCF 服务

WCF 服务基于在服务与客户端之间定义协定的接口。 它标记有 <xref:System.ServiceModel.ServiceContractAttribute> 特性，如以下代码所示：

[!code-csharp[WCFWalkthrough#6](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_1.cs)]
[!code-vb[WCFWalkthrough#6](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_1.vb)]

通过使用 <xref:System.ServiceModel.OperationContractAttribute> 特性来标记 WCF 服务公开的函数或方法，对它们进行定义。

[!code-csharp[WCFWalkthrough#1](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_2.cs)]
[!code-vb[WCFWalkthrough#1](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_2.vb)]

此外，还可使用 <xref:System.Runtime.Serialization.DataContractAttribute> 特性标记复合类型来公开序列化的数据。 这会在客户端中启用数据绑定。

定义接口及其方法后，将它们封装在实现该接口的类中。 单个 WCF 服务类可实现多个服务协定。

WCF 服务通过终结点公开以供使用。 终结点提供了与服务通信的唯一方法；你不能像访问其他类那样通过直接引用访问该服务。

终结点由地址、绑定和协定组成。 该地址定义了服务所在的位置；它可能是 URL、FTP 地址，也可能是网络或本地路径。 绑定定义了你与服务通信的方式。 WCF 绑定提供了一个通用模型，它用于指定协议（如 HTTP 或 FTP）和安全机制（例如 Windows 身份验证或用户名加密码）等等。 协定包括 WCF 服务类公开的操作。

可公开多个终结点供一个 WCF 服务使用。 这样，不同的客户端可通过不同的方式与同一服务进行通信。 例如，银行服务可能为员工提供一个终结点，为外部客户提供不同的终结点，而每种终结点使用不同的地址、绑定和/或协定。

### <a name="wcf-client"></a>WCF client（WCF 客户端）

WCF 客户端包含一个代理和一个终结点，前者使应用程序能够与 WCF 服务进行通信，后者与为该服务定义的终结点相匹配。 代理是在客户端上的 app.config 文件中生成的，它包含服务公开的类型和方法的相关信息。 对于公开多个终结点的服务，客户端可选择最适合其需求的服务，例如通过 HTTP 进行通信并使用 Windows 身份验证。

创建 WCF 客户端后，就可像引用其他任何对象一样在代码中引用该服务。 例如，若要调用之前所示的 `GetData` 方法，需编写如下所示的代码：

[!code-csharp[WCFWalkthrough#3](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_3.cs)]
[!code-vb[WCFWalkthrough#3](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_3.vb)]

## <a name="wcf-tools-in-visual-studio"></a>Visual Studio 中的 WCF 工具

Visual Studio 提供了工具来帮助创建 WCF 服务和 WCF 客户端。 有关工具演练，请参阅[演练：在 Windows 窗体中创建简单的 WCF 服务](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md)。

### <a name="create-and-test-wcf-services"></a>创建和测试 WCF 服务

可以 WCF Visual Studio 模板为基础来快速创建自己的服务。 然后，可使用 WCF 服务自动主机和 WCF 测试客户端来调试和测试服务。 这些工具共同作用，可让你快速方便地完成调试和测试，无需在早期阶段提交给承载模型。

#### <a name="wcf-templates"></a>WCF 模板

WCF Visual Studio 模板为服务开发提供基本的类结构。 “添加新项目”对话框中提供了若干 WCF 模板。 其中包括 WCF 服务 lLibrary 项目、WCF 服务网站和 WCF 服务项模板。

选择模板时，会为服务协定、服务实现和服务配置添加文件。 所有必需的属性都已添加，这会创建一个简单的“Hello World”类型的服务，你无需编写任何代码。 当然，你需要添加代码来为你的实际服务提供函数和方法，但这些模板提供了基础。

若要详细了解 WCF 模板，请参阅 [WCF Visual Studio 模板](/dotnet/framework/wcf/wcf-vs-templates)。

#### <a name="wcf-service-host"></a>WCF 服务主机

（通过按 F5）为 WCF 服务项目启动 Visual Studio 调试程序时，WCF 服务主机工具会自动启动，在本地托管服务。 WCF 服务主机会枚举 WCF 服务项目中的服务、加载项目的配置并针对它找到的每个服务对主机进行实例化。

通过使用 WCF 服务主机，无需在开发期间额外编写代码或提交到特定主机即可测试 WCF 服务。

若要详细了解 WCF 服务主机，请参阅 [WCF 服务主机 (WcfSvcHost.exe)](/dotnet/framework/wcf/wcf-service-host-wcfsvchost-exe)。

#### <a name="wcf-test-client"></a>WCF 测试客户端

借助 WCF 测试客户端，可输入测试参数、将该输入提交给 WCF 服务并查看服务发回的响应。 在将其与 WCF 服务主机组合使用时，它将提供便捷的服务测试体验。 在 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE 文件夹中找到该工具。

按 F5 调试 WCF 服务项目时，WCF 测试客户端会打开，并显示在配置文件中定义的服务终结点的列表。 可测试参数和启动服务，并重复此过程以继续测试和验证服务。

要详细了解 WCF 测试客户端，请参阅 [WCF 测试客户端 (WcfTestClient.exe)](/dotnet/framework/wcf/wcf-test-client-wcftestclient-exe)。

### <a name="accessing-wcf-services-in-visual-studio"></a>在 Visual Studio 中访问 WCF 服务

Visual Studio 简化了 WCF 客户端创建任务，它为你通过“添加服务引用”对话框添加的服务自动生成一个代理和一个终结点。 所有必需的配置信息都将添加到 app.config 文件中。 大多数时候，你只需实例化服务即可使用。

通过“添加服务引用”对话框，可输入服务的地址或搜索在解决方案中定义的服务。 此对话框会一个列表，其中有服务及其提供的操作。 你还可用它来定义命名空间；你将在代码中通过该命名空间引用这些服务。

使用“配置服务引用”对话框可自定义服务的配置。 可更改服务的地址，指定访问级别、异步行为和消息协定类型，还可配置类型重用。

## <a name="how-to-select-a-service-endpoint"></a>如何：选择服务终结点

一些 Windows Communication Foundation (WCF) 服务会公开多个终结点，客户端可通过这些终结点与服务进行通信。 例如，某项服务可能会公开一个终结点来使用 HTTP 绑定和用户名加密码安全性，再公开一个终结点来使用 FTP 和 Windows 身份验证。 从防火墙外部访问该服务的应用程序可能会使用第一个终结点，而第二个终结点可能会在 Intranet 上使用。

这样的话，可将 `endpointConfigurationName` 指定为服务引用的构造函数的参数。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-select-a-service-endpoint"></a>选择服务终结点

1. 通过在解决方案资源管理器中右键单击项目节点，然后选择“添加服务引用”，添加对 WCF 服务的引用 。

2. 在代码编辑器中，为服务引用添加构造函数：

    ```vb
    Dim proxy As New ServiceReference.Service1Client(
    ```

    ```csharp
    ServiceReference.Service1Client proxy = new ServiceReference.Service1Client(
    ```

    > [!NOTE]
    > 将 ServiceReference 替换为服务引用的命名空间，将 Service1Client 替换为服务的名称 。

3. 将显示一个 IntelliSense 列表，其中包含构造函数的重载。 选择 `endpointConfigurationName As String` 重载。

4. 重载后，键入 `=` ConfigurationName，其中 ConfigurationName 是要使用的终结点的名称 。

    > [!NOTE]
    > 如果你不知道可用的终结点的名称，可在 app.config 文件中找到它们。

### <a name="to-find-the-available-endpoints-for-a-wcf-service"></a>查找 WCF 服务的可用终结点

1. 在解决方案资源管理器中，右键单击包含服务引用的项目的 app.config 文件，然后单击“打开”  。 文件将显示在代码编辑器中。

2. 在文件中搜索 `<Client>` 标记。

3. 在 `<Client>` 标记下搜索以 `<Endpoint>` 开头的标记。

     如果服务引用提供多个终结点，则将有两个或多个 `<Endpoint` 标记。

4. 在 `<EndPoint>` 标记中，会找到一个 `name="`SomeService`"` 参数（其中 SomeService 表示终结点名称） 。 这是终结点的名称，可将其传递给服务引用的构造函数的 `endpointConfigurationName As String` 重载。

## <a name="how-to-call-a-service-method-asynchronously"></a>如何：异步调用服务方法

Windows Communication Foundation (WCF) 服务中的大多数方法都可同步或异步调用。 通过异步调用方法，可使应用程序在通过慢速连接操作时在调用方法时继续工作。

默认情况下，将服务引用添加到项目时，会将其配置为同步调用方法。 可更改“配置服务引用”对话框中的设置，将此行为更改为异步调用方法。

> [!NOTE]
> 此选项是按每个服务进行设置的。 如果异步调用服务的一种方法，则必须异步调用所有方法。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-call-a-service-method-asynchronously"></a>异步调用服务方法

1. 在解决方案资源管理器中，选择服务引用。

2. 在“项目”菜单中，单击“配置服务引用” 。

3. 在“配置服务引用”对话框中，选择“生成异步操作”复选框 。

## <a name="how-to-bind-data-returned-by-a-service"></a>如何：绑定服务返回的数据

可将 Windows Communication Foundation (WCF) 服务返回的数据绑定到控件，就像可将任何其他数据源绑定到控件一样。 添加对 WCF 服务的引用时，如果该服务包含返回数据的复合类型，则它们将自动添加到“数据源”窗口中。

### <a name="to-bind-a-control-to-single-data-field-returned-by-a-wcf-service"></a>将控件绑定到 WCF 服务返回的单个数据字段

1. 在 **“数据”** 菜单上，单击 **“显示数据源”**。

   随即出现“数据源”窗口。

2. 在“数据源”窗口中，展开服务引用的节点。 这会显示服务返回的所有复合类型。

3. 展开某个类型的节点。 这会显示该类型的数据字段。

4. 选择一个字段并单击下拉箭头，显示可用于该数据类型的控件的列表。

5. 单击要绑定到的控件的类型。

6. 将字段拖到窗体上。 该控件会与一个 <xref:System.Windows.Forms.BindingSource> 组件和一个 <xref:System.Windows.Forms.BindingNavigator> 组件一起添加到窗体中。

7. 对于要绑定的其他任何字段，请重复步骤 4 到 6。

### <a name="to-bind-a-control-to-composite-type-returned-by-a-wcf-service"></a>将控件绑定到 WCF 服务返回的复合类型

1. 在“数据”菜单上，选择“显示数据源” 。 随即出现“数据源”窗口。

2. 在“数据源”窗口中，展开服务引用的节点。 这会显示服务返回的所有复合类型。

3. 选择某个类型的节点并单击下拉箭头，显示可用选项的列表。

4. 单击“DataGridView”以在网格中显示数据，或单击“详细信息”以显示单个控件中的数据 。

5. 将节点拖到窗体上。 该控件会与一个 <xref:System.Windows.Forms.BindingSource> 组件和一个 <xref:System.Windows.Forms.BindingNavigator> 组件一起添加到窗体。

## <a name="how-to-configure-a-service-to-reuse-existing-types"></a>如何：将服务配置为重复使用现有类型

将服务引用添加到项目中时，会在本地项目中生成服务中定义的任何类型。 在许多情况下，当服务使用常见的 .NET 类型或在共享库中定义类型时，这会创建重复的类型。

为避免此问题，会默认共享引用的程序集中的类型。 如果要禁用一个或多个程序集的类型共享，可在“配置服务引用”对话框中进行操作。

### <a name="to-disable-type-sharing-in-a-single-assembly"></a>在单个程序集中禁用类型共享

1. 在解决方案资源管理器中，选择服务引用。

2. 在“项目”菜单中，单击“配置服务引用” 。

3. 在“配置服务引用”对话框中，选择“重新使用指定的引用程序集中的类型” 。

4. 选中要在其中启用类型共享的每个程序集的复选框。 若要禁用某程序集的类型共享，请将其复选框保留在未选中状态。

### <a name="to-disable-type-sharing-in-all-assemblies"></a>禁用所有程序集中的类型共享

1. 在解决方案资源管理器中，选择服务引用。

2. 在“项目”菜单中，单击“配置服务引用” 。

3. 在“配置服务引用”对话框中，清除“重新使用引用的程序集中的类型”复选框 。

## <a name="related-topics"></a>相关主题

| Title | 说明 |
| - | - |
| [演练：在 Windows 窗体中创建简单的 WCF 服务](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md) | 提供在 Visual Studio 中创建和使用 WCF 服务的分步演示。 |
| [演练：通过 WPF 和实体框架创建 WCF 数据服务](../data-tools/walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework.md) | 提供有关如何在 Visual Studio 中创建和使用 WCF Data Services 的分步演示。 |
| [使用 WCF 开发工具](/dotnet/framework/wcf/using-the-wcf-development-tools) | 介绍如何在 Visual Studio 中创建和测试 WCF 服务。 |
| | [如何：添加、更新或删除 WCF 数据服务引用](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md) |
| [服务引用疑难解答](../data-tools/troubleshooting-service-references.md) | 介绍服务引用可能发生的一些常见错误及其预防方式。 |
| [调试 WCF 服务](../debugger/debugging-wcf-services.md) | 描述在调试 WCF 服务时可能会遇到的常见调试问题和技术。 |
| [演练：创建 n 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md) | 提供有关创建类型化数据集并将 TableAdapter 和数据集代码分离到多个项目中的分步说明。 |
| [“配置服务引用”对话框](../data-tools/configure-service-reference-dialog-box.md) | 介绍“配置服务引用”对话框的用户界面元素。 |

## <a name="reference"></a>参考

- <xref:System.ServiceModel>
- <xref:System.Data.Services>

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
