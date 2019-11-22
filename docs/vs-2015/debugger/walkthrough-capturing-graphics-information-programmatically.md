---
title: 'Walkthrough: Capturing Graphics Information Programmatically | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: a5adeff9-afaf-4047-b5ce-ef0aefe710eb
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 54097420fd212ec9057f4a968e2c6d5de199e56e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74296902"
---
# <a name="walkthrough-capturing-graphics-information-programmatically"></a>演练：以编程方式捕获图形信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 图形诊断以编程方式从 Direct3D 应用中捕获图形信息。  
  
 编程捕获在以下方案中非常有用：  
  
- 当图形应用不使用存在的交换链时（例如当它呈现为纹理时），开始以编程方式捕获。  
  
- 当应用不呈现任何内容时（例如当它使用 DirectCompute 来执行计算时），开始以编程方式捕获。  
  
- 当在手动测试中难以预计和捕获呈现问题，但可用通过使用有关运行时的应用状态信息以编程方式预测呈现问题时，调用 `CaptureCurrentFrame`。  
  
## <a name="CaptureDX11_2"></a> Windows 8.1 中的编程捕获  
 本部分演练演示了在 Windows 8.1 上使用 DirectX 11.2 API 的应用中的编程捕获，它使用可靠捕获方法。 有关如何在 Windows 8.0 系统计算机上使用更早版的 DirectX 的应用中使用编程捕获的信息，请参阅本演练后面的 [Programmatic capture in Windows 8.0 and earlier](#CaptureDX11_1) 。  
  
 本部分显示如何完成这些任务：  
  
- 准备你的应用以使用编程捕获  
  
- 获取 IDXGraphicsAnalysis 接口  
  
- 捕获图形信息  
  
> [!NOTE]
> 以前的编程捕获的实现依赖于 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的远程工具提供捕获功能，但 Windows 8.1 直接通过 Direct3D 11.2 支持捕获。 因此，你不再需要在 Windows 8.1 上安装用于编程捕获的远程工具。  
  
### <a name="preparing-your-app-to-use-programmatic-capture"></a>准备你的应用以使用编程捕获  
 若要在应用中使用编程捕获，它必须包括必要的标头。 这些标头属于 Windows 8.1 SDK。  
  
##### <a name="to-include-programmatic-capture-headers"></a>包括编程捕获标头  
  
- 将这些标头包含在你要在其中定义 IDXGraphicsAnalysis 接口的源文件中：  
  
    ```  
    #include <DXGItype.h>  
    #include <dxgi1_2.h>  
    #include <dxgi1_3.h>  
    #include <DXProgrammableCapture.h>  
    ```  
  
    > [!IMPORTANT]
    > Do not include the header file vsgcapture.h—which supports programmatic capture on Windows 8.0 and earlier—to perform programmatic capture in your Windows 8.1 apps. 此标头无法与 DirectX 11.2 兼容。 If this file is included after the d3d11_2.h header is included, the compiler issues a warning. If vsgcapture.h is included before d3d11_2.h, the app will not start.  
  
    > [!NOTE]
    > 如果你的计算机上安装了 DirectX SDK（2010 年 6 月），并且你的项目的包括路径包含 `%DXSDK_DIR%includex86`，请将它移动到包括路径末尾。 针对你的库路径执行相同操作。  
  
#### <a name="windows-phone-81"></a>Windows Phone 8.1  
 Because the Windows Phone 8.1 SDK doesn't include the DXProgrammableCapture.h header, you'll need to define the `IDXGraphicsAnalysis` interface yourself so that you can use the `BeginCapture()` and `EndCapture()` methods. 包括上一节中所述的其他标头。  
  
###### <a name="to-define-the-idxgraphicsanalysis-interface"></a>定义 IDXGraphicsAnalysis 接口  
  
- 在与你包括头文件的相同文件中定义 IDXGraphicsAnalysis 接口。  
  
  ```  
  interface DECLSPEC_UUID("9f251514-9d4d-4902-9d60-18988ab7d4b5") DECLSPEC_NOVTABLE  
  IDXGraphicsAnalysis : public IUnknown  
  {  
      STDMETHOD_(void, BeginCapture)() PURE;  
      STDMETHOD_(void, EndCapture)() PURE;  
  };  
  ```  
  
  为了方便起见，你可以在一个新的头文件中执行这些步骤，然后将其包括到应用中需要它的位置上。  
  
### <a name="getting-the-idxgraphicsanalysis-interface"></a>获取 IDXGraphicsAnalysis 接口  
 在可以从 DirectX 11.2 中捕获图形信息之前，你必须获取 DXGI 调试接口。  
  
> [!IMPORTANT]
> When using programmatic capture, you must still run your app under graphics diagnostics (Alt+F5 in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]) or under the [Command-Line Capture Tool](../debugger/command-line-capture-tool.md).  
  
