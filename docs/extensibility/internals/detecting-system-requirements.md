---
title: 检测系统要求 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- setup, VSPackages
- launch conditions
ms.assetid: 0ba94acf-bf0b-4bb3-8cca-aaac1b5d6737
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1ef76bc111fc48a717605f1beea74c4b91d0f2b4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351631"
---
# <a name="detect-system-requirements"></a>检测系统要求
VSPackage 不能作用，除非安装了 Visual Studio。 当您使用 Microsoft Windows 安装程序来管理你的 VSPackage 的安装时，您可以配置要检测是否安装了 Visual Studio 的安装程序。 此外可以配置它检查到系统的其他要求，例如，Windows 的特定版本或特定 RAM 量。

## <a name="detect-visual-studio-editions"></a>检测到 Visual Studio 版本
 若要确定是否安装了 Visual Studio 的版本，请确认的值**安装**注册表项是 *(REG_DWORD) 1*与下表中列出的相应文件夹中。 请注意，Visual Studio 版本的层次结构：

1. 企业

2. Professional

3. 社区

安装较新的版本时，该版本的注册表项还将添加与早期版本。 也就是说，如果安装的 Enterprise edition，则**安装**键设置为*1*企业，以及专业版和社区版本。 因此，您需要检查仅为所需的最新版本。

> [!NOTE]
> 在 64 位版本的注册表编辑器中，32 位密钥下显示**HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\\** 。 Visual Studio 密钥正在**HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing\\** 。

|产品|键|
|-------------|---------|
|Visual Studio Enterprise 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\enterprise|
|Visual Studio Professional 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\professional|
|Visual Studio Community 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\community|
|Visual Studio 2015 Shell （集成和独立）|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell|

## <a name="detect-when-visual-studio-is-running"></a>检测到运行 Visual Studio
 如果 Visual Studio 正在安装 VSPackage 时，不能正确注册你的 VSPackage。 安装程序必须检测到 Visual Studio 运行，且然后拒绝安装程序。 Windows 安装程序不允许您使用表条目来启用此类检测。 相反，必须按如下所示创建自定义操作：使用`EnumProcesses`函数来检测*devenv.exe*处理，然后设置启动条件中使用或有条件地显示一个对话框，提示用户关闭 Visual Studio 的安装程序属性。

## <a name="see-also"></a>请参阅
- [使用 Windows Installer 安装 Vspackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)