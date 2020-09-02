---
title: 在模拟器中运行 Windows Phone 应用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: c7590788-beb3-403c-a7dd-18472a9e585e
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5673ebf28cc652e3bcd973808db87b5bb058659c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683529"
---
# <a name="run-windows-phone-apps-in-the-emulator"></a>在仿真程序中运行 Windows Phone 应用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows Phone 仿真程序提供了一个虚拟环境，你可以在其中调试并测试计算机上的 Windows Phone 应用，而无需使用物理设备。 你可以模拟常用的触摸和旋转事件，还可以选择要模拟的物理屏幕大小和分辨率。 还可以测试许多常用的功能，例如定位、网络、通知、传感器、加速计以及可选的 SD 卡。  
  
 有关可以在模拟器中测试的功能的详细信息，请参阅 [在 Windows Phone 模拟器中测试应用功能](https://msdn.microsoft.com/c1b2b0ec-b8cc-4a98-84c1-701428e45cb1)。  
  
 该仿真程序与 Visual Studio 相结合形成一个完整的环境，从中可设计、开发、调试和测试 Windows Phone 应用。  
  
## <a name="run-a-windows-phone-app-in-the-emulator"></a><a name="BKMK_run"></a> 在模拟器中运行 Windows Phone 应用  
 在开发 Windows Phone 应用时，可使用 Windows Phone 仿真程序来快速部署和测试应用。 然而，建议你在 Windows Phone 应用商店中发布应用之前，先在实际的 Windows Phone 设备上测试该应用。 这可让你像用户那样体验应用。  
  
 当首次在 Windows Phone 仿真程序中运行 Windows Phone 应用时，会发生以下事件：  
  
1. 仿真程序将启动。  
  
2. 仿真程序将加载 Windows Phone 操作系统。  
  
3. 仿真程序将显示 Windows Phone“开始”屏幕。  
  
4. 应用将部署到仿真程序。  
  
5. 应用将在仿真程序上运行。  
  
   若选定的仿真程序已在运行，将部署应用并且该应用将在运行的仿真程序上启动。 每次只能运行每个仿真程序的一个实例。  
  
> [!TIP]
> 若要在仿真程序上测试应用，请在调试会话之间将仿真程序保持为打开状态，以便能够再次快速运行该应用。  
  
### <a name="run-an-app-from-visual-studio"></a><a name="BKMK_vs"></a> 从 Visual Studio 运行应用  
  
##### <a name="to-deploy-and-run-an-app-from-visual-studio"></a>从 Visual Studio 部署并运行应用  
  
1. 在 Visual Studio 中，打开 Windows Phone 项目。  
  
2. 在 " **标准** " 工具栏上，选择一个仿真程序选项。  
  
     ![Windows Phone 仿真程序图像列表](../debugger/media/wp-emulator-list.png "WP_Emulator_list")  
  
3. 若要通过调试部署并运行应用，请在 " **调试** " 菜单上单击 " **启动调试**"，或按 F5。  
  
     若要在不调试的情况下部署和运行应用程序，请在 " **调试** " 菜单上单击 " **启动（不调试**）" 或按 Ctrl + F5。  
  
     已部署并启动你的应用。  
  
     若要在不运行的情况下部署应用，请在 " **生成** " 菜单上单击 " **部署解决方案**"。  
  
##### <a name="to-stop-a-running-app"></a>停止正在运行的应用  
  
- 若要停止正在运行的应用，请执行下列操作之一：  
  
  - 在 Visual Studio 中的 " **调试** " 菜单上，单击 " **停止调试**" 或按 Shift + F5。  
  
  - 在模拟器中，按 " **后退** " 按钮退出应用程序。 如果应用的活动页面不是应用的起始页，则你可能需要多次按 " **后退** " 按钮。  
  
    应用将退出并打开“开始”屏幕。 此操作将结束当前调试会话。  
  
##### <a name="to-restart-an-app-without-debugging"></a>不进行调试而直接重新启动应用  
  
1. 在仿真程序中，在“开始”屏幕上向左滑动以查看应用列表。  
  
2. 在应用列表中，点击应用图标。 应用将不进行调试而直接重新启动。  
  
##### <a name="to-deactivate-a-running-app"></a>停用正在运行的应用  
  
1. 在运行应用之前，在 Visual Studio 中，右键单击 "解决方案资源管理器" 中的项目，然后选择 " **属性** " 以打开 " **项目设计器**"。  
  
2. 在 " **项目设计器**" 的 " **调试** " 页上，如果你希望应用在停用后进入休眠状态，请在 "调试 **时禁用逻辑删除** " 复选框保持未选中状态。 若要在停用应用时将其逻辑删除，请选中该复选框。  
  
3. 在 " **调试** " 菜单上，单击 " **启动调试**"，或按 F5 运行应用。  
  
4. 在模拟器中，按 " **开始** " 按钮。 将显示“开始”屏幕并停用应用。 应用将进入休眠状态或被逻辑删除，具体取决于 "在 **调试时停用时逻辑删除** " 复选框的设置。  
  
##### <a name="to-reactivate-a-dormant-or-tombstoned-app"></a>重新激活处于睡眠状态或被逻辑删除的应用  
  
- 在模拟器中，按 " **后退** " 按钮返回到应用程序。 如果你导航到其他页面或已打开其他应用，你可能需要多次按 " **后退** " 按钮才能重新激活该应用。  
  
     调试会话将会恢复。 如果调试器已从应用分离，你可能需要按 F5 以恢复调试会话。  
  
### <a name="run-an-app-with-the-application-deployment-tool"></a><a name="BKMK_depltool"></a> 使用应用程序部署工具运行应用程序  
 你还可以使用 Windows Phone 应用程序部署工具 (**AppDeploy.exe**) 在模拟器中运行你的应用程序。 该工具为安装 Windows Phone 开发工具时安装的一个独立应用。  
  
 有关详细信息，请参阅 [通过应用程序部署工具部署 Windows Phone 8.1 应用](https://msdn.microsoft.com/library/23700f82-1399-44d9-bc0c-714be4a48ee6)。  
  
## <a name="configure-the-windows-phone-emulator-with-the-emulator-toolbar"></a><a name="BKMK_toolbar"></a> 通过仿真程序工具栏配置 Windows Phone 模拟器  
 此表显示了仿真程序工具栏上可用的配置按钮。  
  
|工具栏按钮|配置选项|  
|---------------------|---------------------------|  
|![Windows Phone 仿真程序工具栏上的输入选项](../debugger/media/wp-emulator.png "WP_Emulator_")|**配置单点或多点输入**<br /><br /> 当启用多点输入时，可右击以移动触摸点，而无需触摸屏幕。 然后你可以左击以同时移动这两个触摸点。|  
|![Windows Phone 仿真程序工具栏上的“方向”](../debugger/media/wp-emulator-rotation.png "WP_Emulator_rotation")|**配置仿真程序的方向**<br /><br /> 可以在 Windows Phone 仿真程序中将方向更改为以下三种方向之一：纵向、横向朝左或横向朝右。 在更改方向时不会更改仿真程序的大小。<br /><br /> 若要更改方向，请单击 " **向左旋转** " 按钮或 " **向右** 旋转" 按钮。|  
|![Windows Phone 仿真程序工具栏上的大小选项](../debugger/media/wp-emulator-size.png "WP_Emulator_size")|**配置仿真程序的大小**<br /><br /> 可以在主机屏幕上更改仿真程序的大小。 仿真程序的每英寸点数 (DPI) 以主机监视器 DPI 为基础，无论缩放值如何。<br /><br /> -若要使仿真程序适合屏幕，请单击 " **适应屏幕** " 按钮。<br />-若要更改缩放设置，请单击 " **缩放** " 按钮。 此时将打开 " **缩放** " 对话框。 在 " **缩放** " 对话框中，输入一个介于33和100之间的缩放值。|  
  
## <a name="use-the-simulated-hardware-buttons-on-the-emulator"></a><a name="BKMK_buttons"></a> 在模拟器上使用模拟的硬件按钮  
 通过使用仿真程序屏幕右侧的模拟的硬件按钮，可模拟手机的硬件按钮的使用。  
  
- 单击 " **电源** " 按钮以模拟关闭和打开显示器。 单击并按住以模拟关闭手机。  
  
- 单击 " **音量 Up** " 或 "调 **低音量** " 按钮以模拟更改手机和通知电话扬声器的音量。  
  
- **相机**按钮用于启动照相机应用。 可使用相机应用中的控件模拟拍摄照片或视频。  
  
  以下屏幕截图显示了模拟的硬件按钮。  
  
1. 左侧图像将在仿真程序上显示“开始”屏幕。  
  
2. 在点击 " **电源** " 按钮后显示仿真程序，以关闭显示器。  
  
3. 右图在点击 "调 **大音量** " 按钮后显示仿真程序屏幕以增加音量。  
  
   ![Windows Phone 仿真程序上的按钮](../debugger/media/wp-emulator-buttons.png "WP_Emulator_buttons")  
  
## <a name="use-the-computer-keyboard-with-the-emulator"></a><a name="BKMK_tasks_kbd"></a> 将计算机键盘与仿真程序一起使用  
 仿真程序支持开发计算机上的硬件键盘在 Windows Phone 键盘上的映射。 键行为与在 Windows Phone 设备中相同。  
  
 默认情况下，不启用硬件键盘。 此实现等效于使用之前必须部署的滑动键盘。 在启用硬件键盘之前，仿真程序只接受控制键的键输入。  
  
 仿真程序不支持本地化版本的 Windows 开发计算机键盘上的特殊字符。 若要输入本地化键盘上显示的特殊字符，请改用软件输入面板 (SIP)。  
  
 若要在仿真程序中使用计算机的键盘，按 PAGE UP 键或 PAUSE/BREAK 键（Windows 8/8.1 仿真程序）或 F4（Windows 10 仿真程序）。  
  
 若要在仿真程序中停止使用计算机的键盘，按 PAGE DOWN 键或 PAUSE/BREAK 键（Windows 8/8.1 仿真程序）或 F4（Windows 10 仿真程序）。  
  
 下表列出了可用于模拟 Windows Phone 上的按钮和其他控件的硬件键盘上的键。  
  
|计算机硬件键|Windows Phone 硬件按钮|备注|  
|---------------------------|-----------------------------------|-----------|  
|F1|BACK|长按可实现预期效果。|  
|F2|START|长按可实现预期效果。|  
|F3|SEARCH||  
|F4|在 Windows 10 仿真程序中，在使用本地计算机的键盘和不使用本地计算机的键盘之间切换。|在 Windows 8/8.1 仿真程序中不适用。|  
|F5|不适用。||  
|F6|CAMERA HALF|半按专用相机按钮。|  
|F7|CAMERA FULL|专用相机按钮。|  
|F8|不适用。||  
|F9|VOLUME UP||  
|F10|VOLUME DOWN||  
|F11|不适用。||  
|F12|POWER|按两次 F12 键可启用锁定屏幕。<br /><br /> 长按可实现预期效果。|  
|Esc|BACK|长按可实现预期效果。|  
|PAUSE/BREAK|切换键盘（仅适用于 windows 8/8.1 仿真程序）。|不适用于 Windows 10 仿真程序。|  
|Page Up|启用硬件键盘（仅适用于 Windows 8/8.1 仿真程序）。|不适用于 Windows 10 仿真程序。|  
|Page Down|禁用硬件键盘（仅适用于 Windows 8/8.1 仿真程序）。|不适用于 Windows 10 仿真程序。|  
  
## <a name="save-and-load-custom-checkpoints"></a><a name="BKMK_checkpoints"></a> 保存并加载自定义检查点  
 使用仿真程序的**其他工具**的 "**检查点**" 选项卡，保存仿真程序状态的快照。 若经常使用相同数据和设置来测试应用，则该功能是有用的。  
  
 例如，如果你的应用需要多个联系人信息，则你可以创建一个联系人记录并保存仿真程序的快照。 否则，你必须在每次启动仿真程序时重建联系人记录。  
  
- 单击 " **新建检查点** "，捕获具有再次测试应用程序所需的数据和设置的仿真程序状态的新快照。 新的检查点将添加到 " **检查点** " 列表中。  
  
   无法在将调试器附加到仿真程序时捕获检查点。  
  
- 在 " **检查** 点" 列表中选择检查点以查看有关检查点的信息。  
  
- 选择 " **默认** " 列中的单选按钮，以使保存的检查点成为活动仿真程序的默认检查点。  
  
- 单击 " **还原** " 以在仿真程序上重新启动 Windows Phone 的操作系统，并加载选定的快照。  
  
- 单击 " **删除** " 可删除不再需要的快照。  
  
  原始仿真程序图像始终显示为 " **检查点** " 列表中的第一项，无法更改或删除。 但是，你可以选择不同的快照作为默认的仿真程序图像。  
  
  ![Windows Phone 仿真程序的“检查点”选项卡](../debugger/media/wp-emulator-checkpoints.png "WP_Emulator_checkpoints")  
  
## <a name="capture-screenshots-in-the-emulator"></a><a name="BKMK_tasks_shot"></a> 在模拟器中捕获屏幕快照  
 通过使用“附加工具”窗口中的屏幕快照工具，可创建 Windows Phone 应用的屏幕快照。 该工具可创建与正在运行的仿真程序的分辨率相匹配的 PNG 文件。  
  
 ![来自 Windows Phone 仿真程序的屏幕快照](../debugger/media/wp-emulator-screenshots.png "WP_Emulator_screenshots")  
  
#### <a name="to-create-an-app-screenshot-by-using-the-built-in-emulator-screenshot-tool"></a>使用内置仿真程序屏幕快照工具创建应用屏幕快照  
  
1. 若要优化屏幕快照的质量，请将仿真程序的缩放级别设置为 100%。 设置的缩放级别越高，屏幕快照的质量越好。  
  
2. 在仿真程序中启动应用。  
  
3. 在模拟器工具栏上，单击展开按钮以打开 " **其他工具** " 窗口。  
  
4. 单击 " **屏幕快照** " 选项卡。  
  
5. 应用准备就绪后，单击 " **捕获** " 按钮。  
  
    屏幕快照将显示在工作区中。  
  
6. 单击 " **保存** " 按钮以打开 " **另存为** " 对话框。  
  
7. 选择所需的位置和 **文件名** ，然后单击 " **保存**"。  
  
8. 或者，导航至应用中的其他页面并捕获其他屏幕快照。  
  
9. 启动具有其他屏幕分辨率的仿真程序，以使用不同的分辨率捕获相同的屏幕快照。 如果在调试情况下运行应用，则必须先停止调试才能在其他仿真程序上再次运行该应用。  
  
   在捕获要提交到 Windows Phone 应用商店的屏幕快照之前，请禁用仿真程序屏幕上的帧速率计数器。  
  
#### <a name="to-disable-frame-rate-counters-in-the-emulator-before-capturing-screenshots"></a>在捕获屏幕快照之前禁用仿真程序中的帧速率计数器  
  
- 在 Visual Studio 中指定发布版本。 指定发布版本后，通过选择 "**生成**" 菜单上的 "**部署" _[应用名称]_ **链接启动你的应用。  
  
- 另外，你可以注释 app.xaml.cs 或 app.xaml.vb 文件中的代码行，以将 `EnableFrameRateCounter` 的值设置为 `true`。
