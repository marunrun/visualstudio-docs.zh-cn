---
title: 解决 DPI 问题2 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 359184aa-f5b6-4b6c-99fe-104655b3a494
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 80f16c5b17a41d1f95b9bcb70e90eb8de46ad69d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740102"
---
# <a name="address-dpi-issues"></a>解决 DPI 问题
越来越多的设备使用"高分辨率"屏幕发货。 这些屏幕通常每英寸 （ppi） 超过 200 像素。 使用这些计算机上的应用程序需要放大内容，以满足在设备正常查看距离下查看内容的需求。 截至 2014 年，高密度显示器的主要目标是移动计算设备（平板电脑、翻盖笔记本电脑和手机）。

Windows 8.1 及更高版本包含多个功能，使这些计算机能够同时处理显示器和计算机同时连接到高密度和标准密度显示器的环境。

- Windows 允许您使用"使文本和其他项目变大或更小"设置（自 Windows XP 以来可用）将内容缩放到设备。

- Windows 8.1 和更高版本将自动缩放大多数应用程序的内容，在像素密度不同的显示之间移动时，内容将保持一致。 当主显示器为高密度（200% 缩放），而辅助显示器为标准密度（100%），Windows 将自动在辅助显示器上向下缩放应用程序窗口内容（应用程序渲染的每 4 个像素显示 1 个像素）。

- Windows 将默认为显示的像素密度和查看距离（Windows 7 及更高版本，OEM 可配置）的右缩放。

- Windows 可以在超过 280 ppi 的新设备上自动缩放内容高达 250%（截至 Windows 8.1 S14）。

  Windows 有一种处理向上扩展 UI 的方法，以利用增加的像素计数。 应用程序通过声明自身为"系统 DPI 感知"来选择加入此系统。 不这样做的应用程序将由系统放大。 这可能导致"模糊"用户体验，其中整个应用程序均匀地拉伸像素。 例如：

  ![DPI 问题 模糊](../extensibility/media/dpi-issues-fuzzy.png "DPI 问题 模糊")

  Visual Studio 选择成为 DPI 缩放感知，因此不是"虚拟化"。

  Windows（和 Visual Studio）利用多种 UI 技术，这些技术在处理系统设置的缩放因素时有不同的处理方式。 例如：

- WPF 以独立于设备的方式测量控件（单位，而不是像素）。 WPF UI 会自动扩展当前 DPI。

- 所有文本大小，无论 UI 框架如何，都以点表示，因此系统将文本大小视为独立于 DPI 的。 Win32、WinForms 和 WPF 中的文本在绘制到显示设备时已正确放大。

- Win32/WinForms 对话框和窗口具有启用使用文本调整大小的布局（例如，通过网格、流和表布局面板）的布局的方法。 这些功能可避免在字体大小增加时未缩放的硬编码像素位置。

- 系统或资源基于系统指标（例如，SM_CXICON和SM_CXSMICON）提供的图标已放大。

## <a name="older-win32-gdi-gdi-and-winforms-based-ui"></a>较旧的 Win32（GDI、GDI+）和基于 WinForms 的 UI
虽然 WPF 已经对 DPI 感知很高，但我们大部分基于 Win32/GDI 的代码最初并不是在考虑到 DPI 意识的情况下编写的。 Windows 提供了 DPI 缩放 API。 Win32 问题的修复应在整个产品中一致地使用这些问题。 Visual Studio 提供了一个帮助器类库，以避免复制功能并确保整个产品的一致性。

## <a name="high-resolution-images"></a>高分辨率图像
本节主要面向扩展 Visual Studio 2013 的开发人员。 对于 Visual Studio 2015，请使用内置于视觉工作室的图像服务。 您可能还会发现，您需要支持/定位 Visual Studio 的许多版本，因此在 2015 年使用影像服务不是一个选项，因为它在以前的版本中并不存在。 本部分也适合您。

## <a name="scaling-up-images-that-are-too-small"></a>放大太小的图像
使用一些常用方法，可以在 GDI 和 WPF 上放大和渲染太小的图像。 托管 DPI 帮助器类可供内部和外部 Visual Studio 集成商使用，用于解决缩放图标、位图、图像绘制和图像列表。 基于 Win32 的本机 C/C++帮助器可用于缩放 HICON、HBITMAP、HIMAGELIST 和 VsUI：GdiplusImage。 位图的缩放通常只需要在包含对帮助器库的引用后进行单行更改。 例如：

```cpp
(Unmanaged) VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);
```

```csharp
(WinForms) DpiHelper.LogicalToDeviceUnits(ref image);
```

缩放图像列表取决于映像列表是在加载时完成，还是在运行时追加。 如果在加载时完成，请像`LogicalToDeviceUnits()`使用位图一样调用图像列表。 当代码在撰写图像列表之前需要加载单个位图时，请确保缩放图像列表的图像大小：

```csharp
imagelist.ImageSize = DpiHelper.LogicalToDeviceUnits(imagelist.ImageSize);
```

在本机代码中，创建图像列表时可以缩放维度，如下所示：

```cpp
ImageList_Create(VsUI::DpiHelper::LogicalToDeviceUnitsX(16),VsUI::DpiHelper::LogicalToDeviceUnitsY(16), ILC_COLOR32|ILC_MASK, nCount, 1);
```

库中的函数允许指定大小调整算法。 缩放要放置在图像列表中的图像时，请确保指定用于透明度的背景颜色，或使用"最近邻居"缩放（这将导致 125% 和 150% 的扭曲）。

请参阅<xref:Microsoft.VisualStudio.PlatformUI.DpiHelper>MSDN 上的文档。

下表显示了如何在相应的 DPI 缩放因子下缩放图像的示例。 橙色中概述的图像表示我们截至 Visual Studio 2013 的最佳实践（100%-200% DPI 缩放）：

![DPI 问题 缩放](../extensibility/media/dpi-issues-scaling.png "DPI 问题 缩放")

## <a name="layout-issues"></a>布局问题
常见的布局问题主要通过在 UI 中缩放和相对于彼此而不是使用绝对位置（特别是以像素单位为单位）来避免。 例如：

- 布局/文本位置需要调整，以考虑放大的图像。

- 网格中的列需要调整缩放文本的宽度。

- 还需要放大元素之间的硬编码大小或空间。 仅基于文本尺寸的大小通常正常，因为字体会自动缩小。

  <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper>帮助器函数在类中可用，允许在 X 轴和 Y 轴上缩放：

- 逻辑到设备单位X/逻辑到设备单元Y（功能允许在 X/Y 轴上缩放）

- 内空间 = DpiHelper.逻辑到设备单元X （10）;

- int 高度 = VsUI：:DpiHelper：：逻辑到设备单元（5）;

  有逻辑到设备单元重载，允许缩放对象，如 Rect、点和大小。

## <a name="using-the-dpihelper-libraryclass-to-scale-images-and-layout"></a>使用 DPIHelper 库/类缩放图像和布局
Visual Studio DPI 帮助器库以本机和托管形式提供，其他应用程序可以在 Visual Studio 外壳之外使用。

要使用库，请访问 Visual [Studio VSSDK 扩展性示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)并克隆高DPI_Images_Icons示例。

在源文件中，包括*VsUIDpiHelper.h*并调用类的`VsUI::DpiHelper`静态函数：

```cpp
#include "VsUIDpiHelper.h"

int cxScaled = VsUI::DpiHelper::LogicalToDeviceUnitsX(cx);
VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);

```

> [!NOTE]
> 请勿在模块级或类级静态变量中使用帮助器函数。 库还使用静态进行线程同步，并且可能会遇到订单初始化问题。 将这些静态变量转换为非静态成员变量，或将它们包装成一个函数（因此，它们在第一次访问时构造）。

要从将在 Visual Studio 环境中运行的托管代码访问 DPI 帮助器函数，请执行以下服务：

- 使用项目必须引用最新版本的壳牌 MPF。 例如：

    ```csharp
    <Reference Include="Microsoft.VisualStudio.Shell.14.0.dll" />
    ```

