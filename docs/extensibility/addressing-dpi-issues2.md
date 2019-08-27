---
title: 解决 DPI 问题 2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 359184aa-f5b6-4b6c-99fe-104655b3a494
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e2b440ff34a5c1f2c60b8874ba56266b636afde3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352263"
---
# <a name="address-dpi-issues"></a>解决 DPI 问题
越来越多的设备随"高分辨率"屏幕。 这些屏幕通常有超过 200 个像素 / 英寸 (ppi)。 使用这些计算机上的应用程序将需要纵向扩展以满足需要查看设备的正常查看距离处的内容的内容。 截至 2014 年的高密度显示的主要目标是移动计算设备 （平板电脑、 蛤便携式计算机和手机）。

Windows 8.1 和更高版本包含多种功能，以使这些计算机能够使用显示和的环境中计算机附加到同时高密度标准密度显示在同一时间。

- Windows 可允许你为缩放内容以使用"使文本和其他项变大或较小"的设备设置 （自 Windows XP 之后可用）。

- Windows 8.1 和更高版本将自动缩放内容对于大多数应用程序以在不同像素密度的显示器之间移动时保持一致。 当主显示器位于高密度 （200%缩放） 和辅助显示是标准密度 （100%) 时，Windows 将自动减少了应用程序窗口的内容辅助显示器上 (显示为呈现的每个 4 个像素的 1 像素应用程序）。

- Windows 将默认向右缩放像素密度和查看的显示器 (Windows 7 及更高版本，OEM 可配置) 的距离。

- Windows 可以自动缩放设置为 250%内容超过 280 ppi （截至 Windows 8.1 S14) 的新设备上。

  Windows 提供纵向扩展 UI 处理的一种方法利用增加的像素计数。 应用程序通过选择启用此系统自身声明为"系统 DPI 感知。" 请执行此操作的应用程序是由系统纵向扩展。 这可以导致整个应用程序是统一像素拉伸的"模糊"用户体验。 例如：

  ![DPI 问题模糊](../extensibility/media/dpi-issues-fuzzy.png "DPI 问题模糊")

  Visual Studio 成为 DPI 缩放感知型，来选择加入，并因此未"虚拟化。"

  Windows （和 Visual Studio） 利用多个 UI 技术，具有不同的缩放系数由系统设置处理方式。 例如：

- WPF 的独立于设备的方式 （单位，不是以像素） 来测量控件。 为当前的 DPI 自动缩放 WPF UI。

- 无论 UI 框架的所有文本大小以磅为单位表示，并因此被视为由作为独立于 DPI 的系统。 Win32、 WinForms 和 WPF 中的文本已纵向扩展正确绘制到显示设备时。

- Win32/WinForms 对话框和窗口具有用于启用与文本 （例如，通过网格、 流和表布局面板） 调整大小的布局。 这些筛选器可避免不进行缩放时的字体大小会增加的硬编码像素位置。

- 已经过扩展由系统提供的图标或基于系统指标 （例如，SM_CXICON 和 SM_CXSMICON） 的资源。

## <a name="older-win32-gdi-gdi-and-winforms-based-ui"></a>较旧的 Win32 （GDI，GDI +） 和基于 WinForms 的 UI
WPF 已高 DPI 感知，而基于 Win32/GDI 的代码大部分未最初使用编写记住 DPI 识别。 Windows 提供了 DPI 缩放的 Api。 Win32 问题的修补程序应使用这些一致地跨产品。 Visual Studio 提供了一个帮助程序类库，以避免复制功能和跨产品确保一致性。

## <a name="high-resolution-images"></a>高分辨率图像
本部分是主要针对开发人员在扩展 Visual Studio 2013。 对于 Visual Studio 2015 中，使用映像服务是内置在 Visual Studio。 您可能会发现您需要支持/目标许多版本的 Visual Studio，因此使用 2015年中的映像服务不是一个选项，因为不存在以前版本中。 本部分中也是为您然后。

