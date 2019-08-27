---
title: 图像库查看器 |Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 9d9c7fbb-ebae-4b20-9dd8-3c9070c0d0d1
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 97d634f97eb7a13cfa54b2c0d326b19f31fb7d9d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65685571"
---
# <a name="image-library-viewer"></a>图像库查看器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio 图像库查看器工具可以加载并搜索图像的清单，从而允许用户在相同的方式将 Visual Studio 中处理它们。 用户可以更改背景、 大小、 DPI、 高对比度和其他设置。 该工具也会显示正在加载信息为每个映像清单和映像清单中显示的每个映像的源信息。 此工具可用于：  
  
1. 诊断错误  
  
2. 在自定义映像的清单中正确设置确保属性  
  
3. 搜索 Visual Studio 映像目录中的映像，以便 Visual Studio 扩展可以使用适合的 Visual Studio 样式的图像  
  
   ![图像库查看器 Hero](../../extensibility/internals/media/image-library-viewer-hero.png "图像库查看器 Hero")  
  
   **图像名字对象**  
  
   图像名字对象 （或简称名字对象） 是唯一标识图像资产或映像库中的图像列表资产的 guid: id 对。  
  
   **图像清单文件**  
  
   图像清单 (.imagemanifest) 文件的 XML 文件，用于定义一组图像资产，表示这些资产和实际的图像或图像，表示每个资产的名字对象。 图像的清单可以定义独立图像或图像列表的旧 UI 支持。 此外，还有设置的属性可以在资产或隐藏每个资产的各个图像上更改何时以及如何显示这些资产。  
  
   **图像清单架构**  
  
   完成映像清单如下所示：  
  
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
  
 **符号**  
  
 可读性和维护的帮助，因为图像清单可以使用属性值的符号。 此类定义了符号：  
  
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
|导入|导入当前清单中使用的给定清单文件的符号。|  
|GUID|该符号表示一个 GUID，并且必须匹配 GUID 的格式设置。|  
|Id|符号表示一个 ID，并必须为非负整数。|  
|String|该符号表示任意字符串值。|  
  
 符号是区分大小写，并引用使用 $(symbol-name) 语法：  
  
```xml  
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >  
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />  
</Image>  
```  
  
 某些符号预定义的所有清单。 这些可在 Uri 特性\<源 > 或\<导入 > 到本地计算机上的引用路径的元素。  
  
|||  
|-|-|  
|**符号**|**说明**|  
|CommonProgramFiles|%Commonprogramfiles%环境变量的值|  
|LocalAppData|%Localappdata%环境变量的值|  
|ManifestFolder|包含清单的文件的文件夹|  
|MyDocuments|当前用户的我的文档文件夹的完整路径|  
|ProgramFiles|%Programfiles%环境变量的值|  
|系统|Windows\System32 文件夹|  
|WinDir|%Windir%环境变量的值|  
  
 **Image**  
  
 \<图像 > 元素定义可由一个名字对象引用的图像。 GUID 和 ID 合起来构成图像名字对象。 跨整个图像库的图像名字对象必须是唯一的。 如果多个映像具有给定名字对象，生成库时遇到的第一个是保留的。  
  
 它必须包含至少一个源。 尽管非特定大小的源将跨各种大小提供最佳的结果，这些内容并非必需。 如果服务要求中未定义的大小的图像\<图像 > 元素和没有非特定大小的源，则服务将选择最佳的大小特定于源并将其缩放到所请求的大小。  
  
```xml  
<Image Guid="guid" ID="int" AllowColorInversion="true/false">  
      <Source ... />  
      <!-- optional additional Source elements -->  
</Image>  
```  
  
|||  
|-|-|  
|**特性**|**定义**|  
|GUID|[必需]图像名字对象的 GUID 部分|  
|Id|[必需]图像名字对象 ID 部分|  
|AllowColorInversion|[可选，默认为 true]指示图像是否可以具有它以编程方式反转深色背景上使用时的颜色。|  
  
 **源**  
  
 \<源 > 元素定义单一映像源资产 （XAML 和 PNG）。  
  
```xml  
<Source Uri="uri" Background="background">  
      <!-- optional NativeResource element -->  
 </Source>  
```  
  
