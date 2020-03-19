---
title: 在设计时解析程序集 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild
ms.assetid: 20dae076-733e-49c1-a2e9-b336757ae21d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 69f5ba2627e2d659665fa0bd3fbf706f9cad5573
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77632558"
---
# <a name="resolve-assemblies-at-design-time"></a>在设计时解析程序集

当通过“添加引用”  对话框的“.NET”  选项卡添加对程序集的引用时，引用将指向一个中间引用程序集；所谓中间引用程序集，是指包含所有类型和签名信息但不一定包含任何代码的程序集。 “.NET”  选项卡列出 .NET Framework 中运行时程序集对应的引用程序集。 此外，它还列出第三方使用的注册 AssemblyFoldersEx 文件夹中运行时程序集所对应的引用程序集。

## <a name="multi-targeting"></a>多目标

 通过 Visual Studio，你可以将目标设定为在 .NET Framework 的多个版本上运行的 .NET Framework 的版本。 如果发行了 .NET Framework 新版本，则可使用目标包安装 Framework，且 Framework 会在 Visual Studio 中作为目标自动显示。

## <a name="how-type-resolution-works"></a>类型解析的工作原理

 在运行时，CLR 通过查找 GAC、bin 目录和任何探测路径来解析程序集中的类型  。 这由融合加载程序处理。 但是，融合加载程序如何知道其要查找的内容？ 这取决于设计时（生成应用程序时）创建的解决方案。

 在生成期间，编译器使用引用程序集解析应用程序类型。 在 .NET Framework 2.0、3.0、3.5、4、4.5 和 4.5.1 版中，引用程序集将随 .NET Framework 一起安装。

 引用程序集由相应版本的 .NET Framework SDK 所附带的目标包提供。 Framework 自身仅提供运行时程序集。 若要生成应用程序，需要安装 .NET Framework 以及相应的 .NET Framework SDK。

 面向特定 .NET Framework 时，生成系统通过使用目标包中的引用程序集来解析所有类型。 在运行时，融合加载程序将这些相同类型解析到运行时程序集（通常位于 GAC 中）。

 如果引用程序集不可用，则生成系统会使用运行时程序集解析程序集类型。 由于 GAC 中的运行时程序集不是以次要版本号区分，因此可能会对错误的程序集生成解决方案。 有可能会发生这种情况。例如，虽然面向版本 3.0，但却引用 .NET Framework 版本 3.5 中引入的新方法。 虽然生成会成功且应用程序会在生成计算机上运行，但应用程序在部署到未安装版本 3.5 的计算机上时会失败。

 .NET Framework SDK 现在附带的目标包中具有该版本 Framework 中所有运行时程序集的列表，即再分发 (redist) 列表，因此生成系统无法解析针对错误版本程序集的类型。

## <a name="see-also"></a>请参阅
- [高级概念](../msbuild/msbuild-advanced-concepts.md)
