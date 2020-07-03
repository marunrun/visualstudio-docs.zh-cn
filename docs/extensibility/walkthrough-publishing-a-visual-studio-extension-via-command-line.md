---
title: 使用命令行发布扩展
ms.date: 07/12/2018
ms.topic: how-to
helpviewer_keywords:
- publishing extensions
- extension, publishing
ms.assetid: 6ff9efc4-919d-4071-a80d-6dbdd2ceb2f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5108f4afa382c00376424432d2086f0494e34a03
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904675"
---
# <a name="walkthrough-publishing-a-visual-studio-extension-via-command-line"></a>演练：通过命令行发布 Visual Studio 扩展

本演练演示如何使用命令行将 Visual Studio 扩展发布到 Visual Studio Marketplace。 将扩展添加到 Marketplace 后，开发人员可以使用 "[**扩展和更新**](../ide/finding-and-using-visual-studio-extensions.md)" 对话框浏览新的和已更新的扩展。

VsixPublisher.exe 是将 Visual Studio 扩展发布到 Marketplace 的命令行工具。 它可从 $ {VSInstallDir} \VSSDK\VisualStudioIntegration\Tools\Bin\VsixPublisher.exe 访问。 此工具上可用的命令包括：**发布**、 **createPublisher**、 **deletePublisher**、 **deleteExtension**、 **login**、**注销**。

## <a name="commands"></a>命令

### <a name="publish"></a>发布

将扩展发布到 Marketplace。 扩展可以是 vsix、exe/msi 文件或链接。 如果已存在具有相同版本的扩展，它将覆盖该扩展。 如果扩展不存在，则将创建一个新扩展。

|命令选项 |说明 |
|---------|---------|
|负载（必需） | 要发布的有效负载的路径或用作 "详细信息 URL" 的链接。 |
|publishManifest （必需） | 要使用的发布清单文件的路径。 |
|ignoreWarnings | 发布扩展时要忽略的警告列表。 发布扩展时，这些警告显示为命令行消息。 （例如，"VSIXValidatorWarning01，VSIXValidatorWarning02"）
|personalAccessToken | 用于对发布服务器进行身份验证的个人访问令牌（PAT）。 如果未提供，则将从已登录用户获取 PAT。 |

```
VsixPublisher.exe publish -payload "{path to vsix}" -publishManifest "{path to vs-publish.json}" -ignoreWarnings "VSIXValidatorWarning01,VSIXValidatorWarning02"
```

### <a name="createpublisher"></a>createPublisher

在 Marketplace 上创建发布者。 还会将发布服务器记录到计算机中，以便将来执行操作（例如，删除/发布扩展）。

|命令选项 |说明 |
|---------|---------|
|displayName （必需） | 发布服务器的显示名称。 |
|publisherName （必需） | 发布服务器的名称（例如，标识符）。 |
|personalAccessToken （必需） | 用于对发布服务器进行身份验证的个人访问令牌。 |
|shortDescription | 发行者的简短说明（不是文件）。 |
|longDescription | 发布服务器（不是文件）的长说明。 |

```
VsixPublisher.exe createPublisher -publisherName "{Publisher Name}" -displayName "{Publisher Display Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deletepublisher"></a>deletePublisher

删除 Marketplace 上的发布服务器。

|命令选项 |说明 |
|---------|---------|
|publisherName （必需） | 发布服务器的名称（例如，标识符）。 |
|personalAccessToken （必需） | 用于对发布服务器进行身份验证的个人访问令牌。 |

```
VsixPublisher.exe deletePublisher -publisherName "{Publisher Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deleteextension"></a>deleteExtension

从 Marketplace 中删除扩展。

|命令选项 |说明 |
|---------|---------|
|extensionName （必需） | 要删除的扩展的名称。 |
|publisherName （必需） | 发布服务器的名称（例如，标识符）。 |
|personalAccessToken | 用于对发布服务器进行身份验证的个人访问令牌。 如果未提供，则将从已登录用户获取 pat。 |

```
VsixPublisher.exe deleteExtension -extensionName "{Extension Name}" -publisherName "{Publisher Name}"
```

### <a name="login"></a>login

将发布服务器记录到计算机中。

|命令选项 |说明 |
|---------|---------|
|personalAccessToken （必需 | 用于对发布服务器进行身份验证的个人访问令牌。 |
|publisherName （必需） | 发布服务器的名称（例如，标识符）。 |
|overwrite | 指定应使用新的个人访问令牌覆盖任何现有发布服务器。 |

