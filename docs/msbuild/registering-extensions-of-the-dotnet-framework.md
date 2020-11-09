---
title: 注册 .NET Framework 的扩展 | Microsoft Docs
description: 了解如何添加包含将特定版本的 .NET Framework 扩展到系统注册表的程序集的文件夹。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add References dialog box, registering extensions of the .NET Framework
- MSBuild, registering extensions of the .NET Framework
- .NET Framework extensions, registering
ms.assetid: deee6f53-ea87-4b88-a120-bea589822e03
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d63dda9cab50474fd357043d5f694a645a18b2b9
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048750"
---
# <a name="register-extensions-of-the-net-framework"></a>注册 .NET Framework 的扩展

可开发一个扩展特定版本的 .NET Framework 的程序集。 为确保该程序集出现在 Visual Studio“添加引用”对话框中，必须将包含程序集的文件夹添加到系统注册表。

 例如，假定 Trey Research 公司开发出了一个可扩展 .NET Framework 4 的库，且希望当项目以 .NET Framework 4 为目标时，该库程序集可出现在“添加引用”对话框中。 同时假定该程序集是在 32 位计算机上运行的 32 位程序集或在 64 位计算机上运行的 64 位程序集，且会将其安装在 C:\TreyResearch\Extensions4\\ 文件夹。

 使用此密钥注册此文件夹：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.21006\AssemblyFoldersEx\TreyResearch\\。 为密钥赋予此默认值：C:\TreyResearch\Extensions4。

> [!NOTE]
> .NET Framework 版本的生成号可能不同。

 若要在 64 位计算机上注册 32 位的程序集，请使用 Wow6432 节点，例如：HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\v4.0.21006\AssemblyFoldersEx\TreyResearch\\。

### <a name="see-also"></a>另请参阅

- [Visual Studio 集成](../msbuild/visual-studio-integration-msbuild.md)
