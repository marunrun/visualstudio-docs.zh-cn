---
title: 图像库查看器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 9d9c7fbb-ebae-4b20-9dd8-3c9070c0d0d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a7c5eda24c235cddec99cb5177c6ed315978bc6f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707752"
---
# <a name="image-library-viewer"></a>图像库查看器
可视化工作室图像库查看器工具可以加载和搜索图像清单，允许用户以视觉工作室相同的方式操作它们。 用户可以更改背景、大小、DPI、高对比度和其他设置。 该工具还显示每个图像清单的加载信息，并显示图像清单中每个图像的源信息。 此工具可用于：

1. 诊断错误

2. 确保在自定义映像清单中正确设置属性

3. 在可视化工作室图像目录中搜索图像，以便可视化工作室扩展可以使用适合视觉工作室样式的图像

   ![图像库查看器 Hero](../../extensibility/internals/media/image-library-viewer-hero.png "图像库查看器 Hero")

   **图像名字**

   图像名称对象（简称名称）是 GUID：ID 对，用于唯一标识图像库中的图像资产或图像列表资产。

   **图像清单文件**

   图像清单 （.imagemanifest） 文件是定义一组图像资产的 XML 文件、表示这些资产的名号以及表示每个资产的真实图像或图像。 映像清单可以为旧版 UI 支持定义独立映像或图像列表。 此外，还可以在每个资产后面的单个图像上设置一些属性，以更改这些资产的显示时间以及方式。

   **映像清单架构**

   完整的图像清单如下所示：

