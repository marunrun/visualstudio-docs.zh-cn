---
title: 管理应用程序资源 (.NET)
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- msvse_resedit.dlg.SetCustomTool
- msvse_settingsdesigner.err.formatvalue
- msvse_resedit.err.nameblank
- msvse_resedit.err.duplicatename
helpviewer_keywords:
- Resource Designer
- resources [Visual Studio]
- Resources page in Project Designer
- application resources [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e53c3701e31733c54869c71820956d674ed4fb8b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75593689"
---
# <a name="manage-application-resources-net"></a>管理应用程序资源 (.NET)

资源文件是应用程序使用的不可编译的文件，例如图标文件或音频文件。 由于这些文件不是编译过程的一部分，因此你可以更改它们而无需重新编译二进制文件。 如果打算本地化你的应用程序，则应为本地化应用程序时需要进行更改的所有字符串和其他资源使用资源文件。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[管理应用资源 (Visual Studio for Mac)](/visualstudio/mac/managing-app-resources)。

有关 .NET 桌面应用中的资源的详细信息，请参阅 [桌面应用中的资源](/dotnet/framework/resources/index)。

## <a name="work-with-resources"></a>使用资源

在托管代码项目中，打开项目属性窗口。 可通过以下任一方法来打开属性窗口：

- 右键单击“解决方案资源管理器”  中的项目节点，并选择“属性” 
- 在 Ctrl  +Q  搜索框中键入项目属性 
- 在解决方案资源管理器窗口中，同时按 Alt+Enter   

选择“资源”  选项卡。如果你的项目尚未包含 .resx 文件，你可以添加一个，添加和删除不同类型的资源，并修改现有资源  。

## <a name="resources-in-other-project-types"></a>其他项目类型中的资源

.NET 项目中管理资源的方式与其他项目类型不同。 若要详细了解以下各项中的资源：

- 通用 Windows 平台 (UWP) 应用中的资源，请参阅[应用资源和资源管理系统](/windows/uwp/app-resources/)
- C++ 项目中的资源，请参阅[使用资源文件](/cpp/windows/working-with-resource-files)和[如何：创建资源](/cpp/windows/how-to-create-a-resource)

## <a name="see-also"></a>请参阅

- [桌面应用中的资源 (.NET Framework)](/dotnet/framework/resources/index)
- [管理应用资源 (Visual Studio for Mac)](/visualstudio/mac/managing-app-resources)