## <a name="scaling-up-images-that-are-too-small"></a>纵向扩展太小的图像
可以纵向扩展和 GDI 和使用某些常见的方法的 WPF 呈现因太小的映像。 托管的 DPI 帮助程序类可供内部和外部 Visual Studio 集成商到缩放图标、 位图、 imagestrips 和 imagelists 的地址。 基于 Win32 的本机 C / C + + 帮助器是可用于缩放 HICON、 HBITMAP、 HIMAGELIST 和 VsUI::GdiplusImage。 缩放的位图的通常只需更改一行后包括对帮助程序库的引用。 例如：

```cpp
(Unmanaged) VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);
```

```csharp
(WinForms) DpiHelper.LogicalToDeviceUnits(ref image);
```

缩放 imagelist 取决于 imagelist 在加载时，已完成还是追加在运行时。 如果在加载时完成，则调用`LogicalToDeviceUnits()`作为您的 imagelist 与将位图。 当代码需要加载各个位图撰写 imagelist 之前时，请确保要缩放的 imagelist 图像大小：

```csharp
imagelist.ImageSize = DpiHelper.LogicalToDeviceUnits(imagelist.ImageSize);
```

在本机代码中，按如下所示创建 imagelist 时，可以缩放尺寸：

```cpp
ImageList_Create(VsUI::DpiHelper::LogicalToDeviceUnitsX(16),VsUI::DpiHelper::LogicalToDeviceUnitsY(16), ILC_COLOR32|ILC_MASK, nCount, 1);
```

库中的函数允许指定的大小调整的算法。 当缩放图像放入 imagelists，请确保指定的透明度，使用的背景色，或使用 NearestNeighbor 缩放 （这将导致在 125%和 150%时会发生失真）。

请查阅<xref:Microsoft.VisualStudio.PlatformUI.DpiHelper>MSDN 上的文档。

下表显示示例的图像的缩放以相应 DPI 的方式缩放比例系数。 橙色中所述的映像表示我们截至 Visual Studio 2013 （100%-200 %dpi 缩放） 的最佳做法：

![DPI 问题缩放](../extensibility/media/dpi-issues-scaling.png "DPI 问题缩放")

## <a name="layout-issues"></a>布局问题
主要通过在 UI 中缩放和相对于其他保留点而不是使用绝对位置 （具体而言，以像素为单位），可以避免常见的布局问题。 例如：

- 布局/文本位置需要调整到帐户的扩展型映像。

- 在网格中的列需要调整的扩展型文本的宽度。

- 硬编码的大小或元素之间的距离将还需要纵向扩展。 仅基于文本的维度的大小是通常会比较好，因为字体自动缩放。

  中提供了帮助程序函数<xref:Microsoft.VisualStudio.PlatformUI.DpiHelper>类，以允许缩放 X 和 Y 轴上：

- LogicalToDeviceUnitsX/LogicalToDeviceUnitsY (函数允许扩展在 X / Y 轴)

- int space = DpiHelper.LogicalToDeviceUnitsX (10);

- int height = VsUI::DpiHelper::LogicalToDeviceUnitsY(5);

  有 LogicalToDeviceUnits 重载以允许缩放对象，如 Rect、 点和大小。

## <a name="using-the-dpihelper-libraryclass-to-scale-images-and-layout"></a>使用缩放图像和布局到 DPIHelper 库/类
Visual Studio DPI 帮助程序库可在本机和托管窗体中，并且可以由其他应用程序之外的 Visual Studio shell。

若要使用的库，请转到[Visual Studio VSSDK 扩展性示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)和克隆高 DPI_Images_Icons 示例。

在源代码文件中包括*VsUIDpiHelper.h*调用的静态函数和`VsUI::DpiHelper`类：

```cpp
#include "VsUIDpiHelper.h"

int cxScaled = VsUI::DpiHelper::LogicalToDeviceUnitsX(cx);
VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);

```

> [!NOTE]
> 不要在模块级别或类级别静态变量中使用的帮助器函数。 库还使用线程同步的静态变量，并可能会遇到顺序初始化问题。 将这些静态对象转换为非静态成员变量，或者将它们包装到的函数 （因此，在首次访问获取构造它们）。

若要从 Visual Studio 环境中运行的托管代码访问 DPI 帮助器函数：

- 使用的项目必须引用 Shell MPF 的最新版本。 例如：

    ```csharp
    <Reference Include="Microsoft.VisualStudio.Shell.14.0.dll" />
    ```

