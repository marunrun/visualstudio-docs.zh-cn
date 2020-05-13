---
title: 影像服务和目录 |微软文档
ms.date: 04/01/2019
ms.topic: conceptual
ms.assetid: 34990c37-ae98-4140-9b1e-a91c192220d9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 79e1ccfad2a678656bcf09e37852532a8b28eb0e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710389"
---
# <a name="image-service-and-catalog"></a>影像服务和目录
本说明书包含采用 Visual Studio 2015 中介绍的可视化工作室影像服务和图像目录的指南和最佳实践。

 Visual Studio 2015 中引入的图像服务允许开发人员获得设备的最佳图像和用户选择的主题来显示图像，包括正确选择显示图像的上下文。 采用影像服务将有助于消除与资产维护、HDPI 扩展和准备相关的主要痛点。

|||
|-|-|
|**今天的问题**|**解决方案**|
|背景颜色混合|内置 alpha 混合|
|人物（一些）图像|主题元数据|
|高对比度模式|备用高对比度资源|
|需要多种资源用于不同的 DPI 模式|具有基于矢量的回退的可选资源|
|重复图像|每个映像概念一个标识符|

 为什么要采用影像服务？

- 始终从视觉工作室获取最新的"像素完美"图像

- 您可以提交和使用自己的图像

- 当 Windows 添加新的 DPI 缩放时，无需测试映像

- 解决实现中的旧体系结构障碍

  使用影像服务之前和之后的 Visual Studio 外壳工具栏：

  ![图像服务前后对比](../extensibility/media/image-service-before-and-after.png "图像服务前后对比")

## <a name="how-it-works"></a>工作原理
 影像服务可以提供适合任何受支持的 UI 框架的位映射映像：

- WPF：位图来源

- 赢窗体：系统.绘图.位图

- 赢32： HBITMAP

  影像服务流程图

  ![图像服务流关系图](../extensibility/media/image-service-flow-diagram.png "图像服务流关系图")

  **图像名字**

  图像名称对象（简称"名称"）是一个 GUID/ID 对，用于唯一标识图像库中的图像资产或图像列表资产。

  **已知名字**

  视觉工作室图像目录中包含的图像名字集，任何 Visual Studio 组件或扩展都公开使用。

  **图像清单文件**

  图像清单 *（.imagemanifest*） 文件是定义一组图像资产的 XML 文件、表示这些资产的名号以及表示每个资产的真实图像或图像。 映像清单可以为旧版 UI 支持定义独立映像或图像列表。 此外，还可以在每个资产后面的单个图像上设置一些属性，以更改这些资产的显示时间以及方式。

  **映像清单架构**

  完整的图像清单如下所示：

```xml
<ImageManifest>
      <!-- zero or one Symbols elements -->
      <Symbols>
        <!-- zero or more Import, Guid, ID, or String elements -->
      </Symbols>
      <!-- zero or one Images elements -->
      <Images>
        <!-- zero or more Image elements -->
      </Images>
      <!-- zero or one ImageLists elements -->
      <ImageLists>
        <!-- zero or more ImageList elements -->
      </ImageLists>
</ImageManifest>
```

 **“符号”**

 作为可读性和维护辅助工具，图像清单可以使用符号进行属性值。 符号的定义如下：

```xml
<Symbols>
      <Import Manifest="manifest" />
      <Guid Name="ShellCommandGuid" Value="8ee4f65d-bab4-4cde-b8e7-ac412abbda8a" />
      <ID Name="cmdidSaveAll" Value="1000" />
      <String Name="AssemblyName" Value="Microsoft.VisualStudio.Shell.UI.Internal" />
</Symbols>
```

|||
|-|-|
|**子元素**|**定义**|
|导入|导入给定清单文件符号，用于当前清单|
|Guid|符号表示 GUID，必须匹配 GUID 格式|
|ID|符号表示 ID，并且必须是非负整数|
|字符串|符号表示任意字符串值|

 符号区分大小写，并使用 $（符号名称）语法引用：

```xml
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />
</Image>
```

 某些符号是为所有清单预定义的。 这些可用于\<源>的 Uri 属性，或者\<导入>元素以引用本地计算机上的路径。

|||
|-|-|
|**象征**|**说明**|
|CommonProgramFiles|%公共程序文件% 环境变量的值|
|本地应用数据|%LocalAppData% 环境变量的值|
|清单文件夹|包含清单文件的文件夹|
|我的文档|当前用户的"我的文档"文件夹的完整路径|
|ProgramFiles|%程序文件% 环境变量的值|
|系统|*Windows_System32*文件夹|
|温迪尔|%WinDir% 环境变量的值|

 **映像**

 图像\<>元素定义一个可以由名字对象引用的图像。 GUID 和 ID 一起构成图像名字。 图像的绰号必须在整个图像库中是唯一的。 如果多个图像具有给定的名字对象，则构建库时遇到的第一个图像是保留的映像。

 它必须至少包含一个源。 大小中性源将在各种大小中提供最佳结果，但不是必需的。 如果要求服务提供\<未在 Image> 元素中定义的大小图像，并且没有大小无关的源，则服务将选择最佳特定于大小的源并将其缩放到请求的大小。

```xml
<Image Guid="guid" ID="int" AllowColorInversion="true/false">
      <Source ... />
      <!-- optional additional Source elements -->
</Image>
```

|||
|-|-|
|**特性**|**定义**|
|Guid|[必需]图像名字项的 GUID 部分|
|ID|[必需]图像名字对象 ID 部分|
|允许颜色反转|[可选，默认为 true]指示在深色背景上使用时，图像的颜色是否可以以编程方式反转。|

 **源**

 源\<>元素定义单个映像源资产（XAML 和 PNG）。

```xml
<Source Uri="uri" Background="background">
      <!-- optional NativeResource element -->
 </Source>
```

|||
|-|-|
|**特性**|**定义**|
|Uri|[必需]定义图像从何处加载的 URI。 该参数可以是下列值之一：<br /><br /> - 使用application:///权限的[包 URI](/dotnet/framework/wpf/app-development/pack-uris-in-wpf)<br />- 绝对组件资源引用<br />- 包含本机资源的文件的路径|
|背景|[可选]指示源在哪些背景上打算使用。<br /><br /> 该参数可以是下列值之一：<br /><br /> *浅色：* 光源可用于浅色背景。<br /><br /> *黑暗：* 源可用于深色背景。<br /><br /> *高对比度：* 源可以在高对比度模式下的任何背景上使用。<br /><br /> *高对比度指示灯：* 光源可在高对比度模式下的光背景上使用。<br /><br /> *高对比度暗：* 源可用于高对比度模式下的黑暗背景。<br /><br /> 如果省略了背景属性，则源可用于任何背景。<br /><br /> 如果背景是 *"浅色*"、*暗*色、*高对比度或**高对比度暗*，则源的颜色永远不会反转。 如果"背景"省略或设置为 *"高对比度*"，则源颜色的反转由图像的**AllowColor 反转**属性控制。|

