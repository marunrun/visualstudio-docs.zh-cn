---
title: 管理应用程序资源 (.NET) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- msvse_resedit.dlg.SetCustomTool
- msvse_settingsdesigner.err.formatvalue
- msvse_resedit.err.nameblank
- msvse_resedit.err.duplicatename
helpviewer_keywords:
- editors [Visual Studio], Resource Designer
- Resource Designer
- resources [Visual Studio], managing
- Resources page in Project Designer
- resources types, Resource Designer
- application resources [Visual Studio]
- Project Designer, Resources page
ms.assetid: f2582734-8ada-4baa-8a7c-e2ef943ddf7e
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: efe2b176db9f6f22f9e38775d5fc8acad87655ba
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651389"
---
# <a name="managing-application-resources-net"></a>管理应用程序资源 (.NET)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

资源文件是应用程序使用的不可编译的文件，例如图标文件或音频文件。 由于这些文件不是编译过程的一部分，因此你可以更改它们而无需重新编译二进制文件。 如果打算本地化你的应用程序，则应为本地化应用程序时需要进行更改的所有字符串和其他资源使用资源文件。

 有关 .NET 桌面应用中的资源的详细信息，请参阅 [桌面应用中的资源](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)。 有关 C++ 桌面应用中的资源的详细信息，请参阅 [Working with Resource Files](https://msdn.microsoft.com/library/2699a539-b369-4b78-80f0-df03eb7b6780)。

 Windows 应用商店应用使用桌面应用中的不同资源模型。 有关 Windows 应用商店应用中的资源的信息，请参阅 Windows 开发人员中心网站上的 [定义应用程序资源](https://msdn.microsoft.com/library/windows/apps/hh465228.aspx) 。

## <a name="working-with-resources"></a>使用资源
 在托管代码项目中，打开项目属性窗口（在“解决方案资源管理器” **** 中，右键单击项目节点并选择“属性” ****，或在“快速启动” **** 窗口中键入 **project properties** ，或在“解决方案资源管理器” **** 窗口中键入 ALT + ENTER）。 选择 " **资源** " 选项卡。如果你的项目不包含，则可以添加一个 .resx 文件，添加和删除不同类型的资源，并修改现有资源。

 若要了解如何使用 C++ 项目中的资源，请参阅 [How to: Create a Resource](https://msdn.microsoft.com/library/aad44914-9145-45a3-a7d8-9de89b366716)。