```
VsixPublisher.exe login -personalAccessToken "{Personal Access Token}" -publisherName "{Publisher Name}"
```

### <a name="logout"></a>logout

将发布服务器记录在计算机之外。

|命令选项 |说明 |
|---------|---------|
|publisherName （必需） | 发布服务器的名称（例如，标识符）。 |
|ignoreMissingPublisher | 如果指定的发布服务器尚未登录，则指定该工具不会出错。 |

```
VsixPublisher.exe logout -publisherName "{Publisher Name}"
```

## <a name="publishmanifest-file"></a>publishManifest 文件

"**发布**" 命令使用 publishManifest 文件。 它表示 Marketplace 需要了解的有关扩展的所有元数据。 如果要上传的扩展来自 VSIX 扩展，则 "identity" 属性只能设置为 "internalName"。 这是因为可以从 source.extension.vsixmanifest 文件生成其余的 "标识" 属性。 如果扩展是 msi/exe 或链接扩展，则用户必须在 "标识" 属性中提供必填字段。 清单的其余部分包含特定于 Marketplace 的信息（例如，类别、Q&是否已启用，等等）。

VSIX 扩展 publishManifest 文件示例：

```json
{
    "$schema": "http://json.schemastore.org/vsix-publish",
    "categories": [ "build", "coding" ],  // The categories of the extension. Between 1 and 3 categories are required.
    "identity": {
        "internalName": "MyVsixExtension" // If not specified, we try to generate the name from the display name of the extension in the vsixmanifest file.
                                            // Required if the display name is not the actual name of the extension.
    },
    "overview": "overview.md",            // Path to the "readme" file that gets uploaded to the Marketplace. Required.
    "priceCategory": "free",              // Either "free", "trial", or "paid". Defaults to "free".
    "publisher": "MyPublisherName",       // The name of the publisher. Required.
    "private": false,                     // Specifies whether or not the extension should be public when uploaded. Defaults to false.
    "qna": true,                          // Specifies whether or not the extension should have a Q&A section. Defaults to true.
    "repo": "https://github.com/MyPublisherName/MyVsixExtension" // Not required.
}
```

MSI/EXE 或 LINK publishManifest 文件示例：

```json
{
    "$schema": "http://json.schemastore.org/vsix-publish",
    "categories": [ "build", "coding" ],
    "identity": {
        "description": "My extension.", // The description of the extension. Required for non-vsix extensions.
        "displayName": "My Extension",  // The display name of the extension. Required for non-vsix extensions.
        "icon": "\\path\\to\\icon.ico", // The path to an icon file (can be relative to the json file location). Required for non-vsix extensions.
        "installTargets": [             // The installation targets for the extension. Required for non-vsix extensions.
            {
                "sku": "Microsoft.VisualStudio.Community",
                "version": "[10.0, 16.0)"
            }
        ],
        "internalName": "MyExtension",
        "language": "en-US",            // The default language id of the extension. Can be in the "1033" or "en-US" format. Required for non-vsix extensions.
        "tags": [ "tag1", "tag2" ],     // The tags for the extension. Not required.
        "version": "3.7.0",             // The version of the extension. Required for non-vsix extensions.
        "vsixId": "MyExtension",        // The vsix id of the extension. Not required but useful for showing updates to installed extensions.
    },
    "overview": "overview.md",
    "priceCategory": "free",
    "publisher": "MyPublisherName",
    "private": false,
    "qna": true,
    "repo": "https://github.com/MyPublisherName/MyVsixExtension"
}
```

## <a name="asset-files"></a>资产文件

可以提供资产文件，以便在自述文件中嵌入图像等。 例如，如果扩展具有以下 "概述" Markdown 文档：

```markdown
TestExtension
...
This is test extension.
![Test logo](images/testlogo.png "Test logo")
```

为了解决上一个示例中的 "images/testlogo.png"，用户可以在其发布清单中提供 "assetFiles"，如下所示：

```json
{
    "assetFiles": [
        {
            "pathOnDisk": "\\path\\to\\logo.png",
            "targetPath": "images/logo.png"
        }
    ],
    // other required fields
}
```

## <a name="publishing-walkthrough"></a>发布演练

### <a name="prerequisites"></a>必备条件

要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="create-a-visual-studio-extension"></a>创建 Visual Studio 扩展