\<源>元素可以完全具有以下可选子元素之一：

||||
|-|-|-|
|**元素**|**属性（所有必需）**|**定义**|
|\<大小>|值|源将用于给定大小的图像（以设备单位为单位）。 图像将是方形的。|
|\<大小范围>|最小尺寸，最大尺寸|源将用于从最小尺寸到 MaxSize（以设备单位为单位）的图像（包括设备单位）。 图像将是方形的。|
|\<尺寸>|Width, Height|源将用于给定宽度和高度（以设备单位为单位）的图像。|
|\<尺寸范围>|最小宽度， 最小高度，<br /><br /> 最大宽度，最大高度|源将用于从最小宽度/高度到最大宽度/高度（以设备单位为单位）的图像（包括设备单位）。|

 \<源>元素还可以具有可选\<的本机资源>子元素，该子元素定义从本机程序集而不是托管程序集加载的\<源>。

```xml
<NativeResource Type="type" ID="int" />
```

|||
|-|-|
|**特性**|**定义**|
|类型|[必需]本机资源的类型，XAML 或 PNG|
|ID|[必需]本机资源的整数 ID 部分|

 **图片列表**

 ImageList \<>元素定义可在单个条带中返回的图像集合。 根据需要，该条条按需构建。

```xml
<ImageList>
      <ContainedImage Guid="guid" ID="int" External="true/false" />
      <!-- optional additional ContainedImage elements -->
 </ImageList>
```

|||
|-|-|
|**特性**|**定义**|
|Guid|[必需]图像名字项的 GUID 部分|
|ID|[必需]图像名字对象 ID 部分|
|外部|[可选，默认错误]指示图像名字对象是否引用当前清单中的图像。|

 包含图像的绰号不必引用在当前清单中定义的图像。 如果在图像库中找不到包含的图像，则在其位置将使用空白占位符图像。

## <a name="using-the-image-service"></a>使用影像服务

### <a name="first-steps-managed"></a>第一步（托管）
 要使用影像服务，您需要向项目添加对以下部分或全部程序集的引用：

- *微软.VisualStudio.ImageCatalog.dll*

  - 需要，如果你使用内置的图像目录**已知莫尼克器**。

- *微软.VisualStudio.成像.dll*

  - 如果在 WPF UI 中使用**CrispImage**和**ImageTheming 实用程序**，则需要。

- *微软.VisualStudio.成像.Interop.14.0.设计时间.dll*

  - 如果使用**ImageMoniker**和**ImageAttributes**类型，则需要。

  - **嵌入类型**应设置为 true。

- *微软.VisualStudio.shell.Interop.14.0.设计时间*

  - 如果使用**IVImageService2**类型，则需要。

  - **嵌入类型**应设置为 true。

- *微软.VisualStudio.实用程序.dll*

  - 如果您使用 **"画笔到颜色转换器****"进行图像实用程序.图像背景颜色**，则需要在 WPF UI 中使用。

- *微软.VisualStudio.Shell.\<vsVersion>.0*

  - 如果使用**IVUIObject**类型，则需要。

- *微软.VisualStudio.shell.Interop.10.0.dll*

  - 如果使用与 WinForms 相关的 UI 帮助器，则需要。

  - **嵌入类型**应设置为 true

### <a name="first-steps-native"></a>第一步（本机）
 要使用影像服务，您需要向项目包括以下部分或全部标头：

- **已知图像 Ids.h**

  - 如果使用内置图像目录**已知 Monikers**，但无法使用**ImageMoniker**类型，例如从**IV 层次结构 GetGuidProperty**或**GetProperty**调用返回值时，则是必需的。

- **已知莫尼克斯.h**

  - 需要，如果你使用内置的图像目录**已知莫尼克器**。

- **图像参数140.h**

  - 如果使用**ImageMoniker**和**ImageAttributes**类型，则需要。

- **VSShell140.h**

  - 如果使用**IVImageService2**类型，则需要。

- **图片实用程序.h**

  - 如果您不能让影像服务为您处理主名，则需要。

  - 如果影像服务可以处理您的图像标题，则不要使用此标头。

::: moniker range="vs-2017"
- **VSUIDPIHelper.h**

  - 如果使用 DPI 帮助器获取当前 DPI，则需要。

::: moniker-end

::: moniker range=">=vs-2019"
- **VsDpiAwareness.h**

  - 如果使用 DPI 意识帮助器获取当前 DPI，则需要。

::: moniker-end

## <a name="how-do-i-write-new-wpf-ui"></a>如何编写新的 WPF UI？

1. 首先，将上述第一步部分中所需的程序集引用添加到项目中。 您无需添加所有引用，因此只需添加所需的引用。 （注意：如果您正在使用或有权访问**颜色**而不是**画笔**，则可以跳过对**实用程序**的引用，因为您不需要转换器。

2. 选择所需的图像并获取其名字对象。 使用**已知Moniker，** 或者使用你自己的，如果你有自己的自定义图像和名字。

3. 将**CrispImage**添加到您的 XAML 中。 （请参阅下面的示例。

4. 在 UI 层次结构中设置**ImageTheming 实用程序.Image背景颜色**属性。 （这应设置在已知背景颜色的位置，不一定在**CrispImage**上。（请参阅下面的示例。

```xaml
<Window
  x:Class="WpfApplication.MainWindow"
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  xmlns:imaging="clr-namespace:Microsoft.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:theming="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:utilities="clr-namespace:Microsoft.Internal.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:catalog="clr-namespace:Microsoft.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.ImageCatalog"
  Title="MainWindow" Height="350" Width="525" UseLayoutRounding="True">
  <Window.Resources>
    <utilities:BrushToColorConverter x:Key="BrushToColorConverter"/>
  </Window.Resources>
  <StackPanel Background="White" VerticalAlignment="Center"
    theming:ImageThemingUtilities.ImageBackgroundColor="{Binding Background, RelativeSource={RelativeSource Self}, Converter={StaticResource BrushToColorConverter}}">
    <imaging:CrispImage Width="16" Height="16" Moniker="{x:Static catalog:KnownMonikers.MoveUp}" />
  </StackPanel>
</Window>
```

 **如何更新现有的 WPF UI？**

 更新现有的 WPF UI 是一个相对简单的过程，由三个基本步骤组成：

