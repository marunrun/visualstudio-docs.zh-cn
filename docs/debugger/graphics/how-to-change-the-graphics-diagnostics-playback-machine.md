---
title: 如何：更改图形诊断播放机 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 1b9aa3ea-29a0-4e21-bc57-936f33537b5c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd1f893874a9b0cfe1c7cd36f8e0bb1c38beaca1
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388569"
---
# <a name="how-to-change-the-graphics-diagnostics-playback-machine"></a>如何：更改图形诊断播放计算机
使用本地计算机，或使用远程计算机或设备，你可以播放图形信息。

## <a name="choosing-a-playback-machine"></a>选择播放计算机
 播放计算机是在计算机或用于播放图形日志中的图形事件的设备。 通常情况下，在本地计算机是最方便的选项，但呈现问题可能不会捕获其中; 具有不同的硬件或驱动程序版本计算机的计算机上重现在此情况下，可以选择更好地重现问题的远程播放计算机并仍使用你的开发计算机进行诊断。

#### <a name="to-use-the-local-machine-to-play-back-graphics-information"></a>若要使用本地计算机播放图形信息

1. 在图形日志文档窗口中，选择**播放机**链接。 **远程调试器连接**对话框随即出现。

2. 下**手动配置**，在**地址**属性中，输入`localhost`。

3. 设置**身份验证模式**属性设置为**None**。

4. 选择“选择”按钮。

#### <a name="to-use-a-remote-machine-to-play-back-graphics-information"></a>若要使用远程计算机播放图形信息

1. 在图形日志文档窗口中，选择**播放机**链接。 **远程调试器连接**对话框随即出现。

2. 下**手动配置**，在**地址**属性，输入 Windows 域名或 IP 地址的计算机或你想要用于播放图形信息的设备。

3. 指定想要用于保护与播放计算机的连接的授权类型。

    - 对于 Windows 身份验证设置**身份验证模式**属性设置为**Windows**。

    - 对于无身份验证设置**身份验证模式**属性设置为**None**。

4. 选择“选择”按钮。

> [!NOTE]
> **远程调试器连接**对话框还可能显示直接连接到你的开发计算机或同一子网的远程调试目标。 您可以使用远程调试目标： 作为图形诊断播放计算机无需手动配置。 在中**远程调试器连接**对话框框中，选择您想，然后选择的目标**选择**按钮。

## <a name="see-also"></a>请参阅
- [图形日志文档](graphics-log-document.md)