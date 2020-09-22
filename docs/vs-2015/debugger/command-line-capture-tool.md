---
title: 命令行捕获工具 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: db75b3a7-80b2-4a74-91d2-fd6e0f73b45d
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 208ff7f9bbfc2d07669a8b485edffc8dfc4cd54f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840591"
---
# <a name="command-line-capture-tool"></a>命令行捕获工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DXCap.exe 是一个用于图形诊断捕获和播放的命令行工具。 它在所有功能级别支持从 Direct3D 10 到 Direct3D 12 的所有版本。  
  
## <a name="syntax"></a>语法  
  
```ms-dos  
DXCap.exe [-file filename] [-frame frames | -period periods | -manual] -c app [args...]  
DXCap.exe -p [filename] [-debug | -warp | -hw] [-config] [-rawmode]  
DXCap.exe –p [filename] –screenshot [-frame frames]  
DXCap.exe –p [filename] –toXML [xml_filename]  
DXCap.exe –v [–file filename] [-examine events] [-haltonfail | -exitonfail] [-showprogress]  
DXCap.exe -e [search_string]  
DXCap.exe –info  
```  
  
#### <a name="parameters"></a>参数  
 `-file` `filename`  
  在捕获模式 (`-c`) 下，`filename` 指定记录图形信息的图形日志文件的名称。 如果 `filename` 未指定，将在默认情况下将图形信息记录到名为的文件 `<appname>-<date>-<time>.vsglog` 。  
  
 在验证 (-v) 模式下，`filename` 指定要验证的图形日志文件的名称。 如果 `filename` 未指定，则会再次使用上次验证过的图形日志。  
  
 `-frame` `frames`  
 在捕获模式下，`frames` 指定你要捕获的帧。 第一帧为 1。 你可以通过使用逗号和范围指定多个帧。 例如，如果 `frames` 为 `2, 5, 7-9, 15`，则捕获帧 `2`、`5`、`7`、`8`、`9` 和 `15`。  
  
 `-period` `periods`  
 在捕获模式下，`periods` 指定捕获帧的时间范围，以秒为单位。 你可以通过使用逗号和范围来指定多个时间段。 例如，如果 `periods` 为 `2.1-5, 7.0-9.3`，则在 `2.1` 到 `5` 秒以及 `7` 到 `9.3` 秒之间呈现的帧将被捕获。  
  
 `-manual`  
 在 "捕获模式" 下， `-manual` 指定将通过按 Print Screen 键手动捕获帧。 帧可在应用启动时捕获；如果要停止捕获帧，请返回到命令行界面，并按 Enter。  
  
 `-c` `app` [`args...`]  
 捕获模式。 在捕获模式下，`app` 指定要捕获的图形信息所在的应用的名称；`args...` 对这个应用指定其他命令行参数。  
  
 `-p` [`filename`]  
 播放模式 (`-p`) 。 在验证 (-v) 模式下，`filename` 指定要播放的图形日志文件的名称。 如果 `filename` 未指定，则会再次使用上次播放过的图形日志。  
  
 `-debug`  
 在播放模式下， `-debug` 指定应在启用 Direct3D 调试层的情况下执行播放。  
  
 `-warp`  
 在播放模式下， `-warp` 指定应使用变形软件呈现器执行播放。  
  
 `-hw`  
 在播放模式下， `-hw` 指定应使用 GPU 硬件执行播放。  
  
 `-config`  
 `-config`如果将此信息记录到日志中，则在播放模式下显示有关用于捕获图形日志文件的计算机的信息。  
  
 `-rawmode`  
  在播放模式下，`-rawmode` 指定播放应在不修改所记录事件的前提下执行。 在正常操作下，播放模式可能会对播放进行细微更改，以简化调试、提高播放速度。 例如，它可能会模拟交换链输出，而不是执行交换链命令。 通常这不是一个问题，但你可能需要以一种更加忠实于记录事件的方式下执行播放；例如，可以使用这个选项将全屏呈现行为还原到在全屏模式下运行时捕获到的应用。  
  
 `-toXML` [`xml_filename`]  
 在播放模式下，`xml_filename` 指定播放的 XML 表示形式被写入的文件的名称。 如果 `xml_filename` 未指定，则 XML 表示形式会被写入与被播放文件同名的文件，但会给定一个 `.xml` 扩展名。  
  
 `-v`  
 验证模式。 在验证模式下，捕获的帧会同时在硬件和 WARP 中播放，它们的结果会通过图像比较函数进行比较。 你可以使用这个功能来快速确定影响呈现的驱动程序问题。  
  
 `-examine` `events`  
 在验证模式下，`events` 指定一组其即时结果将被比较的图形事件。 例如，`-examine present,draw,copy,clear` 将比较仅限于属于这些类别的事件。  
  
