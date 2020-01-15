---
title: 通过源链接调试 NuGet 包
description: 本文介绍 Visual Studio for Mac 中的源链接功能。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 12/16/2019
ms.assetid: 4bcb8acf-db50-4bd8-a48e-86248f00c90b
ms.openlocfilehash: 530ad09bbf72d9696621f328c2df40b37f362c13
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75439084"
---
# <a name="debugging-into-nuget-packages-with-source-link"></a>通过源链接调试 NuGet 包

源链接是一种可以从 NuGet 对 .NET 程序集进行源代码调试的技术，从而将带有源链接的 .PDB 发送给源文件。 源链接在开发人员创建 NuGet 包时执行，然后将源代码管理元数据嵌入在程序集和包中。 如果在 Visual Studio for Mac 中启用源链接，IDE 将检测源文件是否适用于已安装的包。 然后，Visual Studio for Mac 将提供下载，你可以单步执行包代码。 源链接也适用于 Xamarin 项目的 Mono 基类库代码，使你也可以单步执行 .NET Framework 代码。 源链接提供源代码管理元数据来创造出色的调试体验。

> [!NOTE]
> Visual Studio for Mac 目前不支持符号服务器。 因此，不支持具有符号服务器上托管的元数据的源链接。

## <a name="enable-source-link"></a>启用源链接

若要在 Visual Studio for Mac 中启用源链接，请浏览到“Visual Studio”>“首选项...”>“项目”>“调试器”  ，并确保选中“单步执行外部代码”  复选框。

![显示“单步执行外部代码”复选框的首选项对话框屏幕截图](media/source-link1.png)

可以更改“下载外部代码”  中的设置，以满足你的偏好：
* 询问：Visual Studio for Mac 将提示你下载外部代码
* 始终：Visual Studio for Mac 将自动下载外部代码
* 从不：Visual Studio for Mac 不会下载相关外部代码

默认情况下，选择的是“询问”  。 如果找到 NuGet 包的外部代码，则会收到以下提示：

![找到 NuGet 包的外部代码时显示的提示屏幕截图](media/source-link2.png)


## <a name="see-also"></a>请参阅

- [源链接 GitHub 存储库](https://github.com/dotnet/sourcelink/blob/master/README.md)
- 有关源链接以及如何向包添加源链接支持的详细信息，请参阅 [.NET 文档](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink)
