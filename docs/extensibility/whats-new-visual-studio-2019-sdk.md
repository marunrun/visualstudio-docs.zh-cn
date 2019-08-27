---
title: 什么是 Visual Studio 2019 SDK 中的新增功能 |Microsoft Docs
ms.date: 03/29/2019
ms.topic: conceptual
ms.assetid: 4a07607b-0c87-4866-acd8-6d68358d6a47
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d4be152cfb39ddea9ddaeea56464a3447be4f2c6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66320607"
---
# <a name="whats-new-in-the-visual-studio-2019-sdk"></a>Visual Studio 2019 SDK 的新增功能

Visual Studio SDK 的 Visual Studio 2019 具有以下新的和更新功能。

## <a name="synchronously-autoloaded-extensions-warning"></a>以同步方式加载扩展的警告

如果任何已安装的扩展以同步方式启动时加载，用户现在将看到一条警告。 了解在警告[以同步方式加载扩展](synchronously-autoloaded-extensions.md)。

## <a name="single-unified-visual-studio-sdk"></a>统一的 Visual Studio SDK

现在可以通过一个 NuGet 包获取 Visual Studio SDK 的所有资产[Microsoft.VisualStudio.SDK](https://www.nuget.org/packages/microsoft.visualstudio.sdk)。

## <a name="editor-registration-enhancements"></a>编辑器注册增强功能

自其创建 Visual Studio 已支持的自定义编辑器注册编辑器可以声明其相关性，特定扩展名 （例如，.xaml 和.rc） 或程序的情况是适用于任何扩展 (。 *)。 我们从 Visual Studio 2019 版本 16.1，扩大编辑器注册的支持。

### <a name="filenames"></a>文件名

除此之外或代替，注册某个特定文件扩展名的支持，可以注册编辑器，它通过应用新支持特定文件名`ProvideEditorFilename`属性编辑器的包。

例如，支持所有的.json 文件的编辑器会应用此`ProvideEditorExtension`到其包属性：

```cs
[ProvideEditorExtension(typeof(MyEditor), ".json", MyEditor.Priority)]
```

从开始 16.1，如果 MyEditor 仅支持几个已知的.json 文件，它可以改为将这些应用`ProvideEditorFilename`到其包属性：

```cs
[ProvideEditorFilename(typeof(MyEditor), "particular.json", MyEditor.Priority)]
[ProvideEditorFilename(typeof(MyEditor), "special.json",    MyEditor.Priority)]
```

### <a name="uicontexts"></a>UIContexts

编辑器可以注册一个或多个表示启用后的 UIContexts。 通过应用一个或多个实例注册 UIContexts`ProvideEditorUIContextAttribute`到注册在编辑器的包。

如果编辑器具有已注册的 UIContexts:

- 如果具有给定扩展名的文件打开时，至少一个其已注册 UIContexts 处于活动状态，编辑器将包括在编辑器中搜索。
- 如果没有任何已注册 UIContexts 处于活动状态，在编辑器不是包含在编辑器中搜索。

如果编辑器未注册任何 UIContexts，它始终包括在编辑器中搜索该扩展。

例如，如果编辑器才可用C#项目处于打开状态，它可以通过应用声明此地缘`ProvideEditorUIContext`属性：

```cs
[ProvideEditorUIContext(typeof(MyEditor), KnownUIContexts.CSharpProjectContext)]
```
