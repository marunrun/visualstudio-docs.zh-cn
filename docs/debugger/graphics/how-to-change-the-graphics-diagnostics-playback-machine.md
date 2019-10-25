---
title: 如何：更改播放计算机图形诊断 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 1b9aa3ea-29a0-4e21-bc57-936f33537b5c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5a41caf3f866c4a21d0a44fc69932066b2b7d923
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72735049"
---
# <a name="how-to-change-the-graphics-diagnostics-playback-machine"></a>如何：更改图形诊断播放机
您可以使用本地计算机或使用远程计算机或设备播放图形信息。

## <a name="choosing-a-playback-machine"></a>选择播放计算机
 播放计算机是用于播放图形日志中的图形事件的计算机或设备。 通常情况下，本地计算机是最方便的选项，但呈现问题可能不会在其硬件或驱动程序版本与捕获到它的计算机不同的计算机上重现;发生这种情况时，你可以选择一个更好的远程播放计算机，它可以更好地重现问题，并仍使用开发计算机对其进行诊断。

#### <a name="to-use-the-local-machine-to-play-back-graphics-information"></a>使用本地计算机播放图形信息

1. 在图形日志文档窗口中，选择 "**播放计算机**" 链接。 此时将显示 "**远程调试器连接**" 对话框。

2. 在 "**手动配置**" 下的 "**地址**" 属性中，输入 `localhost`。

3. 将 "**身份验证模式**" 属性设置为 "**无**"。

4. 选择“选择”按钮。

#### <a name="to-use-a-remote-machine-to-play-back-graphics-information"></a>使用远程计算机播放图形信息

1. 在图形日志文档窗口中，选择 "**播放计算机**" 链接。 此时将显示 "**远程调试器连接**" 对话框。

2. 在 "**手动配置**" 下的 "**地址**" 属性中，输入要用于播放图形信息的计算机或设备的 Windows 域名或 IP 地址。

3. 指定要用于保护与播放计算机连接的授权类型。

    - 对于 Windows 身份验证，请将 "**身份验证模式**" 属性设置为 " **windows**"。

    - 如果没有身份验证，请将 "**身份验证模式**" 属性设置为 "**无**"。

4. 选择“选择”按钮。

> [!NOTE]
> "**远程调试器连接**" 对话框还可能会显示直接连接到您的开发计算机或位于同一子网上的远程调试目标。 你可以使用其中一个远程调试目标作为图形诊断播放计算机，而无需手动配置它。 在 "**远程调试器连接**" 对话框中，选择所需的目标，然后选择 "**选择**" 按钮。

## <a name="see-also"></a>请参阅
- [图形日志文档](graphics-log-document.md)