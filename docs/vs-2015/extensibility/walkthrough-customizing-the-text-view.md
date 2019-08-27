---
title: 演练：自定义文本视图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - customizing the view
ms.assetid: 32d32ac8-22ff-4de7-af69-bd46ec4ad9bf
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e96bb177d3cfa90b2c80304eabfd93d1bea76d5b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202028"
---
# <a name="walkthrough-customizing-the-text-view"></a>演练：自定义文本视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过修改其编辑器格式映射中的下列属性的任何自定义文本视图：  
  
- 指示器边距  
  
- 插入脱字符号  
  
- 覆盖插入点  
  
- 所选的文本  
  
- 非活动选定的文本 （即，所选文本的已失去焦点）  
  
- 可见空白  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-mef-project"></a>创建 MEF 项目  
  
1. 创建一个 C# VSIX 项目。 (在**新的项目**对话框中，选择**Visual C# / 可扩展性**，然后**VSIX 项目**。)将解决方案命名为 `ViewPropertyTest`。  
  
2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3. 删除现有的类文件。  
  
## <a name="defining-the-content-type"></a>定义的内容类型  
  
1. 添加一个类文件并将其命名为 `ViewPropertyModifier`。  
  
2. 以下代码添加到`using`指令：  
  
    [!code-csharp[VSSDKViewPropertyTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#1)]
    [!code-vb[VSSDKViewPropertyTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#1)]  
  
3. 声明一个名为的类`TestViewCreationListener`，它继承自<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>。 导出此类具有以下属性：  
  
   - <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 若要指定的内容应用到此侦听器的类型。  
  
   - <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> 若要指定该侦听器的角色。  
  
     [!code-csharp[VSSDKViewPropertyTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#2)]
     [!code-vb[VSSDKViewPropertyTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#2)]  
  
4. 在此类中，导入<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>。  
  
    [!code-csharp[VSSDKViewPropertyTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#3)]
    [!code-vb[VSSDKViewPropertyTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#3)]  
  
## <a name="changing-the-view-properties"></a>更改视图属性  
  
1. 实现<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>方法，以便在视图打开时更改视图属性。 若要使此更改，首先找到<xref:System.Windows.ResourceDictionary>对应于你想要查找的视图的方面。 然后更改的资源字典中的相应属性和设置的属性。 对调用进行批处理<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.SetProperties%2A>方法通过调用<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.BeginBatchUpdate%2A>方法之前设置的属性，然后<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.EndBatchUpdate%2A>设置属性之后。  
  
     [!code-csharp[VSSDKViewPropertyTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#4)]
     [!code-vb[VSSDKViewPropertyTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#4)]  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
  
1. 生成解决方案。  
  
     在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
2. 创建一个文本文件并键入一些文本。  
  
    - 插入脱字符号应为洋红色和覆盖插入点应为青绿色。  
  
    - 指示器边距 （文本视图左侧） 应为浅绿色。  
  
3. 选择刚刚键入的文本。 所选文本的颜色应为浅粉色。  
  
4. 在选定文本，文本窗口外任意位置单击。 所选文本的颜色应为深粉红色。  
  
5. 打开可见空白。 (在**编辑**菜单，依次指向**高级**，然后单击**查看空白**)。 在文本中键入某些选项卡。 应显示红色箭头表示选项卡。  
  
## <a name="see-also"></a>请参阅  
 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
