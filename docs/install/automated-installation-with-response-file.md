---
title: 通过响应文件自动执行安装
description: 了解如何创建 JSON 响应文件，以便自动安装 Visual Studio
ms.date: 03/30/2019
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- response file
- automate
- installation
- command-line
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: eb822a275f55b8c0f833f0c284aba2fd663a27fd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62974444"
---
# <a name="how-to-define-settings-in-a-response-file"></a>如何在响应文件中定义设置

部署 Visual Studio 的管理员可以使用 `--in` 参数来指定响应文件，如下例所示：

```cmd
vs_enterprise.exe --in customInstall.json
```

响应文件是 [JSON](http://json-schema.org/) 文件，其内容镜像反转命令行自变量。  一般来说，如果命令行参数未使用任何自变量（例如，`--quiet`、`--passive` 等），响应文件中的值应为 true/false。  如果使用自变量（例如，`--installPath <dir>`），响应文件中的值应为字符串。  如果使用自变量并能在命令行中多次出现（例如，`--add <id>`），响应文件中的值应为一组字符串。

命令行中指定的参数将替代响应文件中的设置，但参数采用多个输入时除外（例如，`--add`）。 具有多个输入时，命令行中提供的输入将与响应文件中的设置合并。

## <a name="setting-a-default-configuration-for-visual-studio"></a>设置 Visual Studio 默认配置

如果使用 `--layout` 创建了网络布局缓存，则会在布局中创建初始 `response.json` 文件。 如果创建一个部分布局，此响应文件将包含与布局中相同的工作负载和语言。  使用此 response.json 文件通过此布局自动运行安装程序，它将选择与布局中相同的工作负载和组件。  安装 Visual Studio 之前，用户仍可选择或取消选择安装 UI 中的任何工作负载。

创建布局的管理员可以修改布局中的 `response.json` 文件，以控制用户通过此布局安装 Visual Studio 时看到的默认设置。  例如，如果管理员希望默认安装特定工作负载和组件，可以配置 `response.json` 文件来添加这些设置。

如果 Visual Studio 安装程序从布局文件夹运行，则会_自动_使用相应布局文件夹中的响应文件。  不必局限于使用 `--in` 选项。

可以更新在脱机布局文件夹中创建的 `response.json` 文件，以定义用户通过此布局进行安装时看到的默认设置。

> [!WARNING]
> 请务必保留创建此布局时定义的现有属性。

布局中的基 `response.json` 文件应与以下示例类似，除非它具有用户想安装的产品和通道的值：

::: moniker range="vs-2017"

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/15/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.15.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise"
}
```

::: moniker-end

::: moniker range="vs-2019"

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/16/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.16.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise"
}
```

::: moniker-end

创建或更新布局时，会同时创建一个 response.template.json 文件。  此文件包含所有可用的工作负载、组件和语言 ID。  此文件以模板形式提供，可包含自定义安装中的所有内容。  管理员可使用此文件作为自定义响应文件的起点。  仅需删除不需要安装的内容的 ID，并将其保存在自己的响应文件中。  请勿自定义 response.template.json 文件，否则一旦布局更新，所做更改就会丢失。

## <a name="example-layout-response-file-content"></a>布局响应文件内容示例

下列示例将安装包含六个常见工作负载和组件且 UI 语言为英语和法语的 Visual Studio Enterprise。 可以将此示例用作模板，只需将工作负载和组件更改为你要安装的内容即可：

::: moniker range="vs-2017"

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/15/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.15.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise",

  "installPath": "C:\\VS2017",
  "quiet": false,
  "passive": false,
  "includeRecommended": true,
  "norestart": false,

  "addProductLang": [
    "en-US",
    "fr-FR"
    ],

    "add": [
        "Microsoft.VisualStudio.Workload.ManagedDesktop",
        "Microsoft.VisualStudio.Workload.Data",
        "Microsoft.VisualStudio.Workload.NativeDesktop",
        "Microsoft.VisualStudio.Workload.NetWeb",
        "Microsoft.VisualStudio.Workload.Office",
        "Microsoft.VisualStudio.Workload.Universal",
        "Component.GitHub.VisualStudio"
    ]
}
```

::: moniker-end

::: moniker range="vs-2019"

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/16/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.16.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise",

  "installPath": "C:\\VS2019",
  "quiet": false,
  "passive": false,
  "includeRecommended": true,
  "norestart": false,

  "addProductLang": [
    "en-US",
    "fr-FR"
    ],

    "add": [
        "Microsoft.VisualStudio.Workload.ManagedDesktop",
        "Microsoft.VisualStudio.Workload.Data",
        "Microsoft.VisualStudio.Workload.NativeDesktop",
        "Microsoft.VisualStudio.Workload.NetWeb",
        "Microsoft.VisualStudio.Workload.Office",
        "Microsoft.VisualStudio.Workload.Universal",
        "Component.GitHub.VisualStudio"
    ]
}
```

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [Visual Studio 工作负荷和组件 ID](workload-and-component-ids.md)
