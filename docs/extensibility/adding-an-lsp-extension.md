---
title: 添加语言服务器协议扩展 |微软文档
ms.date: 11/14/2017
ms.topic: conceptual
ms.assetid: 52f12785-1c51-4c2c-8228-c8e10316cd83
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ef2093915538f09f425fc961420c4a3078043c91
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740230"
---
# <a name="add-a-language-server-protocol-extension"></a>添加语言服务器协议扩展

语言服务器协议 （LSP） 是一种通用协议，其形式为 JSON RPC v2.0，用于向各种代码编辑器提供语言服务功能。 使用该协议，开发人员可以编写一个语言服务器，向支持 LSP 的各种代码编辑器提供语言服务功能，如 IntelliSense、错误诊断、查找所有引用等。 传统上，可以使用 TextMate 语法文件提供语法突出显示等基本功能，或者编写使用全套 Visual Studio 扩展 API 提供更丰富数据的自定义语言服务来添加 Visual Studio 中的语言服务。 借助 Visual Studio 对 LSP 的支持，有第三个选项。

![可视化工作室中的语言服务器协议服务](media/lsp-service-in-VS.png)

## <a name="language-server-protocol"></a>语言服务器协议

![语言服务器协议实现](media/lsp-implementation.png)

本文介绍如何创建使用基于 LSP 的语言服务器的 Visual Studio 扩展。 它假定您已经开发了基于 LSP 的语言服务器，并且只想将其集成到 Visual Studio 中。

为了在 Visual Studio 中提供支持，语言服务器可以通过任何基于流的传输机制与客户端（Visual Studio） 通信，例如：

* 标准输入/输出流
* Named pipes
* 套接字（仅限 TCP）

LSP 和 Visual Studio 中支持它的目的是将不属于 Visual Studio 产品的语言服务载入。 它不打算扩展视觉工作室中的现有语言服务（如 C#）。 要扩展现有语言，请参阅语言服务的扩展性指南（例如[，"Roslyn".NET 编译器平台](../extensibility/dotnet-compiler-platform-roslyn-extensibility.md)），或请参阅[扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)。

