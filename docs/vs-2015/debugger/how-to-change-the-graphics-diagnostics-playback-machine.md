---
title: 如何：更改图形诊断播放计算机 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 1b9aa3ea-29a0-4e21-bc57-936f33537b5c
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cb14fb4017ea1df6659b9a1a0ac093cd7cf7e0b1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840599"
---
# <a name="how-to-change-the-graphics-diagnostics-playback-machine"></a>如何：更改图形诊断播放计算机
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以使用本地计算机、远程计算机或设备播放图形信息。  
  
## <a name="choosing-a-playback-machine"></a>选择播放计算机  
 播放计算机是用于播放图形日志中的图形事件的计算机或设备。 通常情况下，本地计算机是最方便的选项，但呈现问题可能不会在具有与捕获到它的计算机不同的硬件或驱动程序版本的计算机上重现；发生这种情况时，你可以选择远程播放计算机，它可以更好地重现问题，并仍使用开发计算机对其进行诊断。  
  
#### <a name="to-use-the-local-machine-to-play-back-graphics-information"></a>使用本地计算机播放图形信息  
  
1. 在“图形日志”文档窗口中，选择“播放计算机”链接。 此时将显示“远程调试器连接”对话框。  
  
2. 在“手动配置”下的“地址”属性中，输入 `localhost` 。  
  
3. 将“身份验证模式”属性设置为“无” 。  
  
4. 选择“选择”按钮。  
  
#### <a name="to-use-a-remote-machine-to-play-back-graphics-information"></a>使用远程计算机播放图形信息  
  
1. 在“图形日志”文档窗口中，选择“播放计算机”链接。 此时将显示“远程调试器连接”对话框。  
  
2. 在“手动配置”下的“地址”属性中，输入要用于播放图形信息的计算机或设备的 Windows 域名或 IP 地址 。  
  
3. 指定要用于保护播放计算机的连接的授权类型。  
  
    - 对于 Windows 身份验证，请将“身份验证模式”属性设置为“Windows” 。  
  
    - 对于无身份验证，请将“身份验证模式”属性设置为“无” 。  
  
4. 选择“选择”按钮。  
  
> [!NOTE]
> “远程调试器连接”对话框还可能显示直接连接到开发计算机或位于同一子网上的远程调试目标。 你可以使用其中一个远程调试目标作为图形诊断播放计算机，而无需手动配置它。 在“远程调试器连接”对话框中，选择所需的目标，然后选择“选择”按钮 。  
  
## <a name="see-also"></a>另请参阅  
 [图形日志文档](../debugger/graphics-log-document.md)