```xml
<ImageManifest>
      <!-- zero or one Symbols elements -->
      <Symbols>
        <!-- zero or more Guid, ID, or String elements -->
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
|导入|导入给定清单文件的符号，用于当前清单。|
|Guid|符号表示 GUID，必须匹配 GUID 格式。|
|ID|符号表示 ID，并且必须是非负整数。|
|字符串|符号表示任意字符串值。|

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
|系统|Windows_System32 文件夹|
|温迪尔|%WinDir% 环境变量的值|

 **映像**

 图像\<>元素定义一个可以由名字对象引用的图像。 GUID 和 ID 一起构成图像名字。 图像的绰号必须在整个图像库中是唯一的。 如果多个图像具有给定的名字对象，则构建库时遇到的第一个图像是保留的映像。

 它必须至少包含一个源。 尽管大小中性源将在各种尺寸中提供最佳结果，但它们不是必需的。 如果要求服务提供\<未在 Image> 元素中定义的大小图像，并且没有大小无关的源，则服务将选择最佳特定于大小的源并将其缩放到请求的大小。

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
|Uri|[必需]定义图像从何处加载的 URI。 该参数可以是下列值之一：<br /><br /> - 使用application:///权限的[包 URI](/dotnet/framework/wpf/app-development/pack-uris-in-wpf)<br /><br /> - 绝对组件资源引用<br /><br /> - 包含本机资源的文件的路径|
|背景|[可选]指示源在哪些背景上打算使用。<br /><br /> 该参数可以是下列值之一：<br /><br /> - *光*：光源可用于光背景。<br /><br /> - *黑暗*：源可用于深色背景。<br /><br /> - *高对比度*：源可用于高对比度模式下的任何背景。<br /><br /> - *高对比度光*：光源可在高对比度模式下在光背景上使用。<br /><br /> -*高对比度暗*：源可用于高对比度模式下的黑暗背景。<br /><br /> 如果省略**了背景**属性，则源可用于任何背景。<br /><br /> 如果**背景**是 *"浅色*"、*暗*色、*高对比度或**高对比度暗*，则源的颜色永远不会反转。 如果"**背景**"省略或设置为 *"高对比度*"，则源颜色的反转由图像的**AllowColor 反转**属性控制。|

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

## <a name="how-to-use-the-tool"></a>如何使用该工具
 **验证自定义映像清单**

 要创建自定义清单，我们建议您使用"清单源"工具自动生成清单。 要验证自定义清单，请启动映像库查看器并选择文件>设置路径...以打开"搜索目录"对话框。 该工具将使用搜索目录加载图像清单，但它也会使用它们来查找包含清单中图像的 .dll 文件，因此请确保在此对话框中同时包含清单和 DLL 目录。

 ![图像库查看器 搜索](../../extensibility/internals/media/image-library-viewer-search.png "图像库查看器 搜索")

 单击"**添加..."** 以选择新的搜索目录以搜索清单及其相应的 DLL。 该工具将记住这些搜索目录，并且可以通过检查或取消检查目录来打开或关闭它们。

 默认情况下，该工具将尝试查找 Visual Studio 安装目录，并将这些目录添加到搜索目录列表中。 您可以手动添加工具找不到的目录。

 加载所有清单后，该工具可用于切换图像**的背景**颜色 **、DPI、****高对比度**或**灰度，** 以便用户可以直观地检查图像资产，以验证它们是否正确呈现为各种设置。

 ![图像库查看器 背景](../../extensibility/internals/media/image-library-viewer-background.png "图像库查看器 背景")

 背景颜色可以设置为"浅色"、深色或自定义值。 选择"自定义颜色"将打开颜色选择对话框，并将自定义颜色添加到背景组合框的底部，以便以后轻松调用。

 ![图像库查看器的自定义颜色](../../extensibility/internals/media/image-library-viewer-custom-color.png "图像库查看器的自定义颜色")

 选择图像名字对象会在右侧的"图像详细信息"窗格中显示该名字对象后面的每个真实图像的信息。 该窗格还允许用户按名称或原始 GUID：ID 值复制名字对象。

 ![图像库查看器 图像详细信息](../../extensibility/internals/media/image-library-viewer-image-details.png "图像库查看器 图像详细信息")

 为每个图像源显示的信息包括要显示它的背景类型、是否可以以主题或支持高对比度、它适用于什么大小或大小是否中性，以及图像是否来自本机程序集。

 ![图像库查看器 罐形主题](../../extensibility/internals/media/image-library-viewer-can-theme.png "图像库查看器 罐形主题")

 验证映像清单时，我们建议您在其实际位置部署清单和映像 DLL。 这将验证任何相对路径是否正常工作，以及图像库是否可以查找和加载清单和图像 DLL。

 **搜索图像目录 已知莫尼克斯**

 为了更好地匹配 Visual Studio 样式，Visual Studio 扩展可以使用 Visual Studio 图像目录中的图像，而不是创建和使用自己的图像。 这样做的好处是不必维护这些图像，并且保证图像具有高 DPI 支持图像，因此在 Visual Studio 支持的所有 DPI 设置中，图像看起来应该是正确的。

 图像库查看器允许搜索清单，以便用户可以找到表示图像资产的绰号，并在代码中使用该名字对象。 要搜索图像，请在搜索框中输入所需的搜索词，然后按 Enter。 底部的状态栏将显示从所有清单中的总图像中找到的匹配项数。

 ![图像库查看器 筛选器](../../extensibility/internals/media/image-library-viewer-filter.png "图像库查看器 筛选器")

 在现有清单中搜索图像名字对象时，我们建议您仅搜索和使用 Visual Studio 图像目录的名言、其他有意公开访问的名字，或者您自己的自定义名字。 如果使用非公共名字，如果更改或更新这些非公共名字对象和图像，自定义 UI 可能会中断或以意外方式更改其映像。

 此外，还可以通过 GUID 进行搜索。 这种类型的搜索可用于将列表筛选到单个清单，或者如果清单包含多个 GUID，则该清单的单个子节。

 ![图像库查看器 筛选器 GUID](../../extensibility/internals/media/image-library-viewer-filter-guid.png "图像库查看器 筛选器 GUID")

 最后，也可以按 ID 进行搜索。

 ![图像库查看器 筛选器 ID](../../extensibility/internals/media/image-library-viewer-filter-id.png "图像库查看器 筛选器 ID")

## <a name="notes"></a>说明

- 默认情况下，该工具将拉取 Visual Studio 安装目录中存在的多个图像清单。 唯一具有公开易用名字的，是**微软.VisualStudio.ImageCatalog**清单。 GUID： ae27a6b0-e345-4288-96df-5eaf394ee369 （**不要**在自定义清单中覆盖此 GUID） 类型： 已知Monikers

- 该工具尝试启动以加载它找到的所有映像清单，因此应用程序可能需要几秒钟才能实际显示。 加载清单时，它也可能很慢或无响应。

## <a name="sample-output"></a>示例输出
 此工具不生成任何输出。
