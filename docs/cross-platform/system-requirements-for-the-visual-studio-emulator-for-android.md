---
title: 适用于 Android 的 Visual Studio 模拟器的系统要求 | Microsoft Docs
ms.custom: ''
ms.prod: visual-studio-dev15
ms.date: 11/04/2016
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 35e766ad-269f-41e4-ba23-74a556c315f3
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f1462769a4ba9929a000bca998c1fe3708908798
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77272054"
---
# <a name="system-requirements-for-the-visual-studio-emulator-for-android"></a>适用于 Android 的 Visual Studio 仿真程序的系统要求

适用于 Android 的 Visual Studio 仿真程序在 Hyper-V（Windows 8 及以上版本的虚拟化技术）上作为虚拟机运行。 要运行仿真器，计算机必须满足本主题中所述的 Hyper-V 运行要求。

安装程序在安装仿真器时尝试以静默方式配置这些先决条件。 安装程序成功配置这些先决条件后，仿真器即会按预期方式工作。 否则，可能需要手动实现这些先决条件。 如果必须手动配置这些先决条件，则步骤和工具与 [此处](/previous-versions/windows/apps/jj863509\(v=vs.105\)) 所述的针对 Windows Phone 仿真器的步骤相同。

> [!IMPORTANT]
> 仿真器的安装程序会检查运行 Visual Studio Emulator for Android 的先决条件。 如果先决条件不存在将显示警告，但并不需要这些条件。

## <a name="Checklist"></a> 快速清单

以下是 Visual Studio Emulator for Android 运行要求的快速清单。 有关更多详细信息，请参阅本主题的后续章节。

系统要求

- Hyper-V 支持（请参阅下面的 Hyper-V 要求）

- 6 GB 或 6 GB 以上的 RAM。

- Windows 8、Windows 8.1、Windows 10 或更高版本的 64 位专业版

- 支持 SSSE3 或更高版本的处理器。

网络要求

- DHCP

- 自动配置的 DNS 和网关设置

Hyper-V 要求

- 在 BIOS 中，必须支持以下功能：

  - 硬件辅助虚拟化

  - 第二级别的地址转换 (SLAT)

  - 基于硬件的数据执行保护 (DEP)

- 在 Windows 中，必须启用并运行 Hyper-V。

- 你需要成为本地 Hyper-V 管理员组的成员。

## <a name="system-requirements"></a>系统要求
 计算机必须满足以下要求：

- Hyper-V 支持（请参阅 [Hyper-V 要求](#hyper-v-requirements)）

- 6 GB 或 6 GB 以上的 RAM。

- Windows 8、Windows 8.1、Windows 10 或更高版本的 64 位专业版。

要检查 RAM 和 Windows 的要求，请在“控制面板”中选择“系统和安全”，然后选择“系统”。

![验证系统要求](../cross-platform/media/android_emu_system_requirements.png "Android_Emu_System_Requirements")

## <a name="network-requirements"></a>网络要求

网络必须满足以下要求：

- DHCP

   仿真程序需要 DHCP，因为它将自身配置为网络上具有自己的 IP 地址的一个单独的设备。

- 自动配置的 DNS 和网关设置

   无法为仿真程序手动配置 DNS 和网关设置。

  要对仿真器中的网络问题进行故障排除，请参阅以下主题：

- [Troubleshooting the Visual Studio Emulator for Android](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)

## <a name="hyper-v-requirements"></a>Hyper-V 要求

BIOS 中的 Hyper-V 要求

计算机的 BIOS 必须支持下列要求，且必须实现这些要求：

- 硬件辅助虚拟化

- 第二级别的地址转换 (SLAT)

- 基于硬件的数据执行保护 (DEP)

Windows 中的 Hyper-V 要求

当计算机和 BIOS 设置已配置为支持 Hyper-V 时，安装程序会启用并启动 Hyper-V。 否则，可能需要手动实现这些要求。

|需求|如何检查并实现此要求|
|-----------------|----------------------------------------------|
|必须安装 Hyper-V|按照用于 [为 Windows Phone 仿真程序启用 Hyper-V](/previous-versions/windows/apps/jj863509(v=vs.105))相同说明操作。<br /><br /> 检查服务管理单元中的 **Hyper-V 虚拟机管理** 服务的状态。|
|必须正在运行 Hyper-V。|有关管理服务的详细信息，请参阅以下主题：<br /><br /> -   [启动、停止、暂停、继续或重新启动服务](https://technet.microsoft.com/library/cc736564\(v=WS.10\).aspx)<br />-   [配置服务启动方式](https://technet.microsoft.com/%20library/cc739213\(v=ws.10\))|

 你需要成为本地 Hyper-V 管理员组的成员。

 要在运行 Visual Studio Emulator for Android 时不收到提升权限的定期提示，你需要成为本地 Hyper-V 管理员组的成员。 如果你在安装 SDK 时已经是计算机上的本地管理员，则 SDK 的安装程序会将你添加到 Hyper-V 管理员组。 否则，可能需要手动实现此要求。

 运行仿真器时，如果你还不是 Hyper-V 管理员组的成员，则系统会提示你加入该组（对话框针对的是 Windows Phone 仿真器）。 加入组需要管理员权限。

> [!IMPORTANT]
> 加入该组后，注销或重启以使更改生效。

 ![加入 Hyper&#45;V 管理员安全组](../cross-platform/media/android_emu_hyperv_admin.png "Android_Emu_HyperV_Admin")

 要手动将自己添加到组中，请打开本地用户和组管理单元。

## <a name="running-the-emulator-from-a-bootable-vhd-is-not-supported"></a>不支持从可启动 VHD 运行仿真器
 从可启动 VHD 运行 Windows 时，如果尝试在 Visual Studio Emulator for Android 上运行应用，则仿真器通常需要几分钟时间才能启动，或会启动失败。 当仿真器启动失败时，你将看到以下消息：应用部署失败。 请重试。

 此配置不受支持。 有关相关问题的信息，请参阅[适用于 Android 的 Visual Studio 模拟器疑难解答](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)。

## <a name="hyper-v-requires-uncompressed-and-unencrypted-files"></a>Hyper-V 需要未经压缩且未经加密的文件
 在配置了 NTFS 文件系统的硬盘上，Hyper-V 使用的虚拟硬盘文件必须是未经压缩且未经加密的。 请确保不要压缩或加密以下目录：

- %localappdata%\Microsoft\XDE

- C:\Program Files (x86)\Microsoft Emulator Manager

- C:\Program Files (x86)\Microsoft Visual Studio Emulator for Android

- %localappdata%\Microsoft\VisualStudioEmulator

在 ReFS 文件系统上，虚拟硬盘文件不能设置完整性位。

## <a name="hardware-graphics-forwarding-opengl-es-support-requirements"></a>硬件图形转发（OpenGL ES 支持）要求

为了让仿真器能够仿真对 GPU 的调用（例如 OpenGL ES 使用的那些调用），计算机必须具有兼容 DirectX 的 GPU 且安装了合适的 DirectX 驱动程序。

## <a name="see-also"></a>另请参阅

- [适用于 Android 的 Visual Studio 模拟器疑难解答](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)