- 确保项目具有对**System.Windows.窗体**、**演示文稿核心**和演示文稿**UI**的引用。

- 在代码中，使用**Microsoft.VisualStudio.PlatformUI**命名空间，并调用 DpiHelper 类的静态函数。 对于受支持的类型（点、大小、矩形等），提供了返回新缩放对象的扩展函数。 例如：

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    double x = DpiHelper.LogicalToDeviceUnitsX(posX);
    Point ptScaled = ptOriginal.LogicalToDeviceUnits();
    DpiHelper.LogicalToDeviceUnits(ref bitmap);

    ```

## <a name="dealing-with-wpf-image-fuzziness-in-zoomable-ui"></a>处理可缩放 UI 中的 WPF 图像模糊性
在 WPF 中，位图由 WPF 自动调整当前 DPI 缩放级别的大小，使用高质量的双立方算法（默认），该算法适用于图片或大型屏幕截图，但不适合菜单项图标，因为它引入了感知的模糊性。

建议：

- 对于徽标图像和横幅图稿，可以使用<xref:System.Windows.Media.BitmapScalingMode>默认调整大小模式。

- 对于菜单项和图标图像，<xref:System.Windows.Media.BitmapScalingMode>当它不会导致其他失真伪影消除模糊性（200% 和 300%）时，应使用 。

- 对于大型变焦级别，不要出现 100% 的倍数（例如，250% 或 350%），使用双立方缩放图标图像会导致模糊、冲刷的 UI。 首先将离邻将图像缩放到最大倍数 100%（例如，200% 或 300%）时，可以获得更好的结果并从那里用双立方进行缩放。 有关详细信息，请参阅特殊情况：针对大型 DPI 级别的预缩放 WPF 映像。

  Microsoft.VisualStudio.PlatformUI 命名空间中的 DpiHelper 类提供了可用于<xref:System.Windows.Media.BitmapScalingMode>绑定的成员。 它将允许 Visual Studio 外壳根据 DPI 缩放因子统一控制整个产品的位图缩放模式。

  要在 XAML 中使用它，添加：

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"

<Setter Property="RenderOptions.BitmapScalingMode" Value="{x:Static vs:DpiHelper.BitmapScalingMode}" />

```

Visual Studio 外壳已在顶级窗口和对话框上设置此属性。 在可视化工作室中运行的基于 WPF 的 UI 将继承它。 如果该设置未传播到特定 UI 部分，则可以在 XAML/WPF UI 的根元素上设置该设置。 发生这种情况的地方包括弹出窗口、具有 Win32 父元素的元素以及进程用完的设计师窗口（如 Blend）。

某些 UI 可以独立于系统设置的 DPI 缩放级别进行缩放，例如可视化工作室文本编辑器和基于 WPF 的设计器（WPF 桌面和 Windows 应用商店）。 在这些情况下，不应使用 DpiHelper.位映射缩放模式。 为了在编辑器中解决此问题，IDE 团队创建了一个自定义属性，名为"呈现选项.BitmapScalingMode"。 根据系统和 UI 的组合缩放级别，将该属性值设置为"高质量"或"最近邻居"。

## <a name="special-case-prescaling-wpf-images-for-large-dpi-levels"></a>特殊情况：针对大型 DPI 级别的预缩放 WPF 映像
对于不是 100% 的倍数（例如，250%、350%等）的非常大的缩放级别，使用双立方缩放图标图像会导致模糊、冲出 UI。 这些图像与清晰文本的印象几乎类似于一个光学错觉。 图像似乎更接近眼睛，与文本无关。 通过首先将"最近邻居"的图像缩放到最大倍数 100%（例如 200% 或 300%），可以改进此放大大小的缩放结果用双立方缩放到其余部分（额外 50%）。

下面是结果差异的示例，其中第一个图像使用改进的双缩放算法 100%->200%->250%进行缩放，第二个图像仅以双立方 100%->250% 进行缩放。

![DPI 发出双重缩放示例](../extensibility/media/dpi-issues-double-scaling-example.png "DPI 发出双重缩放示例")

