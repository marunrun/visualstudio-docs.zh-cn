---
title: 并排安装 Visual Studio 版本 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
helpviewer_keywords:
- side-by-side installations [Visual Studio]
- Help [Visual Studio], installing
- install multiple versions of Visual Studio
ms.assetid: 4d00f240-4910-4699-aaf3-cda6461f0c29
caps.latest.revision: 48
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: a146872561c4be5fe48016c17eb64ad6f854106a
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298026"
---
# <a name="install-visual-studio-versions-side-by-side"></a>并行安装 Visual Studio 版本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以在已安装早期版本的计算机上安装此版本的 Visual Studio。 如果遇到安装故障，则可以使用 [日志收集工具](https://go.microsoft.com/fwlink/?LinkId=262077) 收集有关故障的信息，以便可以自行调试问题。

> [!NOTE]
> 建议您按照发布顺序来安装不同版本的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 例如，在安装 Visual Studio 2015 之前安装 Visual Studio 2013。

 在并行安装各版本之前，您应该了解以下情况：

- 如果使用 Visual Studio 2015 打开在 [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)]中创建的解决方案，则稍后可以在旧版本中再次打开和修改该解决方案，前提是你没有执行任何 Visual Studio 2015 特有的功能。

- 如果你尝试使用 Visual Studio 2015 打开在 [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] 或更早的版本中创建的解决方案，则可能需要修改你的项目和文件才能与 Visual Studio 2015 兼容。 有关详细信息，请参阅[移植、迁移和升级 Visual Studio 项目](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects?view=vs-2015)页。

- 如果在已安装多个版本的计算机上卸载 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的一个版本，则将为所有版本移除 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的文件关联。 通过使用 **“选项”** 对话框的 **“常规”** 页上的 **“环境”** 中的 [“还原文件关联”](../ide/reference/general-environment-options-dialog-box.md) 按钮，可以重新映射这些文件关联。

- 因为并非所有扩展都兼容，所以 Visual Studio 不会自动升级扩展。 必须从 [Visual Studio Marketplace](https://go.microsoft.com/fwlink/?LinkId=178891) 或软件发行者处重新安装扩展。

## <a name="net-framework-versions-and-side-by-side-installations"></a>.NET Framework 版本和并行安装

- Visual Basic、Visual C# 和 Visual F# 项目使用 **“项目设计器”** 中的 **“目标框架”** 选项来指定项目使用的 .NET Framework 版本。 对于 C++ 项目，您可以通过修改 .vcxproj 文件手动更改目标框架。 有关详细信息，请参阅[版本兼容性](https://msdn.microsoft.com/library/2f25e522-456a-48c3-8a53-e5f39275649f)。

     创建项目时，可以在 **“新建项目”** 对话框中的 **“.NET Framework”** 列表中指定项目针对的 .NET Framework 版本。

     有关语言特定的信息，请参见下表中的相应主题。

    |语言|主题|
    |--------------|-----------|
    |[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]|[“项目设计器”->“应用程序”页 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)|
    |Visual C#|[“项目设计器”->“应用程序”页 (C#)](../ide/reference/application-page-project-designer-csharp.md)|
    |Visual F#|[配置项目](https://msdn.microsoft.com/library/a1489abb-6294-4f8f-b71f-2cb126393526)|
    |C++|[如何：修改目标框架和平台工具集](https://msdn.microsoft.com/library/031b1d54-e6e1-4da7-9868-3e75a87d9ffe)|
    |[!INCLUDE[jsprjscript](../includes/jsprjscript-md.md)]|[在公共语言运行时的上一版本上运行 JScript 应用程序](https://msdn.microsoft.com/bbea51b5-ac03-4e6c-b9a6-f487ef63eda5)|

## <a name="see-also"></a>另请参阅

- [安装 Visual Studio](../install/install-visual-studio-2015.md)
- [移植、迁移和升级 Visual Studio 项目](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects?view=vs-2015)
- [生成 C/C++ 独立应用程序和并行程序集](https://msdn.microsoft.com/library/9465904e-76f7-48bd-bb3f-c55d8f1699b6)
- [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)