---
title: 演练：以编程方式捕获图形信息 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e2036588fe04825b0fe1a1aa2db7ae8f7e0b5ad4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72734774"
---
# <a name="walkthrough-capturing-graphics-information-programmatically"></a>演练：以编程方式捕获图形信息
你可以使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 图形诊断以编程方式从 Direct3D 应用中捕获图形信息。

编程捕获在以下方案中非常有用：

- 当图形应用不使用存在的交换链时（例如当它呈现为纹理时），开始以编程方式捕获。

- 当应用不呈现任何内容时（例如当它使用 DirectCompute 来执行计算时），开始以编程方式捕获。

- 调用 `CaptureCurrentFrame`when 在手动测试中难以预测和捕获呈现问题，但可以通过在运行时使用有关应用状态的信息以编程方式预测。

## <a name="CaptureDX11_2"></a> Windows 10 中的编程捕获
本部分演练演示了在 Windows 10 上使用 DirectX 11.2 API 的应用中的编程捕获，它使用可靠捕获方法。

本部分显示如何完成这些任务：

- 准备你的应用以使用编程捕获

- 获取 IDXGraphicsAnalysis 接口

- 捕获图形信息

> [!NOTE]
> 以前的编程捕获的实现依赖于 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Visual Studio 远程工具来提供捕获功能。

### <a name="preparing-your-app-to-use-programmatic-capture"></a>准备你的应用以使用编程捕获
若要在应用中使用编程捕获，它必须包括必要的标头。 这些标头属于 Windows 10 SDK。

##### <a name="to-include-programmatic-capture-headers"></a>包括编程捕获标头

- 将这些标头包含在你要在其中定义 IDXGraphicsAnalysis 接口的源文件中：

    ```cpp
    #include <DXGItype.h>
    #include <dxgi1_2.h>
    #include <dxgi1_3.h>
    #include <DXProgrammableCapture.h>
    ```

    > [!IMPORTANT]
    > 请勿包括头文件 vsgcapture.h（支持 Windows 8.0 及更早版本上的编程捕获）来在 Windows 10 应用中执行编程捕获。 此标头无法与 DirectX 11.2 兼容。 如果在包含 d3d11_2 标头之后包含此文件，则编译器会发出警告。 如果 d3d11_2 之前包含 vsgcapture.h，应用将不会启动。

    > [!NOTE]
    > 如果你的计算机上安装了 DirectX SDK（2010 年 6 月），并且你的项目的包括路径包含 `%DXSDK_DIR%includex86`，请将它移动到包括路径末尾。 针对你的库路径执行相同操作。

### <a name="getting-the-idxgraphicsanalysis-interface"></a>获取 IDXGraphicsAnalysis 接口
在可以从 DirectX 11.2 中捕获图形信息之前，你必须获取 DXGI 调试接口。

> [!IMPORTANT]
> 使用编程捕获时，仍必须在图形诊断下运行应用（[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中的 Alt + F5），或在[命令行捕获工具](command-line-capture-tool.md)下运行。

##### <a name="to-get-the-idxgraphicsanalysis-interface"></a>获取 IDXGraphicsAnalysis 接口

- 请使用以下代码挂钩 DXGI 调试接口的 IDXGraphicsAnalysis 接口。

  ```cpp
  IDXGraphicsAnalysis* pGraphicsAnalysis;
  HRESULT getAnalysis = DXGIGetDebugInterface1(0, __uuidof(pGraphicsAnalysis), reinterpret_cast<void**>(&pGraphicsAnalysis));
  ```

  务必检查[DXGIGetDebugInterface1](/windows/desktop/api/dxgi1_3/nf-dxgi1_3-dxgigetdebuginterface1)返回的 `HRESULT`，以确保在使用它之前获得一个有效的接口：

  ```cpp
  if (FAILED(getAnalysis))
  {
      // Abort program or disable programmatic capture in your app.
  }
  ```

  > [!NOTE]
  > 如果在 `DXGIGetDebugInterface1` 返回 `E_NOINTERFACE` （`error: E_NOINTERFACE No such interface supported`），请确保应用在图形诊断下运行（ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中的 Alt + F5）。

### <a name="capturing-graphics-information"></a>捕获图形信息
现在你已拥有一个有效的 `IDXGraphicsAnalysis` 接口，你可以使用 `BeginCapture` 和 `EndCapture` 捕获图形信息。

##### <a name="to-capture-graphics-information"></a>捕获图形信息

- 若要开始捕获图形信息，请使用 `BeginCapture`：

    ```cpp
    ...
    pGraphicsAnalysis->BeginCapture();
    ...
    ```

    调用 `BeginCapture` 后捕获会立即开始；它不会等待下一帧开始。 显示当前帧或调用 `EndCapture`后，捕获将停止：

    ```cpp
    ...
    pGraphicsAnalysis->EndCapture();
    ...
    ```

- 调用 `EndCapture` 后，释放图形对象。

## <a name="next-steps"></a>后续步骤
本演练演示了如何采用编程方式捕获图形信息。 下一步，请考虑此选项：

- 了解如何使用图形诊断工具分析捕获的图形信息。 请参阅[概述](overview-of-visual-studio-graphics-diagnostics.md)。

## <a name="see-also"></a>请参阅
- [演练：捕获图形信息](walkthrough-capturing-graphics-information.md)
- [Capturing Graphics Information](capturing-graphics-information.md)
- [命令行捕获工具](command-line-capture-tool.md)
