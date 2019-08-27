---
title: 发布扩展使用命令行
ms.date: 07/12/2018
ms.topic: conceptual
helpviewer_keywords:
- publishing extensions
- extension, publishing
ms.assetid: 6ff9efc4-919d-4071-a80d-6dbdd2ceb2f8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8a6b5531bc5dc138f2f90a0a67da39f9583bc4b0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66320641"
---
# <a name="walkthrough-publishing-a-visual-studio-extension-via-command-line"></a>演练：发布 Visual Studio 扩展中的通过命令行

此演练演示如何将 Visual Studio 扩展发布到 Visual Studio Marketplace 使用命令行。 当你的扩展添加到 Marketplace 后时，开发人员可以使用[**扩展和更新**](../ide/finding-and-using-visual-studio-extensions.md)对话框从中浏览新建和更新的扩展。

VsixPublisher.exe 是发布到 Marketplace 的 Visual Studio 扩展的命令行工具。 可以从 ${VSInstallDir}\VSSDK\VisualStudioIntegration\Tools\Bin\VsixPublisher.exe 访问。 可在上找到此工具的命令是：**发布**， **createPublisher**， **deletePublisher**， **deleteExtension**， **登录名**，**注销**。

## <a name="commands"></a>命令

### <a name="publish"></a>publish

将扩展发布到 Marketplace。 该扩展可以是 vsix、 exe/msi 文件或链接。 如果扩展已存在具有相同的版本，它将覆盖该扩展。 如果尚不存在该扩展，它将创建一个新的扩展。

|命令选项 |描述 |
|---------|---------|
|有效负载 （必需） | 若要发布的有效负载或将其用作"详细信息 URL"的链接到的路径。 |
|publishManifest （必需） | 发布路径清单文件使用。 |
|ignoreWarnings | 要发布扩展时忽略的警告的列表。 发布扩展时，将为命令行的消息中显示这些警告。 (例如，"VSIXValidatorWarning01，VSIXValidatorWarning02")
|personalAccessToken | 个人访问令牌 (PAT) 用于进行身份验证发布服务器。 如果未提供，则会从登录的用户获取 PAT。 |

```
VsixPublisher.exe publish -payload "{path to vsix}" -publishManifest "{path to vs-publish.json}" -ignoreWarnings "VSIXValidatorWarning01,VSIXValidatorWarning02"
```

### <a name="createpublisher"></a>createPublisher

在 Marketplace 上创建发布服务器。 此外将记录发布服务器到未来的操作 （例如删除/发布扩展） 的计算机。

|命令选项 |描述 |
|---------|---------|
|displayName （必需） | 发布服务器上的显示名称。 |
|publisherName （必需） | 发布服务器 （例如，标识符） 的名称。 |
|personalAccessToken （必需） | 个人访问令牌用于进行身份验证发布服务器。 |
|shortDescription | 发布服务器 （而不是文件） 的简短说明。 |
|longDescription | 发布服务器 （而不是文件） 的详细说明。 |

```
VsixPublisher.exe createPublisher -publisherName "{Publisher Name}" -displayName "{Publisher Display Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deletepublisher"></a>deletePublisher

发布服务器上，在 Marketplace 中删除。

|命令选项 |描述 |
|---------|---------|
|publisherName （必需） | 发布服务器 （例如，标识符） 的名称。 |
|personalAccessToken （必需） | 个人访问令牌用于进行身份验证发布服务器。 |

```
VsixPublisher.exe deletePublisher -publisherName "{Publisher Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deleteextension"></a>deleteExtension

从 Marketplace 中删除扩展。

|命令选项 |描述 |
|---------|---------|
|extensionName （必需） | 要删除的扩展插件的名称。 |
|publisherName （必需） | 发布服务器 （例如，标识符） 的名称。 |
|personalAccessToken | 个人访问令牌用于进行身份验证发布服务器。 如果未提供，则会从登录的用户获取 pat。 |

```
VsixPublisher.exe deleteExtension -extensionName "{Extension Name}" -publisherName "{Publisher Name}"
```

### <a name="login"></a>登录

登录到计算机的发布服务器。

|命令选项 |描述 |
|---------|---------|
|（所需的 personalAccessToken | 个人访问令牌用于进行身份验证发布服务器。 |
|publisherName （必需） | 发布服务器 （例如，标识符） 的名称。 |
|overwrite | 指定应使用新的个人访问令牌覆盖任何现有发布服务器。 |

```
VsixPublisher.exe login -personalAccessToken "{Personal Access Token}" -publisherName "{Publisher Name}"
```

### <a name="logout"></a>注销

记录从计算机的发布服务器。

|命令选项 |描述 |
|---------|---------|
|publisherName （必需） | 发布服务器 （例如，标识符） 的名称。 |
|ignoreMissingPublisher | 指定该工具应不是错误，是否指定的发布服务器是不已登录的。 |

```
VsixPublisher.exe logout -publisherName "{Publisher Name}"
```

## <a name="publishmanifest-file"></a>publishManifest 文件

