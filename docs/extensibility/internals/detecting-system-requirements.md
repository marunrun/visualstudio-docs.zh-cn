---
title: 检测系统要求 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- setup, VSPackages
- launch conditions
ms.assetid: 0ba94acf-bf0b-4bb3-8cca-aaac1b5d6737
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9ab254df5d53f379704128d8860b8d7fe5655bae
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708739"
---
# <a name="detect-system-requirements"></a>检测系统要求
除非安装了 Visual Studio，否则 VS 包无法正常工作。 当您使用 Microsoft Windows 安装程序管理 VSPackage 的安装时，可以配置安装程序以检测是否安装了 Visual Studio。 您还可以将其配置为检查系统是否具有其他要求，例如，特定版本的 Windows 或特定数量的 RAM。

## <a name="detect-visual-studio-editions"></a>检测视觉工作室版本
 要确定是否安装了 Visual Studio 版本，请验证**安装**注册表项的值是否为相应文件夹中 *（REG_DWORD 如下表中列出的）1。* 请注意，有视觉工作室版本的层次结构：

1. Enterprise

2. 专业版

3. 社区

安装较新版本后，将添加该版本的注册表项以及早期版本的注册表项。 也就是说，如果安装了企业版，则**安装密钥设置为** *1*面向企业版以及专业版和社区版。 因此，您只需检查所需的最新版本。

> [!NOTE]
> 在注册表编辑器的 64 位版本中，32 位键显示在**HKEY_LOCAL_MACHINE_SOFTWARE_Wow6432Node\\**下。 视觉工作室键在**HKEY_LOCAL_MACHINE_SOFTWARE_Wow6432Node_微软_DevDiv_vs_服务\\**。

|Products|密钥|
|-------------|---------|
|Visual Studio Enterprise 2015|HKEY_LOCAL_MACHINE_软件_微软_DevDiv_vs_服务\14.0\企业|
|Visual Studio Professional 2015|HKEY_LOCAL_MACHINE_软件_微软_DevDiv_vs_服务\14.0\专业|
|Visual Studio Community 2015|HKEY_LOCAL_MACHINE_SOFTWARE_微软_DevDiv_vs_服务\14.0\社区|
|视觉工作室 2015 外壳（集成和隔离）|HKEY_LOCAL_MACHINE_SOFTWARE_微软_DevDiv_vs_服务\14.0\isoshell|

## <a name="detect-when-visual-studio-is-running"></a>检测可视化工作室何时运行
 如果安装 VSPackage 时 Visual Studio 正在运行，则无法正确注册您的 VS 包。 安装程序必须检测 Visual Studio 何时运行，然后拒绝安装程序。 Windows 安装程序不允许使用表条目启用此类检测。 相反，您必须创建一个自定义操作，如下所示：使用`EnumProcesses`函数检测*devenv.exe*进程，然后设置在启动条件中使用的安装程序属性，或者有条件地显示一个对话框，提示用户关闭 Visual Studio。

## <a name="see-also"></a>请参阅
- [使用 Windows 安装程序安装 VS 包](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
