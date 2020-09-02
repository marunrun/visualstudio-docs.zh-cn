---
title: 寻址 DPI Issues2 |Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 359184aa-f5b6-4b6c-99fe-104655b3a494
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9b8bc5963ba9263d72800cc473cfa56324884ace
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65699267"
---
# <a name="addressing-dpi-issues"></a>解决 DPI 问题
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 "高分辨率" 屏幕装运的设备数量增加。 这些屏幕的每英寸一般超过200像素 (ppi) 。 在这些计算机上使用应用程序时，需要对内容进行扩展，以满足在设备的正常查看距离内查看内容的需要。 从2014，高密度显示的主要目标是移动计算设备 (平板电脑、clamshell 便携式计算机和手机) 。  
  
 Windows 8.1 和更高版本包含多项功能，使这些计算机能够与将计算机同时连接到高密度和标准密度显示的显示器和环境结合使用。  
  
- Windows 可以通过 windows XP) ，使用 "使文本和其他项目变大或更小" (设置，将内容缩放到设备。  
  
- Windows 8.1 和更高版本会自动缩放大多数应用程序的内容，以便在不同像素密度的显示之间移动时保持一致。 如果主显示屏的密度为高密度 (200%) 并且辅助显示器为标准密度 (100% ) ，则 Windows 将自动在辅助显示器上向下缩放应用程序窗口内容 (每4个像素显示1个像素。  
  
- 在 Windows 7 和更高版本的 OEM 可配置) 中，windows 将默认为 (显示的像素密度和查看距离的适当缩放。  
  
- 在 Windows 8.1 S14) 时，Windows 可在超过 280 ppi (的新设备上自动将内容缩放到250%。  
  
  Windows 有一种方法可以处理多个 UI，以利用增加的像素数。 应用程序通过声明自身 "系统 DPI 识别" 来使用该系统。 对于不执行此操作的应用程序，系统会对其进行扩展。 这可能会导致 "模糊" 用户体验，在这种情况下，整个应用程序的像素拉伸都是统一的。 例如：  
  
  ![DPI 问题 模糊](../extensibility/media/dpi-issues-fuzzy.png "DPI 问题 模糊")  
  
  Visual Studio 会将识别为 DPI 缩放，因此不会 "虚拟化"。  
  
  Windows (和 Visual Studio) 利用多种 UI 技术，它们具有不同的方法来处理系统设置的缩放系数。 例如：  
  
- WPF 以与设备无关的方式来度量控件 (单位，而不是像素) 。 对于当前 DPI，WPF UI 会自动向上缩放。  
  
- 所有文本大小（无论使用何种 UI 框架）都用点表示，因此系统会将其视为与 DPI 无关。 在绘制到显示设备时，Win32、WinForms 和 WPF 中的文本已正确缩放。  
  
- Win32/WinForms 对话框和 windows 具有用于启用使用文本调整大小的布局的方式，例如通过网格、流和表布局面板。 这样可以避免在字体大小增加时未缩放的硬编码像素位置。  
  
- 系统或基于系统指标的资源提供的图标 (例如，SM_CXICON 和 SM_CXSMICON) 已经过扩展。  
  
## <a name="older-win32-gdi-gdi-and-winforms-based-ui"></a>旧版 Win32 (GDI、GDI +) 和基于 WinForms 的 UI  
 虽然 WPF 已经有很高的 DPI 感知，但我们最初并未编写过许多基于 Win32/GDI 的代码，但最初并未考虑 DPI 感知。 Windows 提供了 DPI 缩放 Api。 对 Win32 问题的修复应跨产品一致地使用它们。 Visual Studio 提供了一个帮助程序类库，以避免重复功能并确保产品之间的一致性。  
  
## <a name="high-resolution-images"></a>高分辨率图像  
 本部分主要面向开发 Visual Studio 2013 的开发人员。 对于 Visual Studio 2015，请使用内置于 Visual Studio 中的映像服务。 你还可能会发现你需要支持/面向多个 Visual Studio 版本，因此使用2015中的映像服务不是一个选项，因为它不存在于早期版本中。 本部分还适用于你。  
  
## <a name="scaling-up-images-that-are-too-small"></a>正在扩展太小的图像  
 对于太小的图像，可以使用一些常用方法 "放大" 并在 GDI 和 WPF 上呈现。 托管的 DPI 帮助器类可供内部和外部 Visual Studio 集成商提供，用于解决缩放图标、位图、imagestrips 和 imagelists。 基于 Win32 的本机 C/C + + 帮助程序可用于缩放 HICON、HBITMAP、HIMAGELIST 和 VsUI：： GdiplusImage。 缩放位图通常只需要在包括对帮助程序库的引用后进行单行更改。 例如：  
  
```cpp  
(Unmanaged)  VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);  
```  
  
```csharp  
(WinForms) DpiHelper.LogicalToDeviceUnits(ref image);  
```  
  
 缩放 imagelist 取决于 imagelist 是在加载时完成，还是在运行时追加。 如果在加载时完成，请使用 imagelist 来调用 LogicalToDeviceUnits ( # A1，就像使用位图一样。 如果代码需要在撰写 imagelist 之前加载单独的位图，请确保缩放 imagelist 的图像大小：  
  
```csharp  
imagelist.ImageSize = DpiHelper.LogicalToDeviceUnits(imagelist.ImageSize);  
```  
  
 在本机代码中，按如下所示创建 imagelist 时可以缩放维度：  
  
```cpp  
ImageList_Create(VsUI::DpiHelper::LogicalToDeviceUnitsX(16),VsUI::DpiHelper::LogicalToDeviceUnitsY(16), ILC_COLOR32|ILC_MASK, nCount, 1);  
```  
  
 库中的函数允许指定调整大小算法。 在缩放要置于 imagelists 中的图像时，请确保指定用于透明度的背景色，或使用 NearestNeighbor 缩放 (这将导致125% 和 150% ) 扭曲。  
  
 请参阅 <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> MSDN 上的文档。  
  
 下表显示了如何在相应的 DPI 缩放系数上缩放图像的示例。 绿色的图像表示最佳实践，Visual Studio 2013 (100%-200% DPI 缩放) ：  
  
 ![DPI 问题 缩放](../extensibility/media/dpi-issues-scaling.png "DPI 问题 缩放")  
  
## <a name="layout-issues"></a>布局问题  
 主要的布局问题可以通过以下方式避免：通过在 UI 中保持点的相对比例，而不是使用绝对位置 (具体而言，以像素单位) 。 例如：  
  
- 布局/文本位置需要调整，以便为向上扩展的图像提供支持。  
  
- 网格中的列需要为向上缩放文本调整宽度。  
  
- 元素间的硬编码大小或空格还需要向上扩展。 仅基于文本尺寸的尺寸通常是正确的，因为字体会自动向上缩放。  
  
  类中提供了 Helper 函数 <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> ，以允许在 X 和 Y 轴上缩放：  
  
- LogicalToDeviceUnitsX/LogicalToDeviceUnitsY (函数允许在 X/Y 轴上缩放)   
  
- int space = DpiHelper. LogicalToDeviceUnitsX (10) ;  
  
- int height = VsUI：:D piHelper：： LogicalToDeviceUnitsY (5) ;  
  
  存在允许缩放对象（如 Rect、点和大小）的 LogicalToDeviceUnits 重载。  
  
## <a name="using-the-dpihelper-libraryclass-to-scale-images-and-layout"></a>使用 DPIHelper 库/类缩放图像和布局  
 Visual Studio DPI 帮助程序库在本机和托管窗体中提供，可在 Visual Studio shell 的其他应用程序的外部使用。  
  
 若要使用库，请参阅 [Visual STUDIO VSSDK 扩展性示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples) 并克隆高 DPI_Images_Icons 示例  
  
 在 "源文件" 中，包含 VsUIDpiHelper 并调用 VsUI：:D piHelper 类的静态函数：  
  
```cpp  
#include "VsUIDpiHelper.h"  
  
int cxScaled = VsUI::DpiHelper::LogicalToDeviceUnitsX(cx);  
VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);  
  
```  
  
> [!NOTE]
> 不要在模块级或类级静态变量中使用 helper 函数。 该库还使用静态来进行线程同步，你可能会遇到顺序初始化问题。 将这些静态成员转换为非静态成员变量，或将它们封装到函数 (以便在第一次访问) 时进行构造。  
  
 若要从将在 Visual Studio 环境中运行的托管代码访问 DPI 帮助程序函数：  
  
- 使用项目必须引用最新版本的 Shell MPF。 例如：  
  
    ```csharp  
    <Reference Include="Microsoft.VisualStudio.Shell.14.0.dll" />  
    ```  
  
- 确保该项目已引用**PresentationCore**和**PresentationUI** **。**  
  
- 在代码中，使用 **VisualStudio. PlatformUI** 命名空间并调用 DpiHelper 类的静态函数。 对于支持的类型 (点、大小、矩形等) ，提供的扩展函数将返回新的缩放对象。 例如：  
  
    ```csharp  
    using Microsoft.VisualStudio.PlatformUI;  
    double x = DpiHelper.LogicalToDeviceUnitsX(posX);  
    Point ptScaled = ptOriginal.LogicalToDeviceUnits();  
    DpiHelper.LogicalToDeviceUnits(ref bitmap);  
  
    ```  
  
## <a name="dealing-with-wpf-image-fuzziness-in-zoomable-ui"></a>在 zoomable UI 中处理 WPF 图像的容差  
 在 WPF 中，将使用高质量的双立方算法 (默认) （适用于图片或大屏幕快照）为当前 DPI 缩放级别自动调整位图大小，但不适用于 "菜单项" 图标，因为它引入了感知的变差。  
  
 建议：  
  
- 对于徽标图像和横幅图稿， <xref:System.Windows.Media.BitmapScalingMode> 可以使用默认大小调整模式。  
  
- 对于菜单项和插图图像， <xref:System.Windows.Media.BitmapScalingMode> 当不会导致其他扭曲项目消除200% 和 300% ) 的 (颜色时，应使用。  
  
- •对于较大的缩放级别，不是100% 的倍数 (例如，250% 或 350% ) ，用双 首先，通过将 NearestNeighbor 的图像缩放到 100% (的最大倍数，如200% 或 300% ) ，并使用双 请参阅特殊案例：有关详细信息，请参阅适用于大型 DPI 级别的 prescaling WPF 映像。  
  
  PlatformUI 命名空间中的 DpiHelper 类提供 <xref:System.Windows.Media.BitmapScalingMode> 可用于绑定的成员。 它将允许 Visual Studio shell 统一控制整个产品的位图缩放模式，具体取决于 DPI 缩放系数。  
  
  若要在 XAML 中使用该方法，请添加：  
  
```xaml  
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
  
<Setter Property="RenderOptions.BitmapScalingMode" Value="{x:Static vs:DpiHelper.BitmapScalingMode}" />  
  
```  
  
 Visual Studio shell 已经在顶级窗口和对话框中设置了此属性。 在 Visual Studio 中运行的基于 WPF 的 UI 已经继承它。 如果该设置不会传播到您特定的 UI 部分，则可以在 XAML/WPF UI 的根元素上进行设置。 出现这种情况的地方包括弹出窗口、包含 Win32 父元素的元素以及在进程外运行的设计器窗口（如 Blend）。  
  
 某些 UI 可以独立于系统集 DPI 缩放级别进行扩展，例如 Visual Studio 文本编辑器和基于 WPF 的设计器 (WPF 桌面和 Windows 应用商店) 。 在这些情况下，不应使用 DpiHelper. System.windows.media.bitmapscalingmode>。 为了解决此问题，IDE 团队创建了一个名为 System.windows.media.renderoptions>. System.windows.media.bitmapscalingmode> 的自定义属性。 将该属性值设置为 HighQuality 或 NearestNeighbor，具体取决于系统和用户界面的组合缩放级别。  
  
## <a name="special-case-prescaling-wpf-images-for-large-dpi-levels"></a>特例： prescaling 适用于大型 DPI 级别的 WPF 映像  
 对于不是 100% (的倍数的非常大的缩放级别（例如250%、350% 等) ），通过双立方缩放插图图像会导致模糊的、冲蚀的 UI。 这些图像与明锐文本的印象几乎与一种视觉效果一样。 图像看起来更接近于与文本相关的眼睛和焦点。 通过首先将具有 NearestNeighbor 的图像缩放为 100% (的最大倍数，例如200% 或 300% ) 并使用三倍调整到剩余部分 (额外的 50% ) ，可以提高此放大大小的缩放结果。  
  
 下面是结果差异的示例，其中，第一个图像使用改进后的双缩放算法 100%->200%->250%，第二个图像使用三倍双精度 100%->250%。  
  
 ![DPI 问题双缩放示例](../extensibility/media/dpi-issues-double-scaling-example.png "DPI 问题双缩放示例")  
  
 为了使 UI 能够使用这种双缩放，需要修改用于显示每个图像元素的 XAML 标记。 下面的示例演示如何使用 DpiHelper 库和 Shell，在 Visual Studio 中使用 WPF 的双缩放。  
  
 步骤1：使用 NearestNeighbor 将图像 Prescale 为200%、300% 等。  
  
 使用应用于绑定的转换器或使用 XAML 标记扩展 Prescale 图像。 例如：  
  
```xaml  
<vsui:DpiPrescaleImageSourceConverter x:Key="DpiPrescaleImageSourceConverter" />  
  
<Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />  
  
<Image Source="{vsui:DpiPrescaledImage Images/Help.png}" Width="16" Height="16" />  
  
```  
  
 如果还需要对映像进行主题 (大多数情况下（如果不是全部）都应该) ，则标记可以使用第一种转换器，该转换器首先执行图像的主题，然后进行预缩放。 标记可以使用 <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageConverter> 或 <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageSourceConverter> ，具体取决于所需的转换输出。  
  
```xaml  
<vsui:DpiPrescaleThemedImageSourceConverter x:Key="DpiPrescaleThemedImageSourceConverter" />  
  
<Image Width="16" Height="16">  
  <Image.Source>  
    <MultiBinding Converter="{StaticResource DpiPrescaleThemedImageSourceConverter}">  
      <Binding Path="Icon" />  
      <Binding Path="(vsui:ImageThemingUtilities.ImageBackgroundColor)"    
               RelativeSource="{RelativeSource Self}" />  
      <Binding Source="{x:Static vsui:Boxes.BooleanTrue}" />  
    </MultiBinding>  
  </Image.Source>  
</Image>  
```  
  
 步骤2：确保最终大小对于当前 DPI 是正确的。  
  
 因为 WPF 将使用 UIElement 上设置的 System.windows.media.bitmapscalingmode> 属性缩放当前 DPI 的 UI，所以，使用 prescaled 图像作为其源的图像控件的外观将会比它的大小大两倍。 下面是用于应对这种效果的几种方法：  
  
- 如果您知道原始图像在100% 的维度，则可以指定图像控件的精确大小。 在应用缩放之前，这些大小将反映 UI 的大小。  
  
    ```xaml  
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />  
    ```  
  
- 如果原始映像的大小未知，则可以使用 System.windows.frameworkelement.layouttransform 来缩减最终图像对象。 例如：  
  
    ```xaml  
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" >  
        <Image.LayoutTransform>  
         <ScaleTransform  
             ScaleX="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}"  
             ScaleY="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}" />  
        </Image.LayoutTransform>  
    </Image>  
    ```  
  
## <a name="enabling-hdpi-support-to-the-weboc"></a>为 WebOC 启用 HDPI 支持  
 默认情况下，WebOC 控件 (如 WPF 中的 WebBrowser 控件或 IWebBrowser2 接口) 不启用 HDPI 检测和支持。 结果将是在高分辨率显示器上显示内容太小的嵌入控件。 下面介绍如何在特定的 web WebOC 实例中启用高 DPI 支持。  
  
 实现 IDocHostUIHandler 接口 (参阅 [IDocHostUIHandler](https://msdn.microsoft.com/library/aa753260.aspx) 接口上的 MSDN 文章) ：  
  
```idl  
[ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown),  
 Guid("BD3F23C0-D43E-11CF-893B-00AA00BDCE1A")]  
public interface IDocHostUIHandler  
{  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int ShowContextMenu(  
        [In, MarshalAs(UnmanagedType.U4)] int dwID,  
        [In] POINT pt,  
        [In, MarshalAs(UnmanagedType.Interface)] object pcmdtReserved,  
        [In, MarshalAs(UnmanagedType.IDispatch)] object pdispReserved);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int GetHostInfo([In, Out] DOCHOSTUIINFO info);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int ShowUI(  
        [In, MarshalAs(UnmanagedType.I4)] int dwID,  
        [In, MarshalAs(UnmanagedType.Interface)] object activeObject,  
        [In, MarshalAs(UnmanagedType.Interface)] object commandTarget,  
        [In, MarshalAs(UnmanagedType.Interface)] object frame,  
        [In, MarshalAs(UnmanagedType.Interface)] object doc);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int HideUI();  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int UpdateUI();  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int EnableModeless([In, MarshalAs(UnmanagedType.Bool)] bool fEnable);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int OnDocWindowActivate([In, MarshalAs(UnmanagedType.Bool)] bool fActivate);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int OnFrameWindowActivate([In, MarshalAs(UnmanagedType.Bool)] bool fActivate);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int ResizeBorder(  
        [In] COMRECT rect,  
        [In, MarshalAs(UnmanagedType.Interface)] object doc,  
        bool fFrameWindow);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int TranslateAccelerator(  
        [In] ref MSG msg,  
        [In] ref Guid group,  
        [In, MarshalAs(UnmanagedType.I4)] int nCmdID);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int GetOptionKeyPath(  
        [Out, MarshalAs(UnmanagedType.LPArray)] string[] pbstrKey,  
        [In, MarshalAs(UnmanagedType.U4)] int dw);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int GetDropTarget(  
        [In, MarshalAs(UnmanagedType.Interface)] IOleDropTarget pDropTarget,  
        [MarshalAs(UnmanagedType.Interface)] out IOleDropTarget ppDropTarget);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int GetExternal([MarshalAs(UnmanagedType.IDispatch)] out object ppDispatch);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int TranslateUrl(  
        [In, MarshalAs(UnmanagedType.U4)] int dwTranslate,  
        [In, MarshalAs(UnmanagedType.LPWStr)] string strURLIn,  
        [MarshalAs(UnmanagedType.LPWStr)] out string pstrURLOut);  
    [return: MarshalAs(UnmanagedType.I4)]  
    [PreserveSig]  
    int FilterDataObject(  
        IDataObject pDO,  
        out IDataObject ppDORet);  
    }   
```  
  
 或者，实现 ICustomDoc 接口 (参见 [ICustomDoc](https://msdn.microsoft.com/library/aa753272.aspx) 接口) 上的 MSDN 文章：  
  
```idl  
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown),  
 Guid("3050F3F0-98B5-11CF-BB82-00AA00BDCE0B")]  
public interface ICustomDoc  
{  
    void SetUIHandler(IDocHostUIHandler pUIHandler);  
}   
```  
  
 将实现 IDocHostUIHandler 的类与 WebOC 的文档相关联。 如果在上面实现了 ICustomDoc 接口，则 WebOC 的文档属性有效后，会立即将其转换为 ICustomDoc，并调用 SetUIHandler 方法，同时传递实现 IDocHostUIHandler 的类。  
  
```csharp  
// "this" references that class that owns the WebOC control and in this case also implements the IDocHostUIHandler interface  
ICustomDoc customDoc = (ICustomDoc)webBrowser.Document;  
customDoc.SetUIHandler(this);  
  
```  
  
 如果未实现 ICustomDoc 接口，则只要 WebOC 的文档属性有效，就需要将其强制转换为 IOleObject，并调用 SetClientSite 方法，并传入实现 IDocHostUIHandler 的类。 设置传递到 GetHostInfo 方法调用的 DOCHOSTUIINFO 上的 DOCHOSTUIFLAG_DPI_AWARE 标志：  
  
```csharp  
public int GetHostInfo(DOCHOSTUIINFO info)  
{  
    // This is what the default site provides.  
    info.dwFlags = (DOCHOSTUIFLAG)0x5a74012;  
    // Add the DPI flag to the defaults  
    info.dwFlags |=.DOCHOSTUIFLAG.DOCHOSTUIFLAG_DPI_AWARE;  
    return S_OK;  
}  
```  
  
 这应该是使 WebOC 控件支持 HPDI 所需的全部工作。  
  
## <a name="tips"></a>提示  
  
1. 如果 WebOC 控件上的文档属性更改，则可能需要将文档与 IDocHostUIHandler 类重新关联。  
  
2. 如果上述操作不起作用，则会出现一个已知问题，WebOC 不会选取 DPI 标志。 解决这种情况的最可靠方法是切换 WebOC 的光纤缩放，这意味着，两次调用具有两个不同的值来表示缩放百分比。 此外，如果需要解决此问题，则可能需要对每个导航调用执行此方法。  
  
    ```csharp  
    // browser2 is a SHDocVw.IWebBrowser2 in this case  
    // EX: Call the Exec twice with DPI%-1 and then DPI% as the zoomPercent values  
    IOleCommandTarget cmdTarget = browser2.Document as IOleCommandTarget;  
    if (cmdTarget != null)  
    {  
        object commandInput = zoomPercent;  
        cmdTarget.Exec(IntPtr.Zero,  
                       OLECMDID_OPTICAL_ZOOM,  
                       OLECMDEXECOPT_DONTPROMPTUSER,  
                       ref commandInput,  
                       ref commandOutput);  
    }  
    ```
