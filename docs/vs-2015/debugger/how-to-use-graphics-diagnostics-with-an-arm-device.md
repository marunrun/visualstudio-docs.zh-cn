---
title: 如何：将图形诊断用于 ARM 设备 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 346fd3c0-9e92-4ab8-bb3b-1aa9000a2483
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5bbe12449849b656af2658c5bab667b0e611515e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685864"
---
# <a name="how-to-use-graphics-diagnostics-with-an-arm-device"></a>如何：使用图形诊断和 ARM 设备
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

图形诊断支持在运行 Windows RT 8.1 或 Windows Phone 8.1 的基于 ARM 的设备上远程调试 Direct3D 应用。 你可以在 Direct3D 应用在设备上运行时从该应用中捕获图形信息，或将设备用作之前捕捉到的图形信息的播放计算机。  
  
## <a name="using-graphics-diagnostics-with-an-arm-based-device"></a>将图形诊断用于基于 ARM 的设备  
 因为 Visual Studio 不在基于 ARM 的设备上运行，所以你必须使用远程调试器才能分析在这些设备上运行的应用。 远程调试器支持图形捕获和播放，以便你可以在这些设备上诊断呈现错误并评估图形性能，该操作与在这些设备上调试应用一样轻松。  
  
 若要使用图形诊断功能，请先在你的设备上启用远程调试。  
  
#### <a name="to-enable-remote-debugging-on-your-arm-based-device"></a>在基于 ARM 的设备上启用远程调试  
  
1. 在基于 ARM 的设备上安装 [Arm 工具包策略](https://msdn.microsoft.com/windows/desktop/dn469188) 。  
  
2. 在基于 ARM 的设备上安装 [远程调试工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015) 。  
  
> [!IMPORTANT]
> 对于 Windows Phone 8.1 设备，你可能需要注册手机以供开发。 为此，你必须是已注册的开发人员。 有关详细信息，请参阅 [如何为 Windows Phone 8 部署和运行应用](https://msdn.microsoft.com/library/windowsphone/develop/ff402565.aspx)。  
  
 在设备上启用了远程调试后，请将它作为你的调试目标并启动图形诊断。  
  
#### <a name="to-configure-and-start-graphics-diagnostics-on-your-device"></a>在设备上配置和启动图形诊断  
  
1. 在 " **解决方案平台** " 下拉列表中，选择 " **arm** "，以便将基于 ARM 的设备作为远程调试目标提供。  
  
2. 在 " **调试目标** " 下拉列表中，选择 "ARM 设备"。  
  
3. 在菜单上，选择 " **调试**"、" **图形**"、" **启动诊断**"。 （键盘：Alt+F5）  
  
## <a name="see-also"></a>另请参阅  
 [在远程计算机上运行 Windows 应用商店应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)   
 [如何：更改图形诊断播放计算机](../debugger/how-to-change-the-graphics-diagnostics-playback-machine.md)