1. 将\<UI 中的所有图像>元素替换为\<CrispImage>元素。

2. 将所有源属性更改为 Moniker 属性。

    - 如果图像从未更改，并且您正在使用 **"已知莫尼克器**"，则静态地将该属性绑定到**已知 Moniker。** （请参阅上述示例。

    - 如果图像从未更改，并且您正在使用自己的自定义映像，则静态绑定到您自己的名字对象。

    - 如果图像可以更改，则将 Moniker 属性绑定到代码属性，该属性会通知属性更改。

3. 在 UI 层次结构的某处，设置**ImageTheming 实用程序.Image背景颜色**，以确保颜色反转正常工作。

    - 这可能需要使用**BrushtoColor 转换器**类。 （请参阅上述示例。

## <a name="how-do-i-update-win32-ui"></a>如何更新 Win32 UI？
 在适当的情况下向代码添加以下内容，以替换映像的原始加载。 根据需要切换用于返回 HBITMA 与 HICOS 与 HIMAGELIST 的值。

 **获取影像服务**

```cpp
CComPtr<IVsImageService2> spImgSvc;
CGlobalServiceProvider::HrQueryService(SID_SVsImageService, &spImgSvc);
```

 **请求映像**

::: moniker range="vs-2017"

```cpp
ImageAttributes attr = { 0 };
attr.StructSize      = sizeof(attributes);
attr.Format          = DF_Win32;
// IT_Bitmap for HBITMAP, IT_Icon for HICON, IT_ImageList for HIMAGELIST
attr.ImageType       = IT_Bitmap;
attr.LogicalWidth    = 16;
attr.LogicalHeight   = 16;
attr.Dpi             = VsUI::DpiHelper::GetDeviceDpiX();
// Desired RGBA color, if you don't use this, don't set IAF_Background below
attr.Background      = 0xFFFFFFFF;
attr.Flags           = IAF_RequiredFlags | IAF_Background;

CComPtr<IVsUIObject> spImg;
// Replace this KnownMoniker with your desired ImageMoniker
spImgSvc->GetImage(KnownMonikers::Blank, attributes, &spImg);
```

::: moniker-end

::: moniker range=">=vs-2019"

```cpp
UINT dpiX, dpiY;
HWND hwnd = // get the HWND where the image will be displayed
VsUI::CDpiAwareness::GetDpiForWindow(hwnd, &dpiX, &dpiY);

ImageAttributes attr = { 0 };
attr.StructSize      = sizeof(attributes);
attr.Format          = DF_Win32;
// IT_Bitmap for HBITMAP, IT_Icon for HICON, IT_ImageList for HIMAGELIST
attr.ImageType       = IT_Bitmap;
attr.LogicalWidth    = 16;
attr.LogicalHeight   = 16;
attr.Dpi             = dpiX;
// Desired RGBA color, if you don't use this, don't set IAF_Background below
attr.Background      = 0xFFFFFFFF;
attr.Flags           = IAF_RequiredFlags | IAF_Background;

CComPtr<IVsUIObject> spImg;
// Replace this KnownMoniker with your desired ImageMoniker
spImgSvc->GetImage(KnownMonikers::Blank, attributes, &spImg);
```

::: moniker-end

## <a name="how-do-i-update-winforms-ui"></a>如何更新 WinForms UI？
 在适当的情况下向代码添加以下内容，以替换映像的原始加载。 根据需要切换用于返回位图和图标的值。

 **有用的使用语句**

```csharp
using GelUtilities = Microsoft.Internal.VisualStudio.PlatformUI.Utilities;
```

 **获取影像服务**

```csharp
// This or your preferred way of querying for Visual Studio services
IVsImageService2 imageService = (IVsImageService2)Package.GetGlobalService(typeof(SVsImageService));

```

 **请求映像**

::: moniker range="vs-2017"

```csharp
ImageAttributes attributes = new ImageAttributes
{
    StructSize    = Marshal.SizeOf(typeof(ImageAttributes)),
    // IT_Bitmap for Bitmap, IT_Icon for Icon, IT_ImageList for ImageList
    ImageType     = (uint)_UIImageType.IT_Bitmap,
    Format        = (uint)_UIDataFormat.DF_WinForms,
    LogicalWidth  = 16,
    LogicalHeight = 16,
    Dpi           = (int)DpiHelper.DeviceDpiX;
    // Desired RGBA color, if you don't use this, don't set IAF_Background below
    Background    = 0xFFFFFFFF,
    Flags         = unchecked((uint)_ImageAttributesFlags.IAF_RequiredFlags | _ImageAttributesFlags.IAF_Background),
};

// Replace this KnownMoniker with your desired ImageMoniker
IVsUIObject uIObj = imageService.GetImage(KnownMonikers.Blank, attributes);

Bitmap bitmap = (Bitmap)GelUtilities.GetObjectData(uiObj); // Use this if you need a bitmap
// Icon icon = (Icon)GelUtilities.GetObjectData(uiObj);    // Use this if you need an icon
```

::: moniker-end

::: moniker range=">=vs-2019"

```csharp
Control control = // get the control where the image will be displayed

ImageAttributes attributes = new ImageAttributes
{
    StructSize    = Marshal.SizeOf(typeof(ImageAttributes)),
    // IT_Bitmap for Bitmap, IT_Icon for Icon, IT_ImageList for ImageList
    ImageType     = (uint)_UIImageType.IT_Bitmap,
    Format        = (uint)_UIDataFormat.DF_WinForms,
    LogicalWidth  = 16,
    LogicalHeight = 16,
    Dpi           = (int)DpiAwareness.GetWindowDpi(control.Handle);
    // Desired RGBA color, if you don't use this, don't set IAF_Background below
    Background    = 0xFFFFFFFF,
    Flags         = unchecked((uint)_ImageAttributesFlags.IAF_RequiredFlags | _ImageAttributesFlags.IAF_Background),
};

// Replace this KnownMoniker with your desired ImageMoniker
IVsUIObject uIObj = imageService.GetImage(KnownMonikers.Blank, attributes);

Bitmap bitmap = (Bitmap)GelUtilities.GetObjectData(uiObj); // Use this if you need a bitmap
// Icon icon = (Icon)GelUtilities.GetObjectData(uiObj);    // Use this if you need an icon
```

::: moniker-end