|||  
|-|-|  
|**特性**|**定义**|  
|URI|[必需]一个 URI，定义可从中加载图像。 它可以是以下值之一：<br /><br /> -A [Pack URI](https://msdn.microsoft.com/library/aa970069\(v=vs.100\).aspx)使用应用程序: / / 颁发机构<br /><br /> -一个绝对组件资源引用<br /><br /> 的包含本机资源的文件路径|  
|背景|[可选]指示什么类型的源应使用的背景。<br /><br /> 它可以是以下值之一：<br /><br /> - *光*:源可以使用浅色背景上。<br /><br /> - *深色*:可以在深色背景上使用源。<br /><br /> - *高对比度*:可以在高对比度模式中的任何背景上使用源。<br /><br /> - *HighContrastLight*:可以在高对比度模式下浅色背景上使用源。<br /><br /> -*HighContrastDark*:可以在高对比度模式中的深色背景上使用源。<br /><br /> 如果**背景**省略属性，可以在任何的背景上使用了源。<br /><br /> 如果**背景**是*Light*，*深色*， *HighContrastLight*，或*HighContrastDark*、永远不会反转源的颜色。 如果**背景**省略或设为*对比度*，由图像的控制的源的颜色反转**AllowColorInversion**属性。|  
  
 一个\<源 > 元素可以具有以下可选子元素之一：  
  
||||  
|-|-|-|  
|**元素**|**属性 （全部所需）**|**定义**|  
|\<Size>|值|源将用于指定大小 （以设备为单位） 的映像。 图将方形。|  
|\<SizeRange>|MinSize, MaxSize|将映像从 MinSize 到最大大小 （以设备为单位） （含限值） 使用源。 图将方形。|  
|\<维度 >|宽度、 高度|源将用于给定的宽度和高度 （以设备为单位） 的映像。|  
|\<DimensionRange>|MinWidth，MinHeight，<br /><br /> MaxWidth MaxHeight|源将用于从最小宽度/高度 （以设备为单位） 的最大宽度/高度的图像 （含）。|  
  
 一个\<源 > 元素还具有一个可选\<NativeResource > 子元素，定义\<源 > 从本机程序集而不是托管程序集加载的。  
  
```xml  
<NativeResource Type="type" ID="int" />  
```  
  
|||  
|-|-|  
|**特性**|**定义**|  
|类型|[必需]类型的本机资源，XAML 或 PNG|  
|Id|[必需]本机资源的整数 ID 部分|  
  
 **ImageList**  
  
 \<ImageList > 元素定义的映像可以在单个条形中返回的集合。 根据需要将按需、 构建在条带。  
  
```xml  
<ImageList>  
      <ContainedImage Guid="guid" ID="int" External="true/false" />  
      <!-- optional additional ContainedImage elements -->  
 </ImageList>  
```  
  
|||  
|-|-|  
|**特性**|**定义**|  
|GUID|[必需]图像名字对象的 GUID 部分|  
|Id|[必需]图像名字对象 ID 部分|  
|外部|[可选，默认值为 false]指示图像名字对象是否引用当前清单中的图像。|  
  
 包含图像的名字对象没有引用当前清单中定义的图像。 如果在映像库中找不到包含的图像，将在其原位置使用空白的占位符图像。  
  
## <a name="how-to-use-the-tool"></a>如何使用该工具  
 **验证自定义映像清单**  
  
 若要创建自定义清单，我们建议你使用 ManifestFromResources 工具自动生成清单。 若要验证自定义清单，请启动图像库查看器并选择文件 > 设置路径... 若要打开搜索目录对话框。 该工具将使用搜索目录加载图像的清单，但它还将使用它它们若要查找的.dll 文件包含在清单中，映像因此请务必在此对话框中包括的清单和 DLL 的目录。  
  
 ![图像库查看器搜索](../../extensibility/internals/media/image-library-viewer-search.png "图像库查看器搜索")  
  
 单击**添加...** 可以选择新的搜索目录搜索清单和其相应的 Dll。 该工具会记住这些搜索目录，并且他们可以打开或关闭通过选中或取消选中一个目录。  
  
 默认情况下，该工具将尝试查找 Visual Studio 安装目录，并将这些目录添加到搜索目录列表。 您可以手动添加找不到该工具的目录。  
  
 一旦加载的所有清单，该工具可用于切换**背景**颜色**DPI**，**高对比度**，或**grayscaling**为映像，以便用户可以直观地检查图像资产，以确认它们正在正确呈现的各种设置。  
  
 ![图像库查看器背景](../../extensibility/internals/media/image-library-viewer-background.png "图像库查看器背景")  
  
 背景色可以设置为浅色、 深色或自定义值。 选择"自定义颜色"将打开颜色选择对话框，并将该自定义颜色添加到以便重新调用更高版本的后台组合框的底部。  
  
 ![图像库查看器自定义颜色](../../extensibility/internals/media/image-library-viewer-custom-color.png "图像库查看器自定义颜色")  
  
 选择图像名字对象右侧的映像详细信息窗格中显示每个实际的图像，该名字对象背后的信息。 在窗格还允许用户按名称或原始 guid: id 值将复制一个名字对象。  
  
 ![图像库查看器图像详细信息](../../extensibility/internals/media/image-library-viewer-image-details.png "图像库查看器图像详细信息")  
  
 显示每个图像源的信息包括哪些类型的背景以显示，指示是否可为主题或支持高对比度，它是有效的何种大小或它是否非特定大小，以及无论映像来自本机程序集。  
  
 ![图像库查看器罐形主题](../../extensibility/internals/media/image-library-viewer-can-theme.png "图像库查看器罐形主题")  
  
 在验证图像清单时，我们建议在部署清单和映像在其实际位置的 DLL。 这将验证任何相对路径能够正常工作并且图像库可以查找并加载清单和映像 DLL。  
  
 **搜索图像目录 KnownMonikers**  
  
 若要更好地匹配 Visual Studio 样式，Visual Studio 扩展可以使用 Visual Studio 映像目录而不是创建和使用其自己的映像。 这无需维护这些映像的好处，并保证该映像将有高 DPI 支持图像，因此其外观应在 Visual Studio 支持的所有 DPI 设置正确。  
  
 图像库查看器允许要在其中搜索，以便用户可以查找表示的图像资产的名字对象并在代码中使用该名字对象的清单。 若要搜索的映像，在搜索框中输入所需的搜索词，然后按 Enter。 在底部状态栏会显示多少个匹配项找出图像总数中所有清单。  
  
 ![图像库查看器筛选器](../../extensibility/internals/media/image-library-viewer-filter.png "图像库查看器筛选器")  
  
 搜索的现有清单中的图像名字对象时，我们建议你搜索和使用仅 Visual Studio 映像目录的名字对象、 其他有意可公开访问的名字对象或你自己的自定义名字对象。 如果使用非公共的名字对象，自定义 UI 可能已损坏或其映像后已经更改以意外方式或如果更改或更新这些非公共的名字对象和图像。  
  
 此外，搜索 guid 是可能的。 搜索此类型可用于筛选到一个单一的清单，列表中，或如果该清单的清单的单个小节包含多个 Guid。  
  
 ![图像库查看器筛选器 GUID](../../extensibility/internals/media/image-library-viewer-filter-guid.png "图像库查看器筛选器 GUID")  
  
 最后，按 ID 搜索也是可以实现。  
  
 ![图像库查看器筛选器 ID](../../extensibility/internals/media/image-library-viewer-filter-id.png "图像库查看器筛选器 ID")  
  
## <a name="notes"></a>说明  
  
- 默认情况下，该工具会在 Visual Studio 安装目录中存在多个映像清单中拉取。 仅具有公开使用名字对象的一种是**Microsoft.VisualStudio.ImageCatalog**清单。 GUID: ae27a6b0-e345-4288-96df-5eaf394ee369 (不要**不**重写自定义清单中的此 GUID) 类型：KnownMonikers  
  
- 该工具会尝试启动时加载它找到的所有映像清单，因此，可能需要几秒钟，要实际出现的应用程序。 它也可能会加载清单时是缓慢或无响应。  
  
## <a name="sample-output"></a>示例输出  
 此工具不会生成任何输出。