PublishManifest 文件可供**发布**命令。 它表示有关 Marketplace 需要知道扩展的所有元数据。 如果正在上传的扩展是从 VSIX 扩展，则"标识"属性必须只有"internalName"设置。 这是因为可以从 vsixmanifest 文件生成的"标识"属性的其余部分。 如果扩展是一个 msi/exe 或链接扩展，用户必须提供必填的字段中的"标识"属性。 在清单的剩余部分包含特定于市场上的信息 (例如，类别，是否问答已启用，等等。)。

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

MSI/EXE 或链接 publishManifest 文件示例：

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

资产文件可提供用于在自述文件中嵌入图像等内容。 例如，如果扩展具有以下"概述"Markdown 文档：

```markdown
TestExtension
...
This is test extension.
![Test logo](images/testlogo.png "Test logo")
```

为了解决"images/testlogo.png"上一示例中的，用户可以在提供"assetFiles"其发布清单类似如下：

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

### <a name="prerequisites"></a>系统必备

要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="create-a-visual-studio-extension"></a>创建 Visual Studio 扩展

在这种情况下，我们将使用默认 VSPackage 扩展，但相同的步骤适用于在每个类型的扩展。

1. 在 C# 中名为"TestPublish"具有菜单命令创建 VSPackage。 有关详细信息，请参阅[创建第一个扩展：Hello World](../extensibility/extensibility-hello-world.md)。

### <a name="package-your-extension"></a>打包你的扩展

1. 更新扩展 vsixmanifest 有关产品名称、 作者和版本的正确信息。

   ![更新扩展 vsixmanifest](media/update-extension-vsixmanifest.png)

2. 构建您的扩展插件**版本**模式。 现在您的扩展插件将打包为 VSIX \bin\Release 文件夹中。

3. 你可以双击 VSIX 验证安装成功。

### <a name="test-the-extension"></a>测试此扩展

 分发扩展之前，生成和测试，以确保 Visual Studio 的实验实例中正确安装。

1. 在 Visual Studio 中，开始调试。 若要打开的 Visual Studio 实验实例。

2. 在实验实例中，转到**工具**菜单，然后单击**扩展和更新...** .TestPublish 扩展应显示在中心窗格中，启用。

3. 上**工具**菜单中，请确保您看到测试命令。

### <a name="publish-the-extension-to-the-marketplace-via-command-line"></a>将扩展发布到 Marketplace 通过命令行

1. 请确保你已经构建了您的扩展插件的版本并且保持最新状态。

2. 请确保已创建 publishmanifest.json 和 overview.md 文件。

3. 打开命令行，并导航到 ${VSInstallDir} \VSSDK\VisualStudioIntegration\Tools\Bin\ 目录。

4. 若要创建新的发布服务器，请使用以下命令：

   ```
   VsixPublisher.exe createPublisher -publisherName "TestVSIXPublisher" -displayName "Test VSIX Publisher" -personalAccessToken "{Personal Access Token that is used to authenticate the publisher. If not provided, the pat is acquired from the logged-in users.}"
   ```

5. 在发布服务器创建成功后，您将看到以下的命令行消息：

   ```
   Added 'Test VSIX Publisher' as a publisher on the Marketplace.
   ```

6. 您可以通过导航到创建的新发布服务器来验证[Visual Studio Marketplace](https://marketplace.visualstudio.com/manage/publishers)

7. 若要发布一个新的扩展，请使用以下命令：

   ```
   VsixPublisher.exe publish -payload "{Path to vsix file}"  -publishManifest "{path to publishManifest file}"
   ```

8. 在发布服务器创建成功后，您将看到以下的命令行消息：

   ```
   Uploaded 'MyVsixExtension' to the Marketplace.
   ```

9. 你可以验证新的扩展插件通过导航到发布[Visual Studio Marketplace](https://marketplace.visualstudio.com/)

### <a name="install-the-extension-from-the-visual-studio-marketplace"></a>从 Visual Studio Marketplace 安装扩展

现在，发布扩展时，在 Visual Studio 中安装它，然后对其进行测试。

1. 在 Visual Studio 中，在**工具**菜单上，单击**扩展和更新...** .

2. 单击**Online** TestPublish 然后搜索。

3. 单击 **“下载”** 。 然后将安装计划扩展。

4. 若要完成安装，请关闭 Visual Studio 的所有实例。

## <a name="remove-the-extension"></a>删除扩展

从 Visual Studio Marketplace 和您的计算机，可以删除该扩展。

### <a name="to-remove-the-extension-from-the-marketplace-via-command-line"></a>若要从命令行通过 Marketplace 中删除扩展

1. 如果你想要删除扩展，使用以下命令：

   ```
   VsixPublisher.exe deleteExtension -publisherName "TestVSIXPublisher" -extensionName "MyVsixExtension"
   ```

2. 在成功删除的扩展，您将看到以下的命令行消息：

   ```
   Removed 'MyVsixExtension' from the Marketplace.
   ```

### <a name="to-remove-the-extension-from-your-computer"></a>若要从您的计算机中删除扩展

1. 在 Visual Studio 中，在**工具**菜单上，单击**扩展和更新**。

2. 选择"MyVsixExtension"，然后单击**卸载**。 然后将卸载计划扩展。

3. 若要完成卸载，请关闭 Visual Studio 的所有实例。
