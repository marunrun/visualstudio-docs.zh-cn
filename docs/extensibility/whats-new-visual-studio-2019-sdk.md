---
title: 视觉工作室 2019 SDK 中的新增功能 |微软文档
ms.date: 03/29/2019
ms.topic: conceptual
ms.assetid: 4a07607b-0c87-4866-acd8-6d68358d6a47
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 187d3df4b5bcefefc0135c010c7d98951e9b3af8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740400"
---
# <a name="whats-new-in-the-visual-studio-2019-sdk"></a>Visual Studio 2019 SDK 的新增功能

Visual Studio SDK 具有以下可视化工作室 2019 的新功能和更新功能。

## <a name="synchronously-autoloaded-extensions-warning"></a>同步自动加载扩展警告

如果用户的已安装扩展在启动时同步自动加载，则用户现在将看到一条警告。 您可以在[同步自动加载扩展](synchronously-autoloaded-extensions.md)处了解有关警告的更多信息。

## <a name="single-unified-visual-studio-sdk"></a>单一、统一的视觉工作室 SDK

现在，您可以通过单个 NuGet 包[Microsoft](https://www.nuget.org/packages/microsoft.visualstudio.sdk)获取所有 Visual Studio SDK 资产。

## <a name="editor-registration-enhancements"></a>编辑器注册增强功能

自创建以来，Visual Studio 一直支持自定义编辑器注册，其中编辑器可以声明其对特定扩展（例如 .xaml 和 .rc）的关联性，或者它适用于任何扩展 （.*）。 从 Visual Studio 2019 版本 16.1 开始，我们扩大了对编辑器注册的支持。

### <a name="filenames"></a>文件名

除了注册对特定文件扩展名的支持之外，编辑器还可以通过将新`ProvideEditorFilename`属性应用于编辑器的包来注册它支持特定的文件名。

例如，支持所有 .json 文件的编辑器会将此属性`ProvideEditorExtension`应用于其包：

```cs
[ProvideEditorExtension(typeof(MyEditor), ".json", MyEditor.Priority)]
```

从 16.1 开始，如果 MyEditor 仅支持几个众所周知的 .json 文件，则可以将这些`ProvideEditorFilename`属性应用于其包：

```cs
[ProvideEditorFilename(typeof(MyEditor), "particular.json", MyEditor.Priority)]
[ProvideEditorFilename(typeof(MyEditor), "special.json",    MyEditor.Priority)]
```

### <a name="uicontexts"></a>UIContexts

编辑器可以注册一个或多个 UIContext，这些 UIContext 表示启用时。 UIContext 通过将 的一`ProvideEditorUIContextAttribute`个或多个实例应用于注册编辑器的包来注册。

如果编辑器已注册 UIContext：

- 如果打开具有给定扩展名的文件时，其注册的 UIContext 中至少有一个处于活动状态，则编辑器将包含在编辑器搜索中。
- 如果未注册任何 UIContext 处于活动状态，则编辑器中不包括编辑器。

如果编辑器不注册任何 UIContext，则它始终包含在该扩展的编辑器搜索中。

例如，如果编辑器仅在打开 C# 项目时可用，它可以通过应用`ProvideEditorUIContext`属性来声明此关联：

```cs
[ProvideEditorUIContext(typeof(MyEditor), KnownUIContexts.CSharpProjectContext)]
```