## <a name="how-do-i-use-image-monikers-in-a-new-tool-window"></a>如何在新工具窗口中使用图像名字对象？
 VSIX 包项目模板已更新为 Visual Studio 2015。 要创建新的工具窗口，请右键单击 VSIX 项目并选择"**添加新** > **项目**+**Shift**+**"（Ctrl**Shift**A**）。 在项目语言的"可扩展性"节点下，选择 **"自定义工具窗口**"，为工具窗口指定名称，然后按 **"添加**"按钮。

 这些是工具窗口中使用名字器的关键位置。 按照每个说明：

1. 当选项卡变得足够小时工具窗口选项卡（也用于**Ctrl**+**选项卡**窗口切换器）。

    将此行添加到派生自 **"工具窗口窗格**"类型的类的构造函数：

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   this.BitmapImageMoniker = KnownMonikers.Blank;
   ```

2. 打开工具窗口的命令。

    在包的 *.vsct*文件中，编辑工具窗口的命令按钮：

   ```xml
   <Button guid="guidPackageCmdSet" id="CommandId" priority="0x0100" type="Button">
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
     <!-- Replace this KnownMoniker with your desired ImageMoniker -->
     <Icon guid="ImageCatalogGuid" id="Blank" />
     <!-- Add this -->
     <CommandFlag>IconIsMoniker</CommandFlag>
     <Strings>
       <ButtonText>MyToolWindow</ButtonText>
     </Strings>
   </Button>
   ```

   **如何在现有工具窗口中使用图像名字对象？**

   更新现有工具窗口以使用图像名字对象类似于创建新工具窗口的步骤。

   这些是工具窗口中使用名字器的关键位置。 按照每个说明：

3. 当选项卡变得足够小时工具窗口选项卡（也用于**Ctrl**+**选项卡**窗口切换器）。

   1. 删除从**工具WindowPane**类型派生的类的构造函数中的这些行（如果存在）：

       ```csharp
       this.BitmapResourceID = <Value>;
       this.BitmapIndex = <Value>;
       ```

   2. #1 请参阅"如何在新工具窗口中使用图像名字器？ 上文部分。

4. 打开工具窗口的命令。

   - 请参阅 #2"如何在新工具窗口中使用图像名字器？ 上文部分。

## <a name="how-do-i-use-image-monikers-in-a-vsct-file"></a>如何在 .vsct 文件中使用图像名字对象？
 按照以下注释行所示更新 *.vsct*文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <!--  Include the definitions for images included in the VS image catalog -->
  <Include href="KnownImageIds.vsct"/>
  <Commands package="guidMyPackage">
    <Buttons>
      <Button guid="guidMyCommandSet" id="cmdidMyCommand" priority="0x0000" type="Button">
        <!-- Add an Icon element, changing the attributes to match the image moniker you want to use.
             In this case, we're using the Guid for the VS image catalog.
             Change the id attribute to be the ID of the desired image moniker. -->
        <Icon guid="ImageCatalogGuid" id="OpenFolder" />
        <CommandFlag>DynamicVisibility</CommandFlag>
        <CommandFlag>DefaultInvisible</CommandFlag>
        <CommandFlag>DefaultDisabled</CommandFlag>
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>IconAndText</CommandFlag>
        <!-- Add the IconIsMoniker CommandFlag -->
        <CommandFlag>IconIsMoniker</CommandFlag>
        <Strings>
          <ButtonText>Quick Fixes...</ButtonText>
          <CommandName>Show Quick Fixes</CommandName>
          <CanonicalName>ShowQuickFixes</CanonicalName>
          <LocCanonicalName>ShowQuickFixes</LocCanonicalName>
        </Strings>
      </Button>
    </Buttons>
  </Commands>
  <!-- It is recommended that you remove <Bitmap> elements that are no longer used in the vsct file -->
  <Symbols>
    <GuidSymbol name="guidMyPackage"    value="{1491e936-6ffe-474e-8371-30e5920d8fdd}" />
    <GuidSymbol name="guidMyCommandSet" value="{10347de4-69a9-47f4-a950-d3301f6d2bc7}">
      <IDSymbol name="cmdidMyCommand" value="0x9437" />
    </GuidSymbol>
  </Symbols>
</CommandTable>
```

 **如果我的 .vsct 文件还需要由旧版本的 Visual Studio 读取，该怎么办？**

 较旧版本的 Visual Studio 无法识别**图标 IsMoniker**命令标志。 您可以在支持该图像工作室的 Visual Studio 版本上使用影像服务中的图像，但在旧版本的 Visual Studio 上继续使用旧式图像。 为此，您将保持 *.vsct*文件不变（因此与旧版本的 Visual Studio 兼容），并创建一个 CSV（逗号分隔值）文件，该文件从 *.vsct*文件中\<定义的 GUID/ID 对映射到图像名字对象 GUID/ID 对>元素。

 映射 CSV 文件的格式是：

```
Icon guid, Icon id, Moniker guid, Moniker id
b714fcf7-855e-4e4c-802a-1fd87144ccad,1,fda30684-682d-421c-8be4-650a2967058e,100
b714fcf7-855e-4e4c-802a-1fd87144ccad,2,fda30684-682d-421c-8be4-650a2967058e,200
```

 CSV 文件随包一起部署，其位置由**ProvideMenuResource**包属性的**IconMappingFilename**属性指定：

```csharp
[ProvideMenuResource("MyPackage.ctmenu", 1, IconMappingFilename="IconMappings.csv")]
```

 **IconMappingFilename**要么是隐式植根于 $PackageFolder$的相对路径（如上例所示），或者是一个显式植根于环境变量定义的目录（如 *_"%userProfile%%_dir1_dir2_MyMappingFile.csv"）* 的绝对路径。

## <a name="how-do-i-port-a-project-system"></a>如何移植项目系统？
 **如何为项目提供图像Monikers**

1. 在项目的**IV 层次结构**上实施**VSHPROPID_SupportsIconMonikers，** 然后返回 true。

2. 实施**VSHPROPID_IconMonikerImageList（** 如果原始项目使用**VSHPROPID_IconImgList）** 或**VSHPROPID_IconMonikerGuid**VSHPROPID_IconMonikerGuid、VSHPROPID_IconMonikerId、VSHPROPID_OpenFolderIconMonikerGuid、VSHPROPID_OpenFolderIconMonikerId（**VSHPROPID_OpenFolderIconMonikerId**如果原始项目使用**VSHPROPID_IconHandle**和**VSHPROPID_OpenFolderIconHandle）。** **VSHPROPID_IconMonikerId** **VSHPROPID_OpenFolderIconMonikerGuid**