- 请确保项目具有对引用**System.Windows.Forms**， **PresentationCore**，并**PresentationUI**。

- 在代码中，使用**Microsoft.VisualStudio.PlatformUI** DpiHelper 类的命名空间和调用静态函数。 对于支持的类型 （点、 大小、 矩形等），没有提供扩展函数返回新的扩展对象。 例如：

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    double x = DpiHelper.LogicalToDeviceUnitsX(posX);
    Point ptScaled = ptOriginal.LogicalToDeviceUnits();
    DpiHelper.LogicalToDeviceUnits(ref bitmap);

    ```

## <a name="dealing-with-wpf-image-fuzziness-in-zoomable-ui"></a>可缩放的 UI 中的 WPF 图像模糊处理
在 WPF 中，位图是自动调整大小由 WPF 的当前 DPI 缩放级别使用高质量的双三次算法 （默认值），这非常适合图片或较大的屏幕截图，但不适合于菜单项图标，因为它引入的感知颜色容差.

建议：

- 徽标图像和横幅图稿，默认值为<xref:System.Windows.Media.BitmapScalingMode>无法使用重设大小模式。

- 为菜单项和插图图像<xref:System.Windows.Media.BitmapScalingMode>但不会导致其他失真项目以消除颜色容差 （在 200%和 300%） 时，应使用。

- 对于较大的缩放级别不为 100%（例如，250%或 350%） 的倍数，缩放与双三次插图图像会导致模糊、 冲蚀用户界面。 更好的结果被通过第一个缩放到 100%（例如，200%或 300%） 的最大的多个与 NearestNeighbor 图像并使用双三次从该处进行缩放。 请参阅特殊情况： 对于大型 DPI prescaling WPF 图像级别的详细信息。

  Microsoft.VisualStudio.PlatformUI 命名空间中的 DpiHelper 类提供成员<xref:System.Windows.Media.BitmapScalingMode>，可以用于绑定。 它将允许 Visual Studio shell 来控制均匀，具体取决于 DPI 比例因子缩放模式下跨产品的位图。

  若要使用它在 XAML 中，添加：

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"

<Setter Property="RenderOptions.BitmapScalingMode" Value="{x:Static vs:DpiHelper.BitmapScalingMode}" />

```

在 Visual Studio shell 已在顶级窗口和对话框设置此属性。 在 Visual Studio 中运行的基于 WPF 的 UI 已继承它。 如果该设置不会传播到您的特定部分 UI，它可以设置 XAML/WPF UI 的根元素上。 发生此问题的地方包括弹出窗口，在 Win32 父级的元素上和运行带的设计器窗口处理，例如 Blend。

一些 UI 可以独立于系统设置 DPI 缩放级别，如 Visual Studio 文本编辑器和基于 WPF 的设计器 （WPF 桌面和 Windows 应用商店） 进行缩放。 在这些情况下，不应使用 DpiHelper.BitmapScalingMode。 若要解决此问题在编辑器中，IDE 团队创建自定义属性的标题为 RenderOptions.BitmapScalingMode。 将该属性值设置为 HighQuality 或 NearestNeighbor 中，具体取决于系统和 UI 的组合的缩放级别。

## <a name="special-case-prescaling-wpf-images-for-large-dpi-levels"></a>特殊情况： prescaling 大 DPI 级别的 WPF 图像
对于不是 100%（例如，250%、 350%等） 的倍数的非常大的缩放级别，缩放与模糊、 冲蚀 UI 中的双三次结果的插图图像。 这些映像清晰的文本旁边的印象几乎就像的光学视觉效果。 图像显示为更接近眼看并且失去与文本相关的焦点。 通过第一个缩放到 100%（例如，200%或 300%） 的最大的多个与 NearestNeighbor 映像，可以提高此放大大小缩放结果使用和缩放到其余部分 （更多的 50%) 的双三次。

以下是在结果中，差异的示例的第一个图像进行缩放，具有 100%-> 的改进了双缩放的算法 200%-> 250%和第二个只需使用双三次 100%-> 250%。

![DPI 问题缩放示例双](../extensibility/media/dpi-issues-double-scaling-example.png "DPI 问题 Double 缩放示例")