##### <a name="to-get-the-idxgraphicsanalysis-interface"></a>获取 IDXGraphicsAnalysis 接口  
  
- 请使用以下代码挂钩 DXGI 调试接口的 IDXGraphicsAnalysis 接口。  
  
    ```  
    IDXGraphicsAnalysis* pGraphicsAnalysis;  
    HRESULT getAnalysis = DXGIGetDebugInterface1(0, __uuidof(pGraphicsAnalysis), reinterpret_cast<void**>(&pGraphicsAnalysis));  
    ```  
  
     请务必检查由 `HRESULT` 返回的 `DXGIGetDebugInterface1` ，以确保在使用它之前获得一个有效的接口：  
  
    ```  
    if (FAILED(getAnalysis))  
    {  
        // Abort program or disable programmatic capture in your app.  
    }  
    ```  
  
    > [!NOTE]
    > 如果在 `DXGIGetDebugInterface1` 返回 `E_NOINTERFACE` （`error: E_NOINTERFACE No such interface supported`），请确保应用在图形诊断下运行（ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中的 Alt + F5）。  
  
### <a name="capturing-graphics-information"></a>捕获图形信息  
 现在你已拥有一个有效的 `IDXGraphicsAnalysis` 接口，你可以使用 `BeginCapture` 和 `EndCapture` 捕获图形信息。  
  
##### <a name="to-capture-graphics-information"></a>捕获图形信息  
  
- 若要开始捕获图形信息，请使用 `BeginCapture`：  
  
    ```  
    ...  
    pGraphicsAnalysis->BeginCapture();  
    ...  
    ```  
  
     调用 `BeginCapture` 后捕获会立即开始；它不会等待下一帧开始。 显示当前帧或调用 `EndCapture`后，捕获将停止：  
  
    ```  
    ...  
    pGraphicsAnalysis->EndCapture();  
    ...  
    ```  
  