3. 更改图标的原始 VSHPROPID 的实现，以创建图标的"旧"版本（如果扩展点请求）。 **IVsImageService2**提供了获取这些图标所需的功能

   **VB/C++ 项目风格的额外要求**

   只有当你检测到你的项目是最**外在的味道**时，才实现**VSHPROPID_SupportsIconMonikers。** 否则，实际最外在的味道可能不支持图像名字在现实中，你的基本风味可能有效地"隐藏"自定义图像。

   **如何在 CPS 中使用图像名字？**

   在 CPS（通用项目系统）中设置自定义映像可以手动或通过项目系统扩展 SDK 附带的项目模板进行。

   **使用项目系统扩展性 SDK**

   按照"[为项目类型/项目类型提供自定义图标](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/scenario/provide_custom_icons_for_the_project_or_item_type.md)"中的说明进行自定义自定义 CPS 图像。 有关 CPS 的更多信息，请参阅[可视化工作室项目系统扩展文档](https://github.com/Microsoft/VSProjectSystem)

   **手动使用图像 Monikers**

4. 在项目系统中实现并导出**IProjectTree 修改器**接口。

5. 确定要使用的**已知 Moniker**或自定义图像名称。

6. 在**应用修改**方法中，在返回新树之前，在方法的某处执行以下操作，类似于下面的示例：

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   tree = tree.SetIcon(KnownMonikers.Blank.ToProjectSystemType());
   ```

7. 如果要创建新树，则可以通过将所需的名字对象传递到 NewTree 方法来设置自定义图像，类似于下面的示例：

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   ProjectImageMoniker icon         = KnownMonikers.FolderClosed.ToProjectSystemType();
   ProjectImageMoniker expandedIcon = KnownMonikers.FolderOpened.ToProjectSystemType();

   return this.ProjectTreeFactory.Value.NewTree(/*caption*/<value>,
                                                /*filePath*/<value>,
                                                /*browseObjectProperties*/<value>,
                                                icon,
                                                expandedIcon);
   ```

## <a name="how-do-i-convert-from-a-real-image-strip-to-a-moniker-based-image-strip"></a>如何从真实图像条转换为基于名字的图像条？
 **我需要支持HIMAGELISTs**

 如果代码已有图像条要更新以使用映像服务，但受需要传递图像列表的 API 的限制，您仍然可以获得映像服务的好处。 要创建基于名字的图像条，请按照以下步骤从现有名字对象创建清单。

1. 运行 **"清单源"** 工具，将其传递给图像条。 这将生成条带的清单。

   - 建议：为清单提供非默认名称，以适应其用法。

2. 如果您只使用**已知莫尼克斯**，则执行以下操作：

   - 将\<清单>图像部分替换为\<图像/>。

   - 删除所有子图像指示（任何具有\<图像行程名称>_*）。

   - 建议：重命名 AssetsGuid 符号和图像条形符号，以适应其用途。

   - 将每个**包含图像**的 GUID 替换为 $（图像目录Guid），将每个**包含图像**的 ID\<替换为 $（名字对象>），并将外部="true"属性添加到每个**包含图像**

       - \<名字>应该被与图像匹配的**已知莫尼克尔**替换，但替换为"已知莫尼克器"。 从名称中删除。

   - 将<导入清单\"$（清单文件夹）<\\相对安装目录路径添加到\>@Microsoft.VisualStudio.ImageCatalog.imagemanifest"/>\*到\<"符号>"部分的顶部。

       - 相对路径由清单的设置创作中定义的部署位置确定。

3. 运行**清单ToCode**工具以生成包装，以便现有代码具有可用于查询图像条的图像服务的名字。

   - 建议：为包装器和命名空间提供非默认名称，以适应其用法。

4. 执行所有添加、设置创作/部署和其他代码更改，以便使用影像服务和新文件。

   示例清单，包括内部和外部图像，以查看它应该是什么样子：

```xml
<?xml version="1.0"?>
<ImageManifest
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns="http://schemas.microsoft.com/VisualStudio/ImageManifestSchema/2014">

  <Symbols>
    <!-- This needs to be the relative path from your manifest to the ImageCatalog's manifest
         where $(ManifestFolder) is the deployed location of this manifest. -->
    <Import Manifest="$(ManifestFolder)\<RelPath>\Microsoft.VisualStudio.ImageCatalog.imagemanifest" />

    <String Name="Resources" Value="/My.Assembly.Name;Component/Resources/ImageStrip" />
    <Guid Name="ImageGuid" Value="{fb41b7ef-6587-480c-aa27-5b559d42cfc9}" />
    <Guid Name="ImageStripGuid" Value="{9c84a570-d9a7-4052-a340-188fb276f973}" />
    <ID Name="MyImage_0" Value="100" />
    <ID Name="MyImage_1" Value="101" />
    <ID Name="InternalList" Value="1001" />
    <ID Name="ExternalList" Value="1002" />
  </Symbols>

  <Images>
    <Image Guid="$(ImageGuid)" ID="$(MyImage_0)">
      <Source Uri="$(Resources)/MyImage_0.png">
        <Size Value="16" />
      </Source>
    </Image>
    <Image Guid="$(ImageGuid)" ID="$(MyImage_1)">
      <Source Uri="$(Resources)/MyImage_1.png">
        <Size Value="16" />
      </Source>
    </Image>
  </Images>

  <ImageLists>
    <ImageList Guid="$(ImageStripGuid)" ID="$(InternalList)">
      <ContainedImage Guid="$(ImageGuid)" ID="$(MyImage_0)" />
      <ContainedImage Guid="$(ImageGuid)" ID="$(MyImage_1)" />
    </ImageList>
    <ImageList Guid="$(ImageStripGuid)" ID="$(ExternalList)">
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusError)" External="true" />
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusWarning)" External="true" />
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusInformation)" External="true" />
    </ImageList>
  </ImageLists>

</ImageManifest>
```

 **我不需要支持HIMAGELISTs**

1. 确定与图像条中的图像匹配的**已知莫尼克斯集**，或为图像条中的图像创建自己的名字。

2. 更新用于在图像条中所需索引获取图像的任何映射，以改用名字。

3. 更新代码以使用影像服务通过更新的映射请求名字。 （这可能意味着更新到**CrispImage**的托管代码，或从映像服务请求 HBITMAP 或 HICON，并将其传递给本机代码。

## <a name="testing-your-images"></a>测试图像
 您可以使用图像库查看器工具测试图像清单，以确保所有内容都正确创作。 您可以在[可视化工作室 2015 SDK](visual-studio-sdk.md)中找到该工具。 此工具和其他文档[可在此处](/visualstudio/extensibility/internals/vssdk-utilities?view=vs-2015)找到。

## <a name="additional-resources"></a>其他资源

### <a name="samples"></a>示例
 GitHub 上的多个 Visual Studio 示例已更新，以演示如何将影像服务用作各种 Visual Studio 扩展点的一部分。

 检查[http://github.com/Microsoft/VSSDK-Extensibility-Samples](https://github.com/Microsoft/VSSDK-Extensibility-Samples)最新样品。

### <a name="tooling"></a>工具
 为映像服务创建了一组支持工具，以帮助创建/更新与影像服务配合工作的 UI。 有关每个工具的详细信息，请查看工具随附的文档。 这些工具包含在[Visual Studio 2015 SDK](visual-studio-sdk.md)中。

 **清单来自资源**

 "来自资源清单"工具获取图像资源列表（PNG 或 XAML），并生成用于将这些图像与影像服务一起使用的图像清单文件。

 **清单代码**

 "清单到代码"工具采用图像清单文件并生成一个包装文件，用于引用代码（C++、C#或 VB）或 *.vsct*文件中的清单值。

 **图像库查看器**

 图像库查看器工具可以加载图像清单，并允许用户以 Visual Studio 相同的方式操作它们，以确保该清单的创作正确。 用户可以更改背景、大小、DPI 设置、高对比度和其他设置。 它还显示加载信息以查找清单中的错误，并显示清单中每个图像的源信息。

## <a name="faq"></a>常见问题解答

- 加载\<参考包含时必须包含的任何依赖项。"Microsoft.VisualStudio.*"。Interop.14.0.设计时间"/>？

  - 在所有互通 DLL 上设置嵌入 InteropType="true"。

- 如何使用扩展部署映像清单？

  - 将 *.image 清单*文件添加到项目中。

  - 将"包含在 VSIX 中"设置为"true"。

- 我正在更新我的 CPS 项目系统。 **图片名称**和**库存服务**发生了什么？

  - 当 CPS 更新以使用名字器时，这些删除。 您不再需要调用**StockIcon 服务**，只需使用 CPS 实用程序中的**ToProjectSystemType（）** 扩展方法将所需的**已知 Moniker**传递给方法或属性即可。 您可以在下面找到从**图像名称**到**已知莫尼克斯的**映射：

    |||
    |-|-|
    |**ImageName**|**已知莫尼克尔**|
    |图片名称.离线网络应用|已知图像 Ids.Web|
    |图像名称.Web引用文件夹|已知图像 Ids.Web|
    |图像名称.打开引用文件夹|已知图像 Id.文件夹打开|
    |图像名称.参考文件夹|已知图像 Id.参考|
    |图像名称.参考|已知图像 Id.参考|
    |图像名称.SdlWeb参考|已知图像 Id.Web 参考文件夹|
    |图片名称.DiscoWeb参考|已知图像 Id.动态发现文档|
    |图像名称.文件夹|已知图像 Id.文件夹已关闭|
    |图像名称.打开文件夹|已知图像 Id.文件夹打开|
    |图像名称.排除文件夹|已知图像 Id.隐藏文件夹已关闭|
    |图像名称.打开排除文件夹|已知图像 Id.隐藏文件夹打开|
    |图像名称.排除文件|已知图像 Id.隐藏文件|
    |图像名称.从属文件|已知图像 Id.生成文件|
    |图像名称.缺少文件|已知图像 Id.文档警告|
    |图像名称.窗口窗体|已知图像 Id.WindowsForm|
    |图像名称.Windows用户控制|已知图像 Id.用户控制|
    |图像名称.窗口组件|已知图像 Id.组件文件|
    |图像名称.XmlSchema|已知图像 Ids.XMLSchema|
    |图像名称.Xml文件|已知图像 Ids.XML 文件|
    |图片名称.WebForm|已知图像 Ids.Web|
    |图片名称.Web服务|已知图像 Ids.Web 服务|
    |图像名称.Web用户控制|已知图像 Id.Web用户控制|
    |图像名称.Web自定义用户控制|已知图像 Id.Web 自定义控制|
    |图片名称.Asppage|已知图像 Id.ASP文件|
    |图像名称.全局应用程序类|已知图像 Id.设置文件|
    |图片名称.Web 配置|已知图像 Id.配置文件|
    |图片名称.htmlPage|已知图像 Ids.HTML文件|
    |图像名称.样式表|已知图像 Id.样式表|
    |图像名称.脚本文件|已知图像 Id.JSScript|
    |图片名称.文本文件|已知图像 Id.文档|
    |图像名称.设置文件|已知图像 Id.设置|
    |图像名称.资源|已知图像 Id.文档组|
    |图像名称.位图|已知图像 Id.图像|
    |图像名称.图标|已知图像 Id.图标文件|
    |图像名称.图像|已知图像 Id.图像|
    |图像名称.图像映射|已知图像 Id.图像映射文件|
    |图片名称.X世界|已知图像 Ids.XWorldFile|
    |图像名称.音频|已知图像 Ids.声音|
    |图片名称.视频|已知图像 Id.媒体|
    |图像名称.Cab|已知图像 Id.CAB 项目|
    |图像名称.Jar|已知图像 Ids.JARFile|
    |图像名称.数据环境|已知图像 Id.数据表|
    |图像名称.预览文件|已知图像 Ids.报告|
    |图像名称.悬空参考|已知图像 Id.参考警告|
    |图像名称.Xslt文件|已知图像 Id.XSL 转换|
    |图像名称.光标|已知图像 Id.光标文件|
    |图像名称.应用设计文件夹|已知图像 Id.属性|
    |图像名称.数据|已知图像 Id.数据库|
    |图像名称.应用程序|已知图像 Id.应用程序|
    |图像名称.数据集|已知图像 Id.数据库组|
    |图像名称.Pfx|已知图像 Id.证书|
    |图像名称.Snk|已知图像 Id.Rule|
    |图像名称.可视化基础项目|已知图像 Id.VB 项目节点|
    |图像名称.C夏普项目|已知图像 Id.CSProjectNode|
    |图像名称.空|已知图像 Id.Blank|
    |图像名称.缺少文件夹|已知图像 Id.文件夹脱机|
    |图像名称.共享导入参考|已知图像 Id.共享项目|
    |图像名称.共享项目|已知图像 Ids.CS 共享项目|
    |图像名称.共享项目Vc|已知图像 Id.CPP 共享项目|
    |图像名称.共享项目J|已知图像 Ids.JS 共享项目|
    |图像名称.C夏普代码文件|已知图像 Id.CSFileNode|
    |图像名称.视觉基本代码文件|已知图像 Id.VBFileNode|

  - 我正在更新我的完成列表提供程序。 什么**已知莫尼克器**与旧的**标准字形组**和**标准字**形值相匹配？

    ||||
    |-|-|-|
    |字形组类|字形项目公开|类公共|
    |字形组类|字形项目内部|类内部|
    |字形组类|字形项目朋友|类内部|
    |字形组类|字形项目保护|类保护|
    |字形组类|字形项目私人|类私有|
    |字形组类|字形项目快捷方式|类快捷方式|
    |字形组常数|字形项目公开|常量公共|
    |字形组常数|字形项目内部|常量内部|
    |字形组常数|字形项目朋友|常量内部|
    |字形组常数|字形项目保护|恒定保护|
    |字形组常数|字形项目私人|常点私人|
    |字形组常数|字形项目快捷方式|常量快捷|
    |字形组代表|字形项目公开|委托公共|
    |字形组代表|字形项目内部|委托内部|
    |字形组代表|字形项目朋友|委托内部|
    |字形组代表|字形项目保护|委托保护|
    |字形组代表|字形项目私人|委托私人|
    |字形组代表|字形项目快捷方式|委托快捷方式|
    |字形组|字形项目公开|枚举公共|
    |字形组|字形项目内部|枚举内部|
    |字形组|字形项目朋友|枚举内部|
    |字形组|字形项目保护|枚举保护|
    |字形组|字形项目私人|枚举私人|
    |字形组|字形项目快捷方式|枚举快捷方式|
    |字形组成员|字形项目公开|枚举项目公开|
    |字形组成员|字形项目内部|枚举项目内部|
    |字形组成员|字形项目朋友|枚举项目内部|
    |字形组成员|字形项目保护|枚举项目保护|
    |字形组成员|字形项目私人|枚举项目专用|
    |字形组成员|字形项目快捷方式|枚举项目快捷方式|
    |字形集团事件|字形项目公开|事件公共|
    |字形集团事件|字形项目内部|事件内部|
    |字形集团事件|字形项目朋友|事件内部|
    |字形集团事件|字形项目保护|事件保护|
    |字形集团事件|字形项目私人|事件私人|
    |字形集团事件|字形项目快捷方式|事件快捷方式|
    |字形组例外|字形项目公开|异常公共|
    |字形组例外|字形项目内部|异常内部|
    |字形组例外|字形项目朋友|异常内部|
    |字形组例外|字形项目保护|异常保护|
    |字形组例外|字形项目私人|例外私有|
    |字形组例外|字形项目快捷方式|异常快捷方式|
    |字形组场|字形项目公开|现场公共|
    |字形组场|字形项目内部|字段内部|
    |字形组场|字形项目朋友|字段内部|
    |字形组场|字形项目保护|现场保护|
    |字形组场|字形项目私人|字段私人|
    |字形组场|字形项目快捷方式|字段快捷方式|
    |字形组接口|字形项目公开|接口公共|
    |字形组接口|字形项目内部|接口内部|
    |字形组接口|字形项目朋友|接口内部|
    |字形组接口|字形项目保护|接口保护|
    |字形组接口|字形项目私人|接口专用|
    |字形组接口|字形项目快捷方式|界面快捷方式|
    |字形集团Macro|字形项目公开|宏公共|
    |字形集团Macro|字形项目内部|宏内部|
    |字形集团Macro|字形项目朋友|宏内部|
    |字形集团Macro|字形项目保护|宏保护|
    |字形集团Macro|字形项目私人|宏私有|
    |字形集团Macro|字形项目快捷方式|宏快捷方式|
    |字形组图|字形项目公开|地图公共|
    |字形组图|字形项目内部|地图内部|
    |字形组图|字形项目朋友|地图内部|
    |字形组图|字形项目保护|地图保护|
    |字形组图|字形项目私人|地图专用|
    |字形组图|字形项目快捷方式|地图快捷方式|
    |字形组映射项目|字形项目公开|地图项目公共|
    |字形组映射项目|字形项目内部|映射项目内部|
    |字形组映射项目|字形项目朋友|映射项目内部|
    |字形组映射项目|字形项目保护|地图项目保护|
    |字形组映射项目|字形项目私人|映射项目私有|
    |字形组映射项目|字形项目快捷方式|映射项目快捷方式|
    |字形组方法|字形项目公开|方法公开|
    |字形组方法|字形项目内部|方法内部|
    |字形组方法|字形项目朋友|方法内部|
    |字形组方法|字形项目保护|MethodProtected|
    |字形组方法|字形项目私人|方法私有|
    |字形组方法|字形项目快捷方式|方法快捷方式|
    |字形组过载|字形项目公开|方法公开|
    |字形组过载|字形项目内部|方法内部|
    |字形组过载|字形项目朋友|方法内部|
    |字形组过载|字形项目保护|MethodProtected|
    |字形组过载|字形项目私人|方法私有|
    |字形组过载|字形项目快捷方式|方法快捷方式|
    |字形组模块|字形项目公开|模块公共|
    |字形组模块|字形项目内部|模块内部|
    |字形组模块|字形项目朋友|模块内部|
    |字形组模块|字形项目保护|模块保护|
    |字形组模块|字形项目私人|模块私有|
    |字形组模块|字形项目快捷方式|模块快捷方式|
    |字形组命名空间|字形项目公开|命名空间公共|
    |字形组命名空间|字形项目内部|命名空间内部|
    |字形组命名空间|字形项目朋友|命名空间内部|
    |字形组命名空间|字形项目保护|命名空间保护|
    |字形组命名空间|字形项目私人|命名空间私人|
    |字形组命名空间|字形项目快捷方式|命名空间快捷方式|
    |字形组操作员|字形项目公开|操作员公共|
    |字形组操作员|字形项目内部|操作员内部|
    |字形组操作员|字形项目朋友|操作员内部|
    |字形组操作员|字形项目保护|操作员保护|
    |字形组操作员|字形项目私人|操作员私人|
    |字形组操作员|字形项目快捷方式|操作员快捷方式|
    |字形集团属性|字形项目公开|属性公开|
    |字形集团属性|字形项目内部|属性内部|
    |字形集团属性|字形项目朋友|属性内部|
    |字形集团属性|字形项目保护|属性保护|
    |字形集团属性|字形项目私人|属性私人|
    |字形集团属性|字形项目快捷方式|属性快捷方式|
    |字形组结构|字形项目公开|结构公共|
    |字形组结构|字形项目内部|结构内部|
    |字形组结构|字形项目朋友|结构内部|
    |字形组结构|字形项目保护|结构保护|
    |字形组结构|字形项目私人|结构私有|
    |字形组结构|字形项目快捷方式|结构快捷方式|
    |字形组模板|字形项目公开|模板公开|
    |字形组模板|字形项目内部|模板内部|
    |字形组模板|字形项目朋友|模板内部|
    |字形组模板|字形项目保护|模板保护|
    |字形组模板|字形项目私人|模板专用|
    |字形组模板|字形项目快捷方式|模板快捷方式|
    |字形组类型def|字形项目公开|类型定义公共|
    |字形组类型def|字形项目内部|类型定义内部|
    |字形组类型def|字形项目朋友|类型定义内部|
    |字形组类型def|字形项目保护|类型定义保护|
    |字形组类型def|字形项目私人|类型定义私有|
    |字形组类型def|字形项目快捷方式|类型定义快捷方式|
    |字形组型|字形项目公开|类型公共|
    |字形组型|字形项目内部|类型内部|
    |字形组型|字形项目朋友|类型内部|
    |字形组型|字形项目保护|类型保护|
    |字形组型|字形项目私人|类型专用|
    |字形组型|字形项目快捷方式|类型快捷方式|
    |字形组联盟|字形项目公开|联合公共|
    |字形组联盟|字形项目内部|联合内部|
    |字形组联盟|字形项目朋友|联合内部|
    |字形组联盟|字形项目保护|联盟保护|
    |字形组联盟|字形项目私人|联合私人|
    |字形组联盟|字形项目快捷方式|联合快捷方式|
    |字形组变量|字形项目公开|现场公共|
    |字形组变量|字形项目内部|字段内部|
    |字形组变量|字形项目朋友|字段内部|
    |字形组变量|字形项目保护|现场保护|
    |字形组变量|字形项目私人|字段私人|
    |字形组变量|字形项目快捷方式|字段快捷方式|
    |字形组值类型|字形项目公开|价值类型公共|
    |字形组值类型|字形项目内部|值类型 内部|
    |字形组值类型|字形项目朋友|值类型 内部|
    |字形组值类型|字形项目保护|价值类型保护|
    |字形组值类型|字形项目私人|值类型私有|
    |字形组值类型|字形项目快捷方式|值类型快捷方式|
    |字形组内生|字形项目公开|对象公共|
    |字形组内生|字形项目内部|对象内部|
    |字形组内生|字形项目朋友|对象内部|
    |字形组内生|字形项目保护|对象保护|
    |字形组内生|字形项目私人|对象专用|
    |字形组内生|字形项目快捷方式|对象快捷方式|
    |字形组J夏普法|字形项目公开|方法公开|
    |字形组J夏普法|字形项目内部|方法内部|
    |字形组J夏普法|字形项目朋友|方法内部|
    |字形组J夏普法|字形项目保护|MethodProtected|
    |字形组J夏普法|字形项目私人|方法私有|
    |字形组J夏普法|字形项目快捷方式|方法快捷方式|
    |字形组J夏普菲尔德|字形项目公开|现场公共|
    |字形组J夏普菲尔德|字形项目内部|字段内部|
    |字形组J夏普菲尔德|字形项目朋友|字段内部|
    |字形组J夏普菲尔德|字形项目保护|现场保护|
    |字形组J夏普菲尔德|字形项目私人|字段私人|
    |字形组J夏普菲尔德|字形项目快捷方式|字段快捷方式|
    |字形组J夏普类|字形项目公开|类公共|
    |字形组J夏普类|字形项目内部|类内部|
    |字形组J夏普类|字形项目朋友|类内部|
    |字形组J夏普类|字形项目保护|类保护|
    |字形组J夏普类|字形项目私人|类私有|
    |字形组J夏普类|字形项目快捷方式|类快捷方式|
    |字形组J夏普命名空间|字形项目公开|命名空间公共|
    |字形组J夏普命名空间|字形项目内部|命名空间内部|
    |字形组J夏普命名空间|字形项目朋友|命名空间内部|
    |字形组J夏普命名空间|字形项目保护|命名空间保护|
    |字形组J夏普命名空间|字形项目私人|命名空间私人|
    |字形组J夏普命名空间|字形项目快捷方式|命名空间快捷方式|
    |字形组JJJJ接口|字形项目公开|接口公共|
    |字形组JJJJ接口|字形项目内部|接口内部|
    |字形组JJJJ接口|字形项目朋友|接口内部|
    |字形组JJJJ接口|字形项目保护|接口保护|
    |字形组JJJJ接口|字形项目私人|接口专用|
    |字形组JJJJ接口|字形项目快捷方式|界面快捷方式|
    |字形组错误||StatusError|
    |字形BscFile||类文件|
    |字形组装||参考|
    |字形库||库|
    |字形VB项目||VB项目节点|
    |字形酷项目||CS项目节点|
    |字形方案项目||CPP项目节点|
    |字形对话Id||对话框|
    |字形打开文件夹||文件夹已打开|
    |字形封闭文件夹||文件夹已关闭|
    |字形箭||转到下一个|
    |字形C夏普文件||CSFileNode|
    |字形C夏普扩展||片段|
    |字形关键词||感知关键词|
    |字形信息||状态信息|
    |字形参考||类方法参考|
    |字形再体||递归|
    |字形项目||标记|
    |字形JJ夏普项目||DocumentCollection|
    |字形J夏普文件||Document|
    |字形前进类型||转到下一个|
    |字形呼叫图||呼叫|
    |字形标注||从|
    |字形警告||StatusWarning|
    |字形参考||问题标记|
    |字形可能呼叫者||呼叫|
    |字形可能呼叫||从|
    |字形延伸法||扩展方法|
    |字形延伸方法内部||扩展方法|
    |字形延伸方法朋友||扩展方法|
    |字形延伸方法保护||扩展方法|
    |字形延伸方法私人||扩展方法|
    |字形延伸方法快捷方式||扩展方法|
    |字形Xml属性||XmlAttribute|
    |字形儿童||XmlElement|
    |字形||XmlDescendant|
    |字形命名空间||XmlNamespace|
    |字形属性问题||XmlAttribute 低信心|
    |字形属性检查||XmlAttribute 高度自信|
    |字形儿童问题||XmlElement 低信心|
    |字形儿童检查||XmlElement 高度自信|
    |字形下降问题||XmlSsLowss 低信心|
    |字形降验||XmlDescendant高信心|
    |字形完成警告||感知警告|
