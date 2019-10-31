---
title: 在模拟器中运行 Windows 应用商店应用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 81b69bf8-ec87-4bb6-9ad4-1fa7b7802d16
caps.latest.revision: 45
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 96224b522b17ff9da520386d56d4fae7a04bd981
ms.sourcegitcommit: bdccab4c2dbd50ea8adaaf88c69c9ca32db88099
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73144774"
---
# <a name="run-windows-store-apps-in-the-simulator"></a>在模拟器中运行 Windows 应用商店应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的 Windows 应用商店应用程序模拟器是一个桌面应用程序，可模拟 Windows 应用商店应用程序。 你可以在开发计算机上运行应用程序并模拟常用的触摸和旋转事件。 此外，可以选择想要仿真和模拟网络连接属性的物理屏幕大小和分辨率。  
  
 模拟器提供可以在其中设计、开发、调试和测试 Windows 应用商店应用的环境。 但是，将应用发布到 Windows 应用商店之前，应在真实设备上测试应用。  
  
 Visual Studio 的 Windows 应用商店应用程序模拟器并非运行在本地计算机上的某个隔离环境中。 因此，模拟器中发生的错误（如不可恢复的系统范围错误）也会影响整个计算机。  
  
 有关 Windows Phone 的信息，请参阅 [Run Windows Phone apps in the emulator](../debugger/run-windows-phone-apps-in-the-emulator.md) 。  
  
> [!IMPORTANT]
> Visual Studio 2015 模拟器不包括地理位置按钮。 这是因为 Windows 10 模拟器中不包含地理位置模拟。 如果需要进行这种类型的模拟，则可以在 Windows 8.1 或更早的操作系统上使用 Visual Studio 2013 模拟器。  
  
## <a name="BKMK_Set_the_simulator_as_the_target"></a> 设置模拟器作为目标  
 若要在模拟器中运行 Windows 应用商店应用程序，请从调试器的 **“标准”** 工具栏上的 **“启动调试”** 按钮旁的下拉列表中选择 **“模拟器”** 。  
  
 ![在模拟器中运行](../debugger/media/vsrun-f5-simulator.png "VSRUN_F5_Simulator")  
  
## <a name="BKMK_Choose_an_interaction_mode"></a> 选择交互模式  
 可以选择下列交互模式  
  
- ![鼠标模式按钮](../debugger/media/simulator-mousemodebtn.png "SIMULATOR_MouseModeBtn")鼠标模式：将交互模式设置为鼠标手势。 鼠手势包括单击、双击和拖动。  
  
- "![启动触摸仿真" 按钮](../debugger/media/simulator-starttouchemulationbtn.png "SIMULATOR_StartTouchEmulationBtn")启动触摸仿真：将交互模式设置为单指的触摸手势。 单指事件包括点击、拖动和轻扫。  
  
     ![模拟器一个 finger 目标](../debugger/media/simulator-onefinger.png "SIMULATOR_OneFinger")单个目标图标指示事件在模拟器中的位置。 使用鼠标为指针定位。  
  
     ![单指触控目标](../debugger/media/simulator-onefingerengaged.png "SIMULATOR_OneFingerEngaged")按鼠标左键以激活触摸模式。 例如，单击按钮以模拟点击，或按住该按钮以模拟拖动或轻扫。  
  
## <a name="pinch-and-zoom"></a>捏合与缩放  
 将交互模式设置为双指的捏合与缩放手势。  
  
- ![模拟器双指目标](../debugger/media/simulator-twofinger.png "SIMULATOR_TwoFinger")  

  - 双目标图标指示双指在设备屏幕上的位置。  

  - 移动鼠标以将图标放置在设备屏幕上的对象上。  

  - 在捏合或缩放之前，向前或向后滚动鼠标滚轮以更改双指的模拟距离。  

