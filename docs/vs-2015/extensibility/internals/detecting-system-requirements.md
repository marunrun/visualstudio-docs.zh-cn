---
title: 检测系统要求 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- setup, VSPackages
- launch conditions
ms.assetid: 0ba94acf-bf0b-4bb3-8cca-aaac1b5d6737
caps.latest.revision: 51
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 467554b8e50878bcdf1029e4792bbf168a09fa11
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840407"
---
# <a name="detecting-system-requirements"></a>检测系统要求
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

除非安装了 Visual Studio，否则 VSPackage 无法正常工作。 使用 Microsoft Windows Installer 管理 VSPackage 的安装时，可以配置安装程序以检测是否安装了 Visual Studio。 你还可以将其配置为检查系统中是否有其他要求，例如 Windows 的特定版本或特定数量的 RAM。  
  
## <a name="detecting-visual-studio-editions"></a>检测 Visual Studio 版本  
 若要确定是否安装了 Visual Studio 的版本，请验证 "安装" 注册表项的值是否 (REG_DWORD 相应文件夹中的) 1，如下表所示。 请注意，有一个 Visual Studio 版本的层次结构：  
  
1. Enterprise  
  
2. Professional  
  
3. 社区  
  
   如果安装了 "更高版本"，则会添加该版本的注册表项以及 "较低版本" 的注册表项。 也就是说，如果安装了企业版，则对于 Enterprise 以及专业版和社区版，安装密钥将设置为1。 因此，只需要检查所需的 "最高" 版本。  
  
> [!NOTE]
> 在64位版本的注册表编辑器中，32位密钥显示在 HKEY_LOCAL_MACHINE \SOFTWARE\Wow6432Node 下 \\ 。 Visual Studio 项位于 HKEY_LOCAL_MACHINE \SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing 下 \\ 。  
  
|产品|密钥|  
|-------------|---------|  
|Visual Studio Enterprise 2015|HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\enterprise|  
|Visual Studio Professional 2015|HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\professional|  
|Visual Studio Community 2015|HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\community|  
|Visual Studio 2015 Shell (集成和隔离) |HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell|  
  
## <a name="detecting-when-visual-studio-is-running"></a>检测 Visual Studio 的运行时间  
 如果安装 VSPackage 时正在运行 Visual Studio，则无法正确注册 VSPackage。 安装程序必须在运行 Visual Studio 时进行检测，然后拒绝安装该程序。 Windows Installer 不允许使用表项来启用此类检测。 相反，您必须创建自定义操作，如下所示：使用 `EnumProcesses` 函数检测 devenv.exe 进程，然后设置在启动条件中使用的安装程序属性，或按条件显示一个对话框，提示用户关闭 Visual Studio。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Windows Installer 安装 VSPackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