有关协议本身的详细信息，请参阅[此处](https://github.com/Microsoft/language-server-protocol)的文档。

有关如何创建示例语言服务器或如何将现有语言服务器集成到 Visual Studio Code 中的详细信息，请参阅[此处](https://code.visualstudio.com/docs/extensions/example-language-server)的文档。

## <a name="language-server-protocol-supported-features"></a>语言服务器协议支持功能

下表显示了可视化工作室中支持哪些 LSP 功能：

消息 | 在视觉工作室中提供支持
--- | ---
初始化 | 是
已初始化 | 是
shutdown | 是
exit | 是
$/取消请求 | 是
窗口/显示消息 | 是
窗口/显示消息请求 | 是
窗口/日志消息 | 是
遥测/事件 |
客户端/寄存器能力 |
客户端/取消注册功能 |
工作区/已更改配置 | 是
工作区/已更改监视文件 | 是
工作区/符号 | 是
工作区/执行命令 | 是
工作区/应用编辑 | 是
文本文档/发布诊断 | 是
文本文档/已打开 | 是
文本文档/已更改 | 是
文本文档/将保存 |
文本文档/将保存等待，直到 |
文本文档/已保存 | 是
文本文档/已关闭 | 是
文本文档/完成 | 是
完成/解决 | 是
文本文档/悬停 | 是
文本文档/签名帮助 | 是
文本文档/引用 | 是
文本文档/文档突出显示 | 是
文本文档/文档符号 | 是
文本文档/格式 | 是
文本文档/范围格式 | 是
文本文档/打开类型格式 |
文本文档/定义 | 是
文本文档/代码操作 | 是
文本文档/代码镜头 |
代码镜头/解析 |
文本文档/文档链接 |
文档链接/解析 |
文本文档/重命名 | 是

## <a name="get-started"></a>入门

> [!NOTE]
> 从 Visual Studio 2017 版本 15.8 开始，对通用语言服务器协议的支持内置于可视化工作室中。 如果您已使用预览[语言服务器客户端 VSIX](https://marketplace.visualstudio.com/items?itemName=vsext.LanguageServerClientPreview)版本构建 LSP 扩展，则升级至版本 15.8 或更高版本后，它们将停止工作。 您需要执行以下操作才能使 LSP 扩展再次工作：
>
> 1. 卸载微软可视化工作室语言服务器协议预览 VSIX。
>
>    从版本 15.8 开始，每次在 Visual Studio 中执行升级时，将自动检测并删除预览 VSIX。
>
> 2. 更新您的 Nuget 引用到[LSP 包](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)的最新非预览版本。
>
> 3. 删除 VSIX 清单中对 Microsoft 可视化工作室语言服务器协议预览 VSIX 的依赖项。
>
> 4. 确保 VSIX 指定 Visual Studio 2017 版本 15.8 预览 3 作为安装目标的下限。
>
> 5. 重新生成并重新部署。

### <a name="create-a-vsix-project"></a>创建 VSIX 项目

要使用基于 LSP 的语言服务器创建语言服务扩展，首先请确保为 VS 实例安装了**Visual Studio 扩展开发**工作负载。

接下来，通过导航到**文件** > **新项目** > **可视化 C_** > **扩展性** > VSIX 项目创建新的**VSIX 项目**：

![创建 vsix 项目](media/lsp-vsix-project.png)

### <a name="language-server-and-runtime-installation"></a>语言服务器和运行时安装

默认情况下，为支持 Visual Studio 中基于 LSP 的语言服务器而创建的扩展不包含语言服务器本身或执行它们所需的运行时。 扩展开发人员负责分发语言服务器和所需的运行时。 有几种方法可以做到这一点：

* 语言服务器可以作为内容文件嵌入到 VSIX 中。
* 创建 MSI 以安装语言服务器和/或所需的运行时。
* 在应用商店上提供说明，告知用户如何获取运行时和语言服务器。

### <a name="textmate-grammar-files"></a>文本Mate语法文件

LSP 不包括有关如何为语言提供文本着色的规范。 要为 Visual Studio 中的语言提供自定义着色，扩展开发人员可以使用 TextMate 语法文件。 要添加自定义 TextMate 语法或主题文件，请按照以下步骤操作：

1. 在扩展室内创建名为"语法"的文件夹（也可以是您选择的任何名称）。

2. 在*语法*文件夹中，包括任何*\*.tm 语言* * \*、.plist、.tmtheme**\** 或*\*.json*文件，您希望提供自定义着色。

   > [!TIP]
   > *.tmtheme*文件定义作用域如何映射到 Visual Studio 分类（命名颜色键）。 有关指导，您可以在 *%程序文件 （x86）%_Microsoft\\\<Visual Studio 版本>\\ \<SKU>_Common7_IDE_共同扩展\Microsoft_TextMate_starterkit_Themesg*目录中引用全局 *.tmtheme*文件。

3. 创建 *.pkgdef*文件并添加类似于此行：

    ```
    [$RootKey$\TextMate\Repositories]
    "MyLang"="$PackageFolder$\Grammars"
    ```

4. 右键单击文件并选择**属性**。 将 **"生成"** 操作**更改为内容**，并将**VSIX 属性中的"包含"** 更改为**true**。

完成上述步骤后，*语法*文件夹将作为名为"MyLang"的存储库源添加到包的安装目录中（"MyLang"只是消除歧义的名称，可以是任何唯一的字符串）。 此目录中的所有语法 *（.tm语言*文件）和主题文件 *（.tmtheme*文件）都作为潜在内容被拾起，它们取代了 TextMate 提供的内置语法。 如果语法文件的声明扩展名与正在打开的文件的扩展名匹配，TextMate 将介入。

## <a name="create-a-simple-language-client"></a>创建简单的语言客户端

### <a name="main-interface---ilanguageclient"></a>主接口 - [I语言客户端](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)

创建 VSIX 项目后，向项目添加以下 NuGet 包：

* [微软.VisualStudio.语言服务器.客户端](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)

> [!NOTE]
> 完成上述步骤后依赖 NuGet 包时，牛顿软.Json 和 StreamJsonRpc 包也添加到您的项目中。 **不要更新这些软件包，除非您确定这些新版本将安装在您的扩展目标 Visual Studio 版本上**。 程序集将不包含在 VSIX 中;因此，这些程序集将不包含在 VSIX 中。相反，它们将从可视化工作室安装目录中拾取。 如果引用的程序集版本较用户计算机上安装的程序集版本要大，则扩展将不起作用。

然后，您可以创建实现[I语言客户端](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)接口的新类，该接口是连接到基于 LSP 的语言服务器的语言客户端所需的主接口。

下面是一个示例：

```csharp
namespace MockLanguageExtension
{
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
        public string Name => "Bar Language Extension";

        public IEnumerable<string> ConfigurationSections => null;

        public object InitializationOptions => null;

        public IEnumerable<string> FilesToWatch => null;

        public event AsyncEventHandler<EventArgs> StartAsync;
        public event AsyncEventHandler<EventArgs> StopAsync;

        public async Task<Connection> ActivateAsync(CancellationToken token)
        {
            await Task.Yield();

            ProcessStartInfo info = new ProcessStartInfo();
            info.FileName = Path.Combine(Path.GetDirectoryName(Assembly.GetExecutingAssembly().Location), "Server", @"MockLanguageServer.exe");
            info.Arguments = "bar";
            info.RedirectStandardInput = true;
            info.RedirectStandardOutput = true;
            info.UseShellExecute = false;
            info.CreateNoWindow = true;

            Process process = new Process();
            process.StartInfo = info;

            if (process.Start())
            {
                return new Connection(process.StandardOutput.BaseStream, process.StandardInput.BaseStream);
            }

            return null;
        }

        public async Task OnLoadedAsync()
        {
            await StartAsync.InvokeAsync(this, EventArgs.Empty);
        }

        public Task OnServerInitializeFailedAsync(Exception e)
        {
            return Task.CompletedTask;
        }

        public Task OnServerInitializedAsync()
        {
            return Task.CompletedTask;
        }
    }
}
```

需要实现的主要方法是["上载Async"](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017)和["激活Async"。](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017) 当 Visual Studio 加载了扩展并准备好启动语言服务器时，将调用[OnLoadedAsync。](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017) 在此方法中，您可以立即调用[StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017)委托以发出语言服务器应启动的信号，或者可以执行其他逻辑并在以后调用[StartAsync。](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017) **要激活语言服务器，您必须在某个时间点调用 StartAsync。**

[ActivateAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017)是最终调用[StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017)委托调用的方法。 它包含启动语言服务器并建立与它连接的逻辑。 必须返回包含用于写入服务器和从服务器读取的流的连接对象。 此处引发的任何异常都通过 Visual Studio 中的信息栏消息捕获并显示给用户。

### <a name="activation"></a>激活

实现语言客户端类后，需要为其定义两个属性，以定义如何将其加载到 Visual Studio 并激活：

```csharp
  [Export(typeof(ILanguageClient))]
  [ContentType("bar")]
```

### <a name="mef"></a>MEF

Visual Studio 使用[MEF（](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md)托管扩展性框架）来管理其扩展点。 ["导出"](/dotnet/api/system.componentmodel.composition.exportattribute)属性指示 Visual Studio 应作为扩展点选取此类并在适当的时间加载。

要使用 MEF，还必须在 VSIX 清单中将 MEF 定义为资产。

打开 VSIX 清单设计器并导航到"**资产**"选项卡：

![添加 MEF 资产](media/lsp-add-asset.png)

单击 **"新建**"创建新资产：

![定义 MEF 资产](media/lsp-define-asset.png)

* **类型**： 微软.VisualStudio.Mef组件
* **源**： 当前解决方案中的项目
* **项目**： [您的项目]

### <a name="content-type-definition"></a>内容类型定义

目前，加载基于 LSP 的语言服务器扩展名的唯一方法是按文件内容类型。 也就是说，在定义语言客户端类（实现[I语言客户端](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)）时，您需要定义文件类型，这些文件在打开时将导致加载扩展名。 如果未打开与您的定义的内容类型匹配的文件，则不会加载扩展名。

这是通过定义一个或多个`ContentTypeDefinition`类来完成的：

```csharp
namespace MockLanguageExtension
{
    public class BarContentDefinition
    {
        [Export]
        [Name("bar")]
        [BaseDefinition(CodeRemoteContentDefinition.CodeRemoteContentTypeName)]
        internal static ContentTypeDefinition BarContentTypeDefinition;

        [Export]
        [FileExtension(".bar")]
        [ContentType("bar")]
        internal static FileExtensionToContentTypeDefinition BarFileExtensionDefinition;
    }
}
```

在前面的示例中，为以 *.bar*文件扩展名结尾的文件创建内容类型定义。 内容类型定义的名称为"bar"，必须派生自[代码远程内容类型名称](/dotnet/api/microsoft.visualstudio.languageserver.client.coderemotecontentdefinition.coderemotecontenttypename?view=visualstudiosdk-2017)。

添加内容类型定义后，可以定义何时在语言客户端类中加载语言客户端扩展：

```csharp
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
    }
```

添加对 LSP 语言服务器的支持不需要您在 Visual Studio 中实现自己的项目系统。 客户可以在 Visual Studio 中打开单个文件或文件夹，以开始使用您的语言服务。 事实上，对 LSP 语言服务器的支持设计仅在打开的文件夹/文件方案中工作。 如果实现了自定义项目系统，则某些功能（如设置）将不起作用。

## <a name="advanced-features"></a>高级功能

### <a name="settings"></a>设置

支持自定义语言服务器特定的设置，但仍处于改进过程中。 设置特定于语言服务器支持的内容，通常控制语言服务器如何发出数据。 例如，语言服务器可能具有报告的最大错误数设置。 扩展作者将定义一个默认值，用户可以更改特定项目。

按照以下步骤向 LSP 语言服务扩展添加对设置的支持：

1. 向包含设置及其默认值的项目添加 JSON 文件（例如 *，Mock语言扩展设置.json）。* 例如：

    ```json
    {
        "foo.maxNumberOfProblems": -1
    }
    ```

2. 右键单击 JSON 文件并选择**属性**。 将**生成**操作更改为"内容"，将"包含在 VSIX"属性更改为**true**。

3. 实现配置节并返回 JSON 文件中定义的设置的前缀列表（在可视化工作室代码中，这将映射到包.json 中的配置节名称）：

    ```csharp
    public IEnumerable<string> ConfigurationSections
    {
        get
        {
            yield return "foo";
        }
    }
    ```

4. 向项目添加 .pkgdef 文件（添加新文本文件并将文件扩展名更改为 .pkgdef）。 pkgdef 文件应包含此信息：

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\[settings-name]]
    @="$PackageFolder$\[settings-file-name].json"
    ```

    示例：

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\MockLanguageExtension]
    @="$PackageFolder$\MockLanguageExtensionSettings.json"
    ```

5. 右键单击 .pkgdef 文件并选择**属性**。 将 **"生成**"操作**更改为"内容**"，将**VSIX 属性中的"包含"** 更改为**true**。

6. 打开*source.扩展.vsix清单*文件，并在 **"资产**"选项卡中添加资产：

   ![编辑与包资产](media/lsp-add-vspackage-asset.png)

   * **类型**： 微软.VisualStudio.Vs包
   * **源**： 文件系统上的文件
   * **路径**： [对 *.pkgdef*文件的路径]

### <a name="user-editing-of-settings-for-a-workspace"></a>用户编辑工作区的设置

1. 用户打开一个工作区，其中包含服务器拥有的文件。
2. 用户在名为*VSWorkspaceSettings.json*的 *.vs*文件夹中添加一个文件。
3. 用户为服务器提供的设置向*VSWorkspaceSettings.json*文件添加一行。 例如：

    ```json
    {
        "foo.maxNumberOfProblems": 10
    }
    ```

### <a name="enable-diagnostics-tracing"></a>启用诊断跟踪

可以启用诊断跟踪以在客户端和服务器之间输出所有消息，这在调试问题时非常有用。 要启用诊断跟踪，可以执行以下操作：

1. 打开或创建工作区设置文件*VSWorkspaceSettings.json（* 请参阅"工作区设置的用户编辑"）。
2. 在设置 json 文件中添加以下行：

```json
{
    "foo.trace.server": "Off"
}
```

跟踪详细性有三个可能的值：

* "关闭"：完全关闭跟踪
* "消息"：已打开但仅跟踪方法名称和响应 ID。
* "详细"：已打开跟踪;跟踪整个 rpc 消息。

启用跟踪后，内容将写入 *%temp%_VisualStudio_LSP*目录中的文件。 日志遵循命名格式 *[语言客户端名称] -[日期时间戳]日志*。 目前，只能为打开的文件夹方案启用跟踪。 打开单个文件以激活语言服务器没有诊断跟踪支持。

### <a name="custom-messages"></a>自定义消息

有 API 用于方便将消息传递到非标准语言服务器协议一部分的语言服务器和接收消息。 要处理自定义消息，请在语言客户端类中实现[I语言客户端消息接口](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)。 [VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md)库用于在语言客户端和语言服务器之间传输自定义消息。 由于 LSP 语言客户端扩展与任何其他 Visual Studio 扩展类似，因此您可以通过自定义消息决定在扩展中向 Visual Studio（使用其他 Visual Studio API）添加其他功能（LSP 不支持）。

#### <a name="receive-custom-messages"></a>接收自定义消息

要从语言服务器接收自定义消息，请在[I语言ClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)上实现[自定义MessageTarget](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.custommessagetarget?view=visualstudiosdk-2017)属性，并返回知道如何处理自定义邮件的对象。 以下示例：

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public object CustomMessageTarget
    {
        get;
        set;
    }

    public class CustomTarget
    {
        public void OnCustomNotification(JToken arg)
        {
            // Provide logic on what happens OnCustomNotification is called from the language server
        }

        public string OnCustomRequest(string test)
        {
            // Provide logic on what happens OnCustomRequest is called from the language server
        }
    }
}
```

#### <a name="send-custom-messages"></a>发送自定义消息

要向语言服务器发送自定义消息，请在[I语言客户端自定义消息](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)上实现[附加ForCustomMessageAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.attachforcustommessageasync?view=visualstudiosdk-2017)方法。 当您的语言服务器启动并准备接收消息时，将调用此方法。 [JsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/src/StreamJsonRpc/JsonRpc.cs)对象作为参数传递，然后您可以保留该参数，使用[VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) API 将消息发送到语言服务器。 以下示例：

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public async Task AttachForCustomMessageAsync(JsonRpc rpc)
    {
        await Task.Yield();

        this.customMessageRpc = rpc;
    }

    public async Task SendServerCustomNotification(object arg)
    {
        await this.customMessageRpc.NotifyWithParameterObjectAsync("OnCustomNotification", arg);
    }

    public async Task<string> SendServerCustomMessage(string test)
    {
        return await this.customMessageRpc.InvokeAsync<string>("OnCustomRequest", test);
    }
}
```

### <a name="middle-layer"></a>中间层

有时，扩展开发人员可能想要拦截发送到语言服务器并从语言服务器接收的 LSP 消息。 例如，扩展开发人员可能希望更改为特定 LSP 消息发送的消息参数，或修改从语言服务器返回的 LSP 功能的结果（例如完成）。 必要时，扩展开发人员可以使用中间层 API 拦截 LSP 消息。

每个 LSP 消息都有自己的中间层接口进行拦截。 要拦截特定消息，请创建一个类，该类为该消息实现中间层接口。 然后，在语言客户端类中实现[I语言ClientCustomMessage接口](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)，并在["中间层"](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.middlelayer?view=visualstudiosdk-2017)属性中返回对象的实例。 以下示例：

```csharp
public class MockLanguageClient: ILanguageClient, ILanguageClientCustomMessage
{
    public object MiddleLayer => MiddleLayerProvider.Instance;

    private class MiddleLayerProvider : ILanguageClientWorkspaceSymbolProvider
    {
        internal readonly static MiddleLayerProvider Instance = new MiddleLayerProvider();

        private MiddleLayerProvider()
        {
        }

        public async Task<SymbolInformation[]> RequestWorkspaceSymbols(WorkspaceSymbolParams param, Func<WorkspaceSymbolParams, Task<SymbolInformation[]>> sendRequest)
        {
            // Send along the request as given
            SymbolInformation[] symbols = await sendRequest(param);

            // Only return symbols that are "files"
            return symbols.Where(sym => string.Equals(new Uri(sym.Location.Uri).Scheme, "file", StringComparison.OrdinalIgnoreCase)).ToArray();
        }
    }
}
```

中间层特征仍在开发中，尚未全面。

## <a name="sample-lsp-language-server-extension"></a>示例 LSP 语言服务器扩展

要查看 Visual Studio 中使用 LSP 客户端 API 的示例扩展的源代码，请参阅 VSSDK-可扩展性-示例[LSP 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/LanguageServerProtocol)。

## <a name="faq"></a>常见问题解答

**我想构建一个自定义项目系统来补充我的 LSP 语言服务器，在 Visual Studio 中提供更丰富的功能支持，我该怎么做？**

Visual Studio 中基于 LSP 的语言服务器的支持依赖于[打开的文件夹功能](https://devblogs.microsoft.com/visualstudio/open-any-folder-with-visual-studio-15-preview/)，并且设计为不需要自定义项目系统。 您可以[按照此处](https://github.com/Microsoft/VSProjectSystem)的说明构建自己的自定义项目系统，但某些功能（如设置）可能无法正常工作。 LSP 语言服务器的默认初始化逻辑是传递当前打开的文件夹的根文件夹位置，因此，如果您使用自定义项目系统，则可能需要在初始化期间提供自定义逻辑，以确保语言服务器可以正确启动。

**如何添加调试器支持？**

我们将在将来的版本中为[通用调试协议](https://code.visualstudio.com/docs/extensionAPI/api-debugging)提供支持。

**如果已经安装了 VS 支持的语言服务（例如 JavaScript），我是否仍可以安装提供其他功能（如 linting）的 LSP 语言服务器扩展？**

可以，但并非所有功能都正常工作。 LSP 语言服务器扩展的最终目标是启用 Visual Studio 不支持的本机语言服务。 您可以使用 LSP 语言服务器创建提供其他支持的扩展，但某些功能（如 IntelliSense）不会是流畅的体验。 通常，建议使用 LSP 语言服务器扩展来提供新的语言体验，而不是扩展现有语言体验。

**在哪里发布已完成的 LSP 语言服务器 VSIX？**

在此处查看[市场说明。](walkthrough-publishing-a-visual-studio-extension.md)

## <a name="see-also"></a>请参阅

- [为其他语言添加 Visual Studio 编辑器支持](../ide/adding-visual-studio-editor-support-for-other-languages.md)