- ![缩小、缩放和旋转目标](../debugger/media/simulator-twofingerengaged.png "SIMULATOR_TwoFingerEngaged")  

  - 按左键并向后旋转滚轮（朝向你）以缩小（捏合）。  

  - 按左键并向前旋转鼠标滚轮（远离你）以放大（缩放）。  
  
## <a name="object-rotation"></a>对象旋转  
 “触摸仿真旋转”按钮将交互模式设置为使用双指的旋转手势。  
  
- 移动鼠标以将图标放置在设备屏幕上的对象上。  
  
  - 在旋转对象之前，向前或向后滚动鼠标滚轮以更改双指的模拟方向。  

- 按左键并向后旋转滚轮（朝向你）以逆时针旋转对象。 在旋转鼠标滚轮时，两个目标图标中的一个围绕另一个旋转以指示旋转的相对大小。  

  - 按左键并向前旋转鼠标滚轮（远离你）以顺时针旋转对象。  

## <a name="BKMK_Enable_or_disable_Always_on_top_mode"></a> 启用或禁用“总在最前面”模式  
 可将模拟器窗口设置为始终位于其他窗口之上。 “切换最顶端窗口”按钮启用或禁用模拟器窗口的“总在最前面” 模式。  
  
## <a name="BKMK_Change_the_device_orientation"></a> 更改设备方向  
 可通过以任意方向将模拟器旋转 90 度，在纵向与横向之间切换设备方向。  
  