> [!TIP]
> 我们建议从 `-examine present,draw,copy,clear` 开始，因为这可以显示出大多数问题，同时所需时间相比数目更多的事件集大幅减少。 如有必要，你可以指定数目更多的或另一组事件来验证这些事件并发现其他类型的问题。  
  
 `-haltonfail`  
  在验证模式下，如果检测到硬件和 WARP 呈现器之间存在差异，`-haltonfail` 会停止验证。 在按下一个键后，验证将继续进行。  
  
 `-exitonfail`  
  在验证模式下，如果检测到硬件和 WARP 呈现器之间存在差异，`-exitonfail` 会立即退出验证。 当程序以这种方式退出时，它会将 `0` 返回到环境中；否则，它会返回 `1`。  
  
 `-showprogress`  
  在验证模式下，`-showprogress` 显示验证会话的进度信息。 WARP 进度将显示在左边；硬件进度将显示在右侧。  
  
 `-e` `search_string`  
 枚举安装的 Windows 应用商店应用。 你可以使用这一信息通过 Windows 应用商店应用执行命令行捕获。  
  
 `-info`  
 显示有关计算机和捕获 DLL 的信息。  
  
## <a name="remarks"></a>备注  
 DXCap.exe 可在以下三种模式下运行：  
  
 捕获模式 (-c)  
 从正在运行的应用捕获图形信息并将它记录到图形日志文件中。 捕获功能和文件格式与 Visual Studio 的相同。  
  
 播放模式 (-p)  
 从现有的图形日志文件播放之前捕获的图形事件。 默认情况下，播放会在窗口中进行（即使图形日志文件捕获于全屏应用）。 仅当从全屏应用捕获图形日志文件并指定了 `–rawmode` 时，才会以全屏方式进行播放。  
  
 验证模式 (`-v`)  
 通过在硬件和 WARP 上播放捕获到的帧来验证呈现行为，然后通过使用图像比较函数来比较它们的结果。 你可以使用这个功能来快速确定影响呈现的驱动程序问题。  
  
 除了这些模式外，dxcap.exe 还执行其他两个不执行图形信息捕获或播放的功能。  
  
 枚举函数 (`-e`)   
 显示有关安装在计算机上的 Windows 应用商店应用的详细信息。 这些详细信息包括可标识出 Windows 应用商店应用中的可执行文件的包名称和 appid。 如果要使用 DXCap.exe 从 Windows 应用商店应用捕获图形信息，请使用包名称和 appid，而不用捕获桌面应用时使用的可执行文件名。  
  
 Info 函数 (`-info)`  
 显示有关计算机和捕获 DLL 的详细信息。  
  
## <a name="examples"></a>示例  
  
### <a name="capture-graphics-information-from-a-desktop-app"></a>从桌面应用捕获图形信息  
 使用 `–c` 指定要从中捕获图形信息的应用。  
  
```ms-dos  
DXCap.exe –c BasicHLSL11.exe  
```  
  
 在默认情况下，图形信息记录到名为 `<appname>-<date>-<time>.vsglog` 的文件中。 使用 `–file` 指定要放入记录信息的另一个文件。  
  
```ms-dos  
DXCap.exe –file regression_test_12.vsglog –c BasicHLSL11.exe  
```  
  
 如果要将其他命令行参数指定到要从中捕捉信息的应用，则方法是将它们包含在应用的文件名后。  
  
```ms-dos  
DXCap.exe –c "C:\Program Files\Internet Explorer\iexplorer.exe" "www.fishgl.com"  
```  
  
 查看位于使用 WebGL API 来呈现三维内容的 www.fishgl.com 中的网页时，上述示例中的命令将从桌面版本的 Internet Explorer 中捕获图形信息。  
  
> [!NOTE]
> 由于出现在应用之后的命令行参数会被传递给它，因此必须在使用 `–c` 选项前指定要用于 DXCap.exe 的参数。  
  
### <a name="capture-graphics-information-from-a-windows-store-app"></a>从 Windows 应用商店应用捕获图形信息。  
 你可以从 Windows 应用商店应用捕获图形信息。  
  
```ms-dos  
DXCap.exe –c Microsof.BingMaps_2.1.2914.1734_x64__8wekyb3d8bbwe,AppexMaps  
```  
  
 用 DXCap.exe 从 Windows 应用商店应用进行捕获类似于使用它从 Windows 桌面应用进行捕获，但与根据文件名来确定桌面应用不同的是，你通过包名称和要从中捕获的包内的可执行文件 ID 或名称来标识 Windows 应用商店应用。 为了更轻松地了解如何识别计算机上安装的 Windows 应用商店应用程序，请使用 `–e` 带有 DXCap.exe 的选项来枚举它们：  
  
```ms-dos  
DXCap.exe -e  
```  
  
 你可以提供一个可选的搜索字符串来帮助查找所需的应用。 提供搜索字符串后，DXCap.exe 将枚举包名称、应用名或应用 ID与搜索字符串相匹配的 Windows 应用商店应用。 搜索不区分大小写。  
  
```ms-dos  
DXCap.exe –e map  
```  
  
 上面的命令枚举了与 "map" 匹配的 Windows 应用商店应用；以下是输出：  
  
 包“Microsoft.BingMaps”****：  
 InstallDirectory : C:\Program Files\WindowsApps\Microsoft.BingMaps_2.1.2914.1734_x64__8wekyb3d8bbwe****  
 FullName         : Microsoft.BingMaps_2.1.2914.1734_x64__8wekyb3d8bbwe****  
 UserSID          : S-1-5-21-2127521184-1604012920-1887927527-5603533****  
 Name             : Microsoft.BingMaps****  
 Publisher        : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US****  
 Version          : 2.1.2914.1734****  
 **可启动应用程序：**  
 **Id   : AppexMaps**  
 **Exe  : C:\Program Files\WindowsApps\Microsoft.BingMaps_2.1.2914.1734_x64__8wekyb3d8bbwe\Map.exe**  
 IsWWA: No****  
 **AppSpec (启动) ： DXCap.exe-1734_x64__8wekyb3d8bbwe BingMaps_2 c AppexMaps** 每个枚举应用的最后一个输出行显示可用于从其捕获图形信息的命令。  
  
### <a name="capture-specific-frames-or-frames-between-specific-times"></a>捕获特定帧或特定时段内的帧。  
 使用 `–frame` 通过逗号和范围指定要捕获的帧：  
  
```ms-dos  
DXCap.exe –frame 2,5,7-9,15 –c SimpleBezier11.exe  
```  
  
 或者，使用 `–period` 指定捕获帧的一组时间范围。 时间范围以秒为单位，可以指定多个范围：  
  
```ms-dos  
DXCap.exe –period 2.1-5, 7.0-9.3 –c SimpleBezier11.exe  
```  
  
### <a name="capture-frames-interactively"></a>以交互方式捕获帧。  
 使用 `–manual` 以交互方式捕获帧。 按 Enter 键开始捕获，再按 Enter 键停止捕获。  
  
```ms-dos  
DXCap.exe –manual -c SimpleBezier11.exe  
```  
  
### <a name="play-back-a-graphics-log-file"></a>播放图形日志文件  
 使用 `-p` 播放之前捕获的图形日志文件。  
  
```ms-dos  
DXCap.exe –p regression_test_12.vsglog  
```  
  
 省略文件名以播放最新捕获的图形日志。  
  
```ms-dos  
DXCap.exe –p  
```  
  
### <a name="play-back-in-raw-mode"></a>在 Raw 模式中播放  
 使用 `-rawmode` 在命令发生的同时播放捕获到的命令。 正常播放时，某些命令会被模拟，例如，从全屏应用捕获到的图形日志文件将在窗口播放；启用 Raw 模式时，相同的文件将尝试全屏播放。  
  
```ms-dos  
DXCap.exe –p regression_test_12.vsglog -rawmode  
```  
  
### <a name="play-back-using-warp-or-a-hardware-device"></a>使用 WARP 或硬件设备播放  
 你可能想要强制使用 WARP 播放在硬件设备上捕获到的图形日志文件，强制使用硬件设备播放在 WARP 上捕获到的日志。 使用 `-warp` 通过 WARP 进行播放。  
  
```ms-dos  
DXCap.exe –p regression_test_12.vsglog -warp  
```  
  
 使用 `-hw` 通过硬件进行播放。  
  
```ms-dos  
DXCap.exe –p regression_test_12.vsglog -hw  
```  
  
### <a name="validate-a-graphics-log-file-against-warp"></a>对照 WARP 验证图形日志文件  
 在验证模式下，图形日志文件会同时在硬件和 WARP 上播放，它们的结果将被进行比较。 这可以帮助你标识由驱动程序引起的呈现错误。 对照 WARP 使用 -v 验证图形硬件行为是否正确。  
  
```ms-dos  
DXCap.exe -v regression_test_12.vsglog  
```  
  
 如果要减少比较量，你可以指定要进行比较的验证命令子集，此时其他命令将被忽略。 使用 –examine 指定要对其结果进行比较的命令。  
  
```ms-dos  
DXCap.exe -v regression_test_12.vsglog –examine present,draw,copy,clear  
```  
  
### <a name="convert-a-graphics-log-file-to-pngs"></a>将图形日志文件转换为 PNG  
 如果要从图形日志文件查看或分析帧，DXCap.exe 可将捕获的帧保存为 .png（可迁移网络图形）图像文件。 在播放模式下使用 `-screenshot` 将捕获的帧输出为 .png 文件。  
  
```ms-dos  
DXCap.exe -p BasicHLSL11.vsglog -screenshot  
```  
  
 配合使用 `–frame` 和 `–screenshot` 以指定要输出的帧。  
  
```ms-dos  
DXCap.exe -p BasicHLSL11.vsglog -screenshot –frame 5, 7-9  
```  
  
### <a name="convert-a-graphics-log-file-to-xml"></a>将图形日志文件转换为 XML  
 如果要使用熟悉的工具（如 FindStr 或 XSLT）来处理和分析图形日志，DXCap.exe 可以将图形日志文件转换为 XML。 在播放模式下使用 `-toXML` 将日志转换为 XML，而不是播放日志。  
  
```ms-dos  
DXCap.exe –p regression_test_12.vsglog –toXML  
```  
  
 默认情况下，XML 输出会被写入与图形日志同名的文件中，而这个文件已被给定了一个 .xml 扩展名。 在上面的示例中，XML 文件将被命名为 regression_test_12.xml。 如果要为 XML 文件指定另一个名称，可在 `-toXML` 之后指定。  
  
```ms-dos  
DXCap.exe –p regression_test_12.vsglog –toXML temp.xml  
```  
  
 生成的文件将包含的 XML 类似于：  
  
```xml  
<Moment value="67"/>  
<Method name="CreateDXGIFactory1" >  
    <Return type="HRESULT" value="S_OK" />  
    <Parameter name="riid" type="IID" value="770AAE78-F26F-4DBA-A829-253C83D1B387" />  
    <Parameter name="ppFactory" type="void" handle="1" isOutput="true" />  
</Method>  
  
<Moment value="167"/>  
<Method name="D3D11CreateDevice" >  
    <Return type="HRESULT" value="S_OK" />  
    <Parameter name="pAdapter" type="IDXGIAdapter" handle="34" />  
    <Parameter name="DriverType" type="D3D_DRIVER_TYPE" value="D3D_DRIVER_TYPE_UNKNOWN" />  
    <Parameter name="Software" type="HMODULE" value="pointer" />  
    <Parameter name="Flags" type="UINT" value="0" />  
    <Parameter name="pFeatureLevels" type="D3D_FEATURE_LEVEL" arrSize="1" >  
        <Element value="D3D_FEATURE_LEVEL_11_0" />  
    </Parameter>  
    <Parameter name="FeatureLevels" type="UINT" value="1" />  
    <Parameter name="SDKVersion" type="UINT" value="7" />  
    <Parameter name="ppDevice" type="ID3D11Device" handle="35" isOutput="true" />  
    <Parameter name="pFeatureLevel" type="D3D_FEATURE_LEVEL" value="D3D_FEATURE_LEVEL_11_0" isOutput="true" />  
    <Parameter name="ppImmediateContext" type="ID3D11DeviceContext" value="nullptr" isOutput="true" />  
</Method>  
```  
  
## <a name="requirements"></a>要求
