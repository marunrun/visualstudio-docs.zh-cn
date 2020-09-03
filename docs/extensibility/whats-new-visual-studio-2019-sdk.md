---
title: Visual Studio 2019 SDK 的新增功能 |Microsoft Docs
ms.date: 03/29/2019
ms.topic: conceptual
ms.assetid: 4a07607b-0c87-4866-acd8-6d68358d6a47
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 187d3df4b5bcefefc0135c010c7d98951e9b3af8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80740400"
---
# <a name="whats-new-in-the-visual-studio-2019-sdk"></a>Visual Studio 2019 SDK 的新增功能

Visual Studio SDK 具有以下新的和更新的 Visual Studio 2019 功能。

## <a name="synchronously-autoloaded-extensions-warning"></a>同步加载扩展警告

如果任何安装的扩展插件在启动时同步加载，则用户现在会看到警告。 你可以在 [同步加载扩展](synchronously-autoloaded-extensions.md)中了解有关警告的详细信息。

## <a name="single-unified-visual-studio-sdk"></a>单个统一 Visual Studio SDK

现在，你可以通过一个 NuGet 包 [VisualStudio](https://www.nuget.org/packages/microsoft.visualstudio.sdk)获取所有 VISUAL Studio SDK 资产。

## <a name="editor-registration-enhancements"></a>编辑器注册增强功能

自它创建后，Visual Studio 支持自定义编辑器注册，其中编辑器可以为特定的扩展声明其相关性 (例如，.xaml 和 .rc) ，或适用于任何扩展名 (. * ) 。 从 Visual Studio 2019 版本16.1 开始，我们扩大了对编辑器注册的支持。

### <a name="filenames"></a>文件名

除了、或而不是注册特定文件扩展名的支持外，编辑器还可以通过将新属性应用于编辑器的包来注册它是否支持特定文件名 `ProvideEditorFilename` 。

例如，支持所有 json 文件的编辑器会将此 `ProvideEditorExtension` 属性应用到其包：

```cs
[ProvideEditorExtension(typeof(MyEditor), ".json", MyEditor.Priority)]
```

从16.1 开始，如果 MyEditor 仅支持几个已知的 json 文件，则可以将这些 `ProvideEditorFilename` 属性应用到其包：

```cs
[ProvideEditorFilename(typeof(MyEditor), "particular.json", MyEditor.Priority)]
[ProvideEditorFilename(typeof(MyEditor), "special.json",    MyEditor.Priority)]
```

### <a name="uicontexts"></a>UIContexts

编辑器可以注册一个或多个表示启用时的 UIContexts。 UIContexts 是通过将一个或多个实例应用 `ProvideEditorUIContextAttribute` 于注册编辑器的包来注册的。

如果编辑器已注册 UIContexts：

- 如果打开具有给定扩展名的文件时，其中至少有一个已注册的 UIContexts 处于活动状态，则编辑器将包含在编辑器搜索中。
- 如果没有任何已注册的 UIContexts 处于活动状态，编辑器将不包含在编辑器搜索中。

如果编辑器未注册任何 UIContexts，则它始终包含在编辑器中搜索该扩展插件。

例如，如果编辑器仅在 c # 项目打开时才可用，则它可以通过应用特性来声明此关联 `ProvideEditorUIContext` ：

```cs
[ProvideEditorUIContext(typeof(MyEditor), KnownUIContexts.CSharpProjectContext)]
```
