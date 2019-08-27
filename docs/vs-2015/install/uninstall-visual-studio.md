---
title: 卸载 Visual Studio 2015 | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
f1_keywords:
- uninstalling
- uninstalling visual studio
- uninstall
- uninstall Visual Studio
ms.assetid: 0e445255-b796-426d-ad93-a4d8e36da2c5
caps.latest.revision: 9
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: ed9d33501644c6fa7252dffa758f92c0919653b1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546897"
---
# <a name="uninstall-visual-studio"></a>卸载 Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅[卸载 Visual Studio](/visualstudio/install/uninstall-visual-studio)。

此页面介绍如何卸载 Visual Studio 2015（一个面向开发人员的工作效率工具集成套件的早期版本）。

## <a name="uninstall-visual-studio-by-using-the-standard-uninstallation-method"></a>使用“标准”卸载方法卸载 Visual Studio

1. 在“控制面板”上的“程序和功能”页中，选择要卸载的产品版本，然后选择“更改”。

2. 在安装向导中，选择“卸载”，再选择“是”，然后在向导中按照其余说明进行操作。

   此标准或默认方法将留下首次安装 Visual Studio 时最初安装的某些项（例如，Microsoft .NET Framework、Microsoft Visual C++ 可再发行组件、Microsoft SQL Server 等）。   由于其他许多应用程序依赖于这些已安装的项，因此我们会保留这些项。 但是，如果也要将其删除，请选择“程序和功能”中对应的条目，然后逐个进行删除。

## <a name="uninstall-visual-studio-and-all-other-related-files-that-is-to-uninstall-almost-everything"></a>卸载 Visual Studio 和所有其他相关文件（即，卸载几乎所有项）

1. 找到 Visual Studio .exe 文件（例如，找到“vs_enterprise.exe”）。

    > [!NOTE]
    > 该文件应位于“%ProgramData%\Package Cache”的子文件夹中，例如：C:\ProgramData\Package Cache\\{37e19555-e88d-4aed-9d42-82d0784d2b79}\vs_enterprise.exe

2. 使用 /uninstall /force 命令行参数运行 .exe 文件。

     例如，运行 ```vs_enterprise.exe /uninstall /force```，这将删除 Visual Studio 以及留在默认卸载中的大部分核心组件。 但是，不会删除 Visual Studio 附加产品和扩展可以安装的所有其他内容（例如，Visual Studio 更新和其他可选组件）。

    > [!TIP]
    > 或者，可以使用“卸载程序总数”工具来删除 Visual Studio 或 Visual Studio 更新可能已安装的所有项。 也就是说，任何版本的 Visual Studio 2013 或更高版本。 若要获取详细信息，请参阅 GitHub 上的 [Visual Studio 卸载程序工具](https://github.com/Microsoft/VisualStudioUninstaller/releases)。

## <a name="uninstall-visual-studio-in-silent-or-passive-modes-that-is-to-uninstall-from-source"></a>在无提示或被动模式下卸载 Visual Studio（即，从源中卸载）

1. 在安装了 Visual Studio 的计算机上，打开 Windows 命令提示符。

2. 输入以下参数：

     DVDRoot \\<Installation File\> \</quiet&#124;/passive> [/norestart]/uninstall

## <a name="roll-back-to-a-previous-version-or-release-of--visual-studio"></a>回滚到早期版本的 Visual Studio

1. 使用本主题中列出的任何方法卸载 Visual Studio。

   > [!WARNING]
   > 可能不会按预期卸载当前版本的 Visual Studio（或 Visual Studio 更新）然后安装早期版本。
   >
   > 结果取决于已安装 Visual Studio 的哪个版本、已安装其组件的哪些版本、已安装哪些产品（可能具有依赖项 Visual Studio 版本或其组件），以及计划安装或重新安装 Visual Studio 的哪个早期版本。  由于所有这些变量，标准卸载通常会保留可能不适用于早期版本的 Visual Studio 的组件。
   >
   > 因此，为了获得最佳结果，我们建议使用 [Visual Studio 卸载程序工具](https://github.com/Microsoft/VisualStudioUninstaller/releases)。

2. 安装或重新安装要使用的 Visual Studio 的早期版本。

   即使安装早期版本的 Visual Studio，安装程序可能仍会尝试使用较新版本（如果有）。 有关详细信息，请参阅[如何：安装特定版本的 Visual Studio](../install/how-to-install-a-specific-release-of-visual-studio.md) 主题。

## <a name="see-also"></a>请参阅

- [安装 Visual Studio](https://msdn.microsoft.com/library/e2h7fzkw.aspx)