---
title: MSBuild 16.0 中的新增功能 | Microsoft Docs
ms.date: 03/11/2019
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 9fb23c8a48493056c9a37f510cefea3cc3374095
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62777901"
---
# <a name="whats-new-in-msbuild-160"></a>MSBuild 16.0 中的新增功能

本文介绍 MSBuild 16.0 中已更新的功能和属性。 有关详细的发行说明（仅限草稿），请参阅 [MSBuild 16.0](https://gist.github.com/rainersigwald/009627466f03964d0028e16fda633d9c)。

## <a name="changed-path"></a>更改的路径

 MSBuild 安装在每版 Visual Studio 下的 \Current 文件夹中。 例如，C:\Program Files (x86)\Microsoft Visual Studio\Current\Enterprise\MSBuild。 也可使用下面的 PowerShell 模块查找 MSBuild：[vssetup.powershell](https://github.com/Microsoft/vssetup.powershell)。

## <a name="changed-properties"></a>更改的属性

 下列 MSBuild 属性已因新版本号而更新。

- 此版工具的 `MSBuildToolsVersion` 为“Current”。 程序集版本与 Visual Studio 2017 中的程序集版本相同，为 15.1.0.0。

- 此版工具的 `VisualStudioVersion` 为“16.0”

## <a name="updates"></a>更新

MSBuild（和 Visual Studio）现面向 .NET Framework 4.7.2。 若想要使用新的 MSBuild API 功能，必须升级程序集，但现有代码将继续工作。

## <a name="see-also"></a>请参阅
- [MSBuild](../msbuild/msbuild.md)