> [!NOTE]
> 模拟器不遵从项目的 [DisplayProperties.AutoRotationPreferences](https://go.microsoft.com/fwlink/?LinkId=249460) 属性。 例如，如果项目将方向设置为 `Landscape`，然后将模拟器的方向旋转至纵向，则模拟器显示的图像仍将经过旋转和调整大小。 请在真实设备上测试这些设置。  
  
> [!NOTE]
> 如果旋转模拟器，并因此使模拟器的一个边大于显示模拟器的屏幕，则自动调整模拟器大小以适合屏幕。 如果再次旋转模拟器，也不会将大小调整回其原始大小。  
  
## <a name="BKMK_Change_the_simulated_screen_size_and_resolution"></a> 更改模拟屏幕的大小和分辨率  
 若要更改模拟屏幕的大小和分辨率，请选择调色板上的 “更改分辨率”按钮，然后从列表中选择新的大小和分辨率。  
  
 屏幕的大小和分辨率以 *屏幕宽度（以英寸为单位）、像素宽度 X 像素高度*形式列出。 注意，同时模拟屏幕大小和分辨率。 模拟器上的位置坐标将转换为所选设备大小和分辨率的坐标。  
  
> [!NOTE]
> 可在应用程序中保存位图的缩放版本，而 Windows 将加载适合当前比例的图像。 有关详细信息，请参见 [响应式设计 101](https://msdn.microsoft.com/library/windows/apps/dn958435.aspx)。 但是，如果更改模拟器分辨率，以使 Windows 选取不同图像以适合该分辨率，则必须停止再重新启动调试会话才能查看新图像。  
  
## <a name="BKMK_Capture_a_screenshot_of_your_app_for_submission_to_the_Microsoft_Store"></a> 捕获应用程序的屏幕快照以提交到 Windows 应用商店  
 向 Windows 应用商店提交应用时，必须包含该应用的屏幕快照。  
  
> [!NOTE]
> 屏幕快照按模拟器的当前分辨率进行保存。 若要更改分辨率，请选择 **“更改分辨率”** 按钮。  
  
- 若要从模拟器创建应用程序的屏幕快照，请选择 **“将屏幕快照捕获到剪贴板”** 按钮。  
  
- 若要设置屏幕快照所在的位置，请选择 “屏幕快照设置”按钮，然后从快捷菜单中选择该位置。  
  
     ![屏幕截图设置上下文菜单](../debugger/media/simulator-screenshotsettingscntxmnu.png "SIMULATOR_ScreenShotSettingsCntxMnu")  
  
## <a name="BKMK_Simulate_network_connection_properties"></a> 模拟网络连接属性  
 你可以通过维护感知网络连接成本或数据计划状态更改的能力并允许你的应用程序使用此信息避免产生额外的漫游成本或超出指定的数据传输限制，来帮助你的应用程序用户管理所测量网络连接的成本。 利用 [Windows.Networking.Connectivity](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.aspx) API 能够对签名的 [NetworkStatusChanged](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.networkinformation.networkstatuschanged.aspx) 和 [TriggerType](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.background.systemtrigger.triggertype.aspx) 事件作出响应。 请参见 [快速入门：管理按流量计费的网络成本约束](https://msdn.microsoft.com/library/windows/apps/Hh750310.aspx)。  
  
 若要调试或测试网络成本感知代码，可使用模拟器模拟通过 [GetInternetConnectionProfile](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectionprofile.aspx) 返回的 [ConnectionProfile](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.networkinformation.getinternetconnectionprofile.aspx)对象公开的网络的属性。  
  
 若要模拟网络属性，请执行以下操作：  
  
1. 在模拟器工具栏上，选择 “更改网络属性”按钮。  
  
2. 在 “设置网络属性”对话框中，选择“使用模拟网络属性”。  
  
    清除复选框以移除模拟并返回到当前连接的接口的网络属性。  
  
3. 输入模拟网络的 **“配置文件名”** 。 建议使用可以用于标识 [ConnectionProfile](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectionprofile.profilename.aspx) 对象的 [ProfileName](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectionprofile.aspx) 属性中的模拟的唯一名称。  
  
4. 选择 [NetworkCostType](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.networkcosttype.aspx) 列表中的配置文件的 **NetworkCostType** 值。  
  
5. 从 “数据限制状态标志”列表中，你可以将 [ApproachingDataLimit](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectioncost.approachingdatalimit.aspx) 属性或 [OverDataLimit](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectioncost.overdatalimit.aspx)属性设为 true，也可以选择 “在数据限制内”将这两个值均设为 false。  
  
6. 从 “漫游状态”列表中，设置 [Roaming](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectioncost.roaming.aspx) 属性。  
  
7. 选择“设置属性” ，通过触发前台 [NetworkStatusChanged](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.networkinformation.networkstatuschanged.aspx) 事件和 [NetworkStateChange](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.background.systemtrigger.aspx) 类型的后台 **SystemTrigger**来模拟网络属性。  
  
   **有关管理网络连接的详细信息**  
  
   [快速入门：管理按流量计费的网络成本约束](https://msdn.microsoft.com/library/windows/apps/Hh750310.aspx)  
  
   [网络信息示例](https://code.msdn.microsoft.com/windowsapps/Network-Information-Sample-63aaa201)  
  
   [分析能量使用情况](../profiling/analyze-energy-use-in-store-apps.md)  
    
   [Windows.Networking.Connectivity](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.aspx)  
  
   [如何通过后台任务响应系统事件](https://msdn.microsoft.com/f7c86e86-a7ae-4abb-a923-76b03337a80a)  
  
   [如何在 Windows 应用商店应用中触发挂起、继续和后台事件](https://msdn.microsoft.com/library/windows/apps/hh974425.aspx)  
  
## <a name="BKMK_Navigate_the_simulator_with_the_keyboard"></a> 用键盘在模拟器中导航  
 通过按 **CTRL+ALT+向上箭头** 将焦点从模拟器窗口切换到模拟器工具栏上，导航模拟器工具栏。 使用 **向上键头** 和 **向下键头** 在工具栏按钮之间移动。  
  
 可以通过按 **CTRL+ALT+F4**来关闭模拟器。  
  
## <a name="see-also"></a>请参阅  
 [从 Visual Studio 运行应用](../debugger/run-store-apps-from-visual-studio.md)
