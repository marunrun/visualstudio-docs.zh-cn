---
title: 注册 .NET Framework 的扩展 | Microsoft Docs
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
ms.openlocfilehash: 1957bae45504e5654b3ed63c9fa0821a7f4c8758
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596757"
---
# <a name="register-extensions-of-the-net-framework"></a>注册 .NET Framework 的扩展
可开发一个扩展特定版本的 .NET Framework 的程序集。 为确保该程序集出现在 Visual Studio“添加引用”  对话框中，必须将包含程序集的文件夹添加到系统注册表。

 例如，假定 Trey Research 公司开发出了一个可扩展 .NET Framework 4 的库，且希望当项目以 .NET Framework 4 为目标时，该库程序集可出现在“添加引用”  对话框中。 同时假定该程序集是在 32 位计算机上运行的 32 位程序集或在 64 位计算机上运行的 64 位程序集，且会将其安装在 C:\TreyResearch\Extensions4\\  文件夹。

 使用此密钥注册此文件夹：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.21006\AssemblyFoldersEx\TreyResearch\\  。 为密钥提供此默认值：C:\TreyResearch\Extensions4  。

> [!NOTE]
> .NET Framework 版本的生成号可能不同。

 要在 64 位计算机上注册 32 位程序集，请使用 Wow6432 节点，例如：HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\v4.0.21006\AssemblyFoldersEx\TreyResearch\\  。

### <a name="see-also"></a>请参阅
- [Visual Studio 集成](../msbuild/visual-studio-integration-msbuild.md)