为了启用要用于此双缩放、 XAML 标记显示每个 Image 元素的 UI 将需要进行修改。 以下示例演示如何在 Visual Studio 中使用的 DpiHelper 库和 Shell.12/14 中使用双缩放在 WPF 中。

步骤 1：Prescale 到 200%、 300%等使用 NearestNeighbor 映像。

Prescale 使用任一转换器应用上一个绑定，或使用 XAML 标记扩展的映像。 例如：

```xaml
<vsui:DpiPrescaleImageSourceConverter x:Key="DpiPrescaleImageSourceConverter" />

<Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />

<Image Source="{vsui:DpiPrescaledImage Images/Help.png}" Width="16" Height="16" />

```

如果还需要主题化映像 （大多数情况下，如果不是全部，应），标记可以使用不同的转换器，首先执行映像，然后预缩放的主题。 标记可以使用两个<xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageConverter>或<xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageSourceConverter>，取决于所需的转换输出。

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

步骤 2：请确保最终的大小适合于当前的 DPI。

由于 WPF 针对使用 BitmapScalingMode 属性 UIElement 上设置的当前 DPI 缩放用户界面，应使用 prescaled 的映像，因为其源将查找两个或三个时间比它更大的图像控件。 以下是几种方法，若要避免这种效果：

- 如果您知道在 100%原始图像的维度，可以指定图像控件的确切大小。 这些大小将反映应用缩放前 UI 的大小。

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />
    ```

- 如果不知道原始图像的大小，可以使用 LayoutTransform 缩减最终图像对象。 例如：

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" >
        <Image.LayoutTransform>
            <ScaleTransform
                ScaleX="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}"
                ScaleY="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}" />
        </Image.LayoutTransform>
    </Image>
    ```

## <a name="enabling-hdpi-support-to-the-weboc"></a>启用到 WebOC 的 HDPI 支持
默认情况下，HDPI 检测和支持，不要启用 WebOC 控件 （如 WPF 中或 IWebBrowser2 接口中的 WebBrowser 控件）。 结果将是太小，高分辨率显示器的显示内容与嵌入的控件。 下面介绍如何启用特定的 web WebOC 实例中的高 DPI 支持。

实现 IDocHostUIHandler 接口 (请参阅 MSDN 文章[IDocHostUIHandler](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753260(v=vs.85)):

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

（可选） 实现 ICustomDoc 接口 (请参阅 MSDN 文章[ICustomDoc](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753272(v=vs.85)):

```idl
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
 Guid("3050F3F0-98B5-11CF-BB82-00AA00BDCE0B")]
public interface ICustomDoc
{
    void SetUIHandler(IDocHostUIHandler pUIHandler);
}
```

将实现 IDocHostUIHandler 与 WebOC 的文档的类相关联。 如果实现上述 ICustomDoc 接口，然后立即 WebOC 的文档属性是否有效，将其转换为 ICustomDoc 并调用 SetUIHandler 方法，传递实现 IDocHostUIHandler 的类。

```csharp
// "this" references that class that owns the WebOC control and in this case also implements the IDocHostUIHandler interface
ICustomDoc customDoc = (ICustomDoc)webBrowser.Document;
customDoc.SetUIHandler(this);

```

如果未实现 ICustomDoc 接口，则只要 WebOC 的文档属性是有效的您将需要将其转换为 IOleObject，并调用`SetClientSite`方法，传入实现 IDocHostUIHandler 的类。 设置传递给 DOCHOSTUIINFO DOCHOSTUIFLAG_DPI_AWARE 标志`GetHostInfo`方法调用：

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

这应该是所有您需要先获取 WebOC 控件支持 HPDI。

## <a name="tips"></a>提示

1. 如果 WebOC 控件上的文档属性发生更改，可能需要将文档与 IDocHostUIHandler 类重新关联。

2. 如果以上命令无效，则不选取更改为 DPI 标志 WebOC 的已知的问题。 修复此问题的最可靠方法是切换 WebOC 含义使用两个不同的缩放百分比值的两个调用视觉缩放。 此外，如果需要此解决方法，它可能需要执行导航的每个调用上。

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