## <a name="CaptureDX11_1"></a> Programmatic capture in Windows 8.0 and earlier  
 本部分演练演示了在使用 DirectX 11.1 API 的 Windows 8.0 及更早版本的应用中的编程捕获，它使用旧版捕获方法。 有关如何在 Windows 8.1 系统计算机上使用 DirectX 11.2 的应用中使用编程捕获的信息，请参阅本演练前面的 [Windows 8.1 中的编程捕获](#CaptureDX11_2) 。  
  
 本部分将显示以下任务：  
  
- 准备你的计算机以使用编程捕获  
  
- 准备你的应用以使用编程捕获  
  
- 配置图形日志文件的名称和位置  
  
- 使用 `CaptureCurrentFrame` API  
  
### <a name="preparing-your-computer-to-use-programmatic-capture"></a>准备你的计算机以使用编程捕获  
 编程捕获 API 使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的远程工具来提供捕获功能。 将运行应用的计算机必须安装远程工具，即使你要在本地计算机上使用编程捕获也是如此。 在本地计算机上执行编程捕获时，不必运行[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
 若要在正在计算机上运行的应用中使用远程捕获 API，首先，你必须在该计算机上安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的远程工具。 不同版本的远程工具支持不同的硬件平台。 有关如何安装远程工具的信息，请参阅 Microsoft 下载网站上的 [远程工具下载页](https://go.microsoft.com/fwlink/p/?LinkId=246691) 。  
  
 或者， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将安装必需的组件来为 32 位应用执行远程捕获。  
  
> [!NOTE]
> 因为对于 ARM 设备，大多数 Windows 桌面应用（包括 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]）在 [!INCLUDE[win8](../includes/win8-md.md)] 上不受支持，因此将 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的远程工具和编程捕获 API 结合使用是在 ARM 设备上捕获图形诊断的唯一方法。  
  
### <a name="preparing-your-app-to-use-programmatic-capture"></a>准备你的应用以使用编程捕获  
 若要使用图形诊断工具，首先，你必须捕获它所依赖的图形信息。 通过使用 `CaptureCurrentFrame` API，可采用编程方式捕获该信息。  
  
##### <a name="to-prepare-your-app-to-capture-graphics-information-programmatically"></a>准备你的应用以采用编程方式捕获图形信息  
  
1. 确保 `vsgcapture.h` 标头包含在应用的源代码中。 它可能仅包含在一个位置中（例如，位于你将在其中调用编程捕获 API 的源代码文件中）或者包含在预编译的头文件中，以从多个源代码文件中调用 API。  
  
2. 在应用的源代码中，无论何时你想要捕获当前帧的其余部分，都请调用 `g_pVsgDbg->CaptureCurrentFrame()`。 此方法无需参数且不会返回值。  
  
### <a name="configuring-the-name-and-location-of-the-graphics-log-file"></a>配置图形日志文件的名称和位置  
 图形日志在由 `DONT_SAVE_VSGLOG_TO_TEMP` 和 `VSG_DEFAULT_RUN_FILENAME` 宏定义的位置中创建。  
  
##### <a name="to-configure-the-name-and-location-of-the-graphics-log-file"></a>配置图形日志文件的名称和位置  
  
- 若要阻止将图形日志写入临时目录，请在 `#include <vsgcapture.h>` 行之前添加以下内容：  
  
  ```  
  #define DONT_SAVE_VSGLOG_TO_TEMP  
  ```  
  
   你可以定义此值，以将图形日志写入与工作目录相关的位置，或者如果 `VSG_DEFAULT_RUN_FILENAME` 的定义是绝对路径，则写入绝对路径。  
  
- 若要将图形日志保存到不同位置，或向其提供不同的文件名，请在 `#include <vsgcapture.h>` 行之前添加以下内容：  
  
  ```  
  #define VSG_DEFAULT_RUN_FILENAME <filename>  
  ```  
  
   如果你不执行此步骤，则文件名为 default.vsglog。 如果你未定义 `DONT_SAVE_VSGLOG_TO_TEMP`，则该文件的位置相对于临时目录；否则，将相对于工作目录或位于其他位置（如果你指定了绝对文件名）。  
  
  For [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] apps, the location of the temp directory is specific to each user and app, and is typically found in a location such as C:\users\\*username*\AppData\Local\Packages\\*package family name*\TempState\\. For desktop apps, the location of the temp directory is specific to each user and is typically found in a location such as C:\Users\\*username*\AppData\Local\Temp\\.  
  
> [!NOTE]
> 若要写入特定位置，你必须拥有写入到该位置的权限；否则，将发生错误。 请牢记，就可以写入数据的位置而言， [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 应用比桌面应用更受限制，而且可能需要进行额外配置才能写入某些位置。  
  
### <a name="capturing-the-graphics-information"></a>捕获图形信息  
 在准备好应用以用于编程捕获并有选择地配置好图形日志文件的位置和名称之后，请生成该应用，然后运行或调试它以捕获数据；当使用编程捕获 API 时，请不要从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中启动图形诊断。 图形日志将写入你指定的位置。 如果你想要保留此版本的日志，请将它移动到另一个位置；否则，当你再次运行该应用时，会对其进行重写。  
  
> [!TIP]
> 使用编程捕获时，你仍然可以手动捕获图形信息（以应用为焦点，直接按 **“Print Screen”** ）。 你可以使用此技术捕获编程捕获 API 未捕获到的其他图形信息。  
  
## <a name="next-steps"></a>后续步骤  
 本演练演示了如何采用编程方式捕获图形信息。 下一步，请考虑此选项：  
  
- 了解如何使用图形诊断工具分析捕获的图形信息。 See [Overview](../debugger/overview-of-visual-studio-graphics-diagnostics.md).  
  
## <a name="see-also"></a>请参阅  
 [Walkthrough: Capturing Graphics Information](../debugger/walkthrough-capturing-graphics-information.md)   
 [Capturing Graphics Information](../debugger/capturing-graphics-information.md)   
 [命令行捕获工具](../debugger/command-line-capture-tool.md)