在这种情况下，我们将使用默认的 VSPackage 扩展，但相同的步骤对每种类型的扩展都有效。

1. 在 c # 中创建一个名为 "TestPublish" 的 VSPackage，其中包含一个菜单命令。 有关详细信息，请参阅[创建第一个扩展： Hello World](../extensibility/extensibility-hello-world.md)。

### <a name="package-your-extension"></a>打包扩展

1. 将扩展 source.extension.vsixmanifest 更新为有关产品名称、作者和版本的正确信息。

   ![更新扩展 source.extension.vsixmanifest](media/update-extension-vsixmanifest.png)

2. 在**发布**模式下构建扩展。 现在，你的扩展将打包为 \bin\Release 文件夹中的一个 VSIX。

3. 可以双击 VSIX 来验证安装。

### <a name="test-the-extension"></a>测试扩展

 在分发扩展之前，请生成并测试该扩展，以确保它已正确安装在 Visual Studio 的实验实例中。

1. 在 Visual Studio 中，启动调试。 打开 Visual Studio 的实验实例。

2. 在实验实例中，请单击 "**工具**" 菜单，然后单击 "**扩展和更新 ...**"。TestPublish 扩展应显示在中心窗格中并启用。

3. 在 "**工具**" 菜单上，确保看到 "测试" 命令。

### <a name="publish-the-extension-to-the-marketplace-via-command-line"></a>通过命令行将扩展发布到 Marketplace

1. 请确保已生成扩展的发行版，并且该版本是最新版本。

2. 请确保已创建 publishmanifest.js和 overview.md 文件。

3. 打开命令行，导航到 $ {VSInstallDir} \VSSDK\VisualStudioIntegration\Tools\Bin\ 目录。

4. 若要创建新的发布服务器，请使用以下命令：

   ```
   VsixPublisher.exe createPublisher -publisherName "TestVSIXPublisher" -displayName "Test VSIX Publisher" -personalAccessToken "{Personal Access Token that is used to authenticate the publisher. If not provided, the pat is acquired from the logged-in users.}"
   ```

5. 成功创建发布服务器后，会显示以下命令行消息：

   ```
   Added 'Test VSIX Publisher' as a publisher on the Marketplace.
   ```

6. 可以通过导航到来验证所创建的新发布服务器[Visual Studio Marketplace](https://marketplace.visualstudio.com/manage/publishers)

7. 若要发布新扩展，请使用以下命令：

   ```
   VsixPublisher.exe publish -payload "{Path to vsix file}"  -publishManifest "{path to publishManifest file}"
   ```

8. 成功创建发布服务器后，会显示以下命令行消息：

   ```
   Uploaded 'MyVsixExtension' to the Marketplace.
   ```

9. 可以通过导航到来验证发布的新扩展[Visual Studio Marketplace](https://marketplace.visualstudio.com/)

### <a name="install-the-extension-from-the-visual-studio-marketplace"></a>从 Visual Studio Marketplace 安装扩展

扩展已发布后，请在 Visual Studio 中进行安装，并在其中进行测试。

1. 在 Visual Studio 的 "**工具**" 菜单上，单击 "**扩展和更新 ...**"。

2. 单击 "**联机**"，然后搜索 "TestPublish"。

3. 单击“下载”。 然后，将计划安装该扩展。

4. 若要完成安装，请关闭 Visual Studio 的所有实例。

## <a name="remove-the-extension"></a>删除扩展

可以从 Visual Studio Marketplace 和计算机中删除该扩展。

### <a name="to-remove-the-extension-from-the-marketplace-via-command-line"></a>通过命令行从 Marketplace 中删除扩展

1. 如果要删除扩展，请使用以下命令：

   ```
   VsixPublisher.exe deleteExtension -publisherName "TestVSIXPublisher" -extensionName "MyVsixExtension"
   ```

2. 成功删除扩展后，会看到以下命令行消息：

   ```
   Removed 'MyVsixExtension' from the Marketplace.
   ```

### <a name="to-remove-the-extension-from-your-computer"></a>从计算机中删除扩展

1. 在 Visual Studio 的 "**工具**" 菜单上，单击 "**扩展和更新**"。

2. 选择 "MyVsixExtension"，然后单击 "**卸载**"。 然后，将为卸载计划该扩展。

3. 若要完成卸载，请关闭 Visual Studio 的所有实例。
