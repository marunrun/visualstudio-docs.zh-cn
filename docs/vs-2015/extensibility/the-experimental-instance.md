---
title: 实验实例 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- VSPackages, experimental builds
- VSIP, experimental builds
ms.assetid: ead0df4e-6f88-4b42-9297-581b7902f050
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ee3c1ef0aed082a0e4e0fb519c744fda376fc8e9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430142"
---
# <a name="the-experimental-instance"></a>实验实例
为了保证从未经测试的应用程序可能会更改其在 Visual Studio 开发环境，请 VSSDK 提供了可用于试验的实验性空间。 像往常一样，使用 Visual Studio 开发新应用程序，但通过使用此实验实例中运行它们。

 具有一个 VSIX 包每个应用程序将启动在调试模式下的 Visual Studio 实验实例。

 如果你想要启动特定的解决方案之外的 Visual Studio 实验实例，请在命令窗口运行以下命令：

 "*\<Visual studio installation path>* \Common7\IDE\devenv.exe" /RootSuffix Exp

> [!NOTE]
> 实验实例写入到注册表`<version number>Exp`和`<version number>Exp_Config`节点。 有关示例的 Visual Studio 2015 的实验性注册表区域是
>
> `HKCU\Software\Microsoft\VisualStudio\14.0Exp` 和 `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`

 我们建议在开发时，在实验实例中运行你的扩展。 当您部署该扩展时，它在开发实例中运行。 有关注册应用程序的详细信息，请参阅[注册 Vspackage](../extensibility/internals/registering-vspackages.md)。