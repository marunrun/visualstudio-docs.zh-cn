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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445245"
---
# <a name="detecting-system-requirements"></a>检测系统要求
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage 不能作用，除非安装了 Visual Studio。 当您使用 Microsoft Windows 安装程序来管理你的 VSPackage 的安装时，您可以配置要检测是否安装了 Visual Studio 的安装程序。 此外可以配置它检查到系统的其他要求，例如，Windows 的特定版本或特定 RAM 量。  
  
## <a name="detecting-visual-studio-editions"></a>检测 Visual Studio 版本  
 若要确定是否安装了 Visual Studio 的版本，验证安装注册表项的值是 (REG_DWORD) 1 中相应的文件夹，如下表中列出。 请注意，Visual Studio 版本的层次结构：  
  
1. 企业  
  
2. Professional  
  
3. 社区  
  
   安装的"更高"的版本时，会添加与"低"的版本以及该版本的注册表项。 也就是说，如果安装的 Enterprise edition，则安装密钥设置为 1 企业版、 以及专业版和社区版。 因此需要进行仅检查所需的"最高"版本。  
  
> [!NOTE]
> 在注册表编辑器的 64 位版本，32 位密钥将显示下 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\\。 Visual Studio 键是下 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing\\。  
  
|产品|键|  
|-------------|---------|  
|Visual Studio Enterprise 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\enterprise|  
|Visual Studio Professional 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\professional|  
|Visual Studio Community 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\community|  
|Visual Studio 2015 Shell （集成和独立）|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell|  
  
## <a name="detecting-when-visual-studio-is-running"></a>Visual Studio 运行时检测  
 如果 Visual Studio 正在安装 VSPackage 时，不能正确注册你的 VSPackage。 安装程序必须检测到 Visual Studio 运行，且然后拒绝安装程序。 Windows 安装程序不允许您使用表条目来启用此类检测。 相反，必须按如下所示创建自定义操作：使用`EnumProcesses`函数来检测 devenv.exe 进程，然后可以设置或有条件地启动条件中使用的安装程序属性显示一个对话框，提示用户关闭 Visual Studio。  
  
## <a name="see-also"></a>请参阅  
 [使用 Windows Installer 安装 VSPackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