为了使 UI 能够使用此双缩放，需要修改用于显示每个图像元素的 XAML 标记。 以下示例演示如何在 Visual Studio 中使用 DpiHelper 库和 Shell.12/14 在 WPF 中使用双缩放。

步骤 1：使用"最近邻居"将图像预缩放为 200%、300%，等等。

使用应用于绑定的转换器或使用 XAML 标记扩展对图像进行预缩放。 例如：

```xaml
<vsui:DpiPrescaleImageSourceConverter x:Key="DpiPrescaleImageSourceConverter" />

<Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />

<Image Source="{vsui:DpiPrescaledImage Images/Help.png}" Width="16" Height="16" />

```

如果图像也需要主题（大多数（如果不是全部）应该），标记可以使用不同的转换器，首先对图像进行主题化，然后预缩放。 标记可以使用 或<xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageConverter><xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageSourceConverter>，具体取决于所需的转换输出。

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

步骤 2：确保当前 DPI 的最终大小正确。

由于 WPF 将使用在 UIElement 上设置的 BitmapScalingMode 属性缩放当前 DPI 的 UI，因此使用预缩放图像作为其源的图像控件看起来将比它应该放大两到三倍。 以下是对抗此效果的几种方法：

- 如果知道原始图像的尺寸为 100%，则可以指定图像控件的确切大小。 在应用缩放之前，这些大小将反映 UI 的大小。

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />
    ```

- 如果不知道原始图像的大小，可以使用 LayoutTransform 来缩小最终图像对象。 例如：

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" >
        <Image.LayoutTransform>
            <ScaleTransform
                ScaleX="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}"
                ScaleY="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}" />
        </Image.LayoutTransform>
    </Image>
    ```

## <a name="enabling-hdpi-support-to-the-weboc"></a>支持 WebOC
默认情况下，WebOC 控件（如 WPF 中的 Web 浏览器控件或 IWebBrowser2 界面）不启用 HDPI 检测和支持。 结果将是一个嵌入式控件，其显示内容在高分辨率显示屏上太小。 下面介绍如何在特定的 Web WebOC 实例中启用高 DPI 支持。

实现 IDocHostUIHandler 接口（请参阅[IDocHostUIHandler](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753260(v=vs.85))上的 MSDN 文章：

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

或者，实现 ICustomDoc 接口（请参阅[ICustomDoc](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753272(v=vs.85))上的 MSDN 文章：

```idl
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
 Guid("3050F3F0-98B5-11CF-BB82-00AA00BDCE0B")]
public interface ICustomDoc
{
    void SetUIHandler(IDocHostUIHandler pUIHandler);
}
```

将实现 IDocHostUIHandler 的类与 WebOC 的文档相关联。 如果上述实现 ICustomDoc 接口，则一旦 WebOC 的文档属性有效，将其转换为 ICustomDoc 并调用 SetUIHandler 方法，传递实现 IDocHostUIHandler 的类。

```csharp
// "this" references that class that owns the WebOC control and in this case also implements the IDocHostUIHandler interface
ICustomDoc customDoc = (ICustomDoc)webBrowser.Document;
customDoc.SetUIHandler(this);

```

如果您没有实现 ICustomDoc 接口，则一旦 WebOC 的文档属性有效，则需要将其强制转换为 IOleObject，并调用`SetClientSite`该方法，传入实现 IDocHostUIHandler 的类。 在传递给`GetHostInfo`方法调用的 DOCHOSTUIINFO 上设置DOCHOSTUIFLAG_DPI_AWARE标志：

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

这应该是获得 WebOC 控制以支持 HPDI 所需的全部功能。

## <a name="tips"></a>提示

1. 如果 WebOC 控件上的文档属性发生更改，则可能需要将文档与 IDocHostUIHandler 类重新关联。

2. 如果上述内容不起作用，则 WebOC 未获取对 DPI 标志的更改存在已知问题。 解决此问题的最可靠方法是切换 WebOC 的光学缩放，这意味着两个调用具有两个不同的缩放百分比值。 此外，如果需要此解决方法，则可能需要在每个导航调用上执行它。

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
