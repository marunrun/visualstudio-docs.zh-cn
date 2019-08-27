---
title: 演练：创建 SDK 使用C++|Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
caps.latest.revision: 33
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1312d61b2d287a5dd8cb757b73e818a9e9cb2241
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202078"
---
# <a name="walkthrough-creating-an-sdk-using-c"></a>演练：使用 C++ 创建 SDK
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何创建一个本机C++数学库 SDK，打包 SDK 作为 Visual Studio 扩展 (VSIX)，并使用它创建的应用程序。 本演练分为以下步骤：  
  
- [若要创建的本机和 Windows 运行时库](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)  
  
- [若要创建 NativeMathVSIX 扩展项目](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)  
  
- [创建示例应用程序使用类库](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)  
  
## <a name="prerequisites"></a>系统必备  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。  
  
## <a name="createClassLibrary"></a> 若要创建的本机和 Windows 运行时库  
  
1. 在菜单栏上，依次选择“文件”  、“新建”  、“项目”  。  
  
2. 在模板列表中，展开**可视化C++** ， **Windows 应用商店**，然后选择**DLL （Windows 应用商店应用）** 模板。 在中**名称**框中，指定`NativeMath`，然后选择**确定**按钮。  
  
3. 更新 NativeMath.h 以匹配下面的代码。  
  
     [!code-cpp[CreatingAnSDKUsingCpp#1](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.h#1)]  
  
4. 更新 NativeMath.cpp 以匹配此代码：  
  
     [!code-cpp[CreatingAnSDKUsingCpp#2](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.cpp#2)]  
  
5. 在**解决方案资源管理器**，打开快捷菜单**解决方案 NativeMath'** ，然后选择**添加**，**新项目**。  
  
6. 在模板列表中，展开**可视化C++** ，然后选择**Windows 运行时组件**模板。 在中**名称**框中，指定`NativeMathWRT`，然后选择**确定**按钮。  
  
7. 若要与此代码相匹配的更新 class1.h 中：  
  
     [!code-cpp[CreatingAnSDKUsingCpp#3](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.h#3)]  
  
8. 更新 Class1.cpp 以匹配此代码：  
  
     [!code-cpp[CreatingAnSDKUsingCpp#4](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.cpp#4)]  
  
9. 在菜单栏上，依次选择 **“生成”** 、 **“生成解决方案”** 。  
  
## <a name="createVSIX"></a> 若要创建 NativeMathVSIX 扩展项目  
  
1. 在**解决方案资源管理器**，打开快捷菜单**解决方案 NativeMath'** ，然后选择**添加**，**新项目**。  
  
2. 在模板列表中，展开**Visual C#** ，**扩展性**，然后选择**VSIX 包**。 在中**名称**框中，指定**NativeMathVSIX**，然后选择**确定**按钮。  
  
3. VSIX 清单设计器出现时，请将其关闭。  
  
4. 在中**解决方案资源管理器**，打开快捷菜单**source.extension.vsixmanifest**，然后选择**查看代码**。  
  
5. 使用以下 XML 替换现有的 XML。  
  
    [!code-xml[CreatingAnSDKUsingCpp#6](../../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_6.xml)]
  
6. 在中**解决方案资源管理器**，打开快捷菜单**NativeMathVSIX**项目，，然后选择**添加**，**新项**。  
  
7. 在列表中**Visual C# 项**，展开**数据**，然后选择**XML 文件**。 在中**名称**框中，指定`SDKManifest.xml`，然后选择**确定**按钮。  
  
8. 使用此 XML 文件的内容替换为：  
  
     [!code-xml[CreatingAnSDKUsingCpp#5](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathvsix/sdkmanifest.xml#5)]  
  
9. 在中**解决方案资源管理器**，在**NativeMathVSIX**项目中，创建此文件夹结构：  
  
    ```  
  
    \DesignTime  
          \CommonConfiguration  
                \Neutral  
                      \Include  
          \Debug  
                \x86  
    \Redist  
          \Debug  
                \x86  
    \References  
          \CommonConfiguration  
                \Neutral  
    ```  
  
10. 在中**解决方案资源管理器**，打开快捷菜单**解决方案 NativeMath'** ，然后选择**在文件资源管理器中打开文件夹**。  
  
11. 在中**文件资源管理器**，复制 \NativeMath\NativeMath.h，然后在**解决方案资源管理器**，在**NativeMathVSIX**项目中，将其粘贴在 \DesignTime\CommonConfiguration\Neutral\Include\ 文件夹。  
  
     复制 \Debug\NativeMath\NativeMath.lib，并将其粘贴 \DesignTime\Debug\x86\ 文件夹中。  
  
     复制 \Debug\NativeMath\NativeMath.dll 并将其粘贴在 \Redist\Debug\x86\ 文件夹中。  
  
     复制 DebugNativeMathWRTNativeMathWRT.dll 并将其粘贴在 RedistDebugx86 文件夹中。  
  
     复制 DebugNativeMathWRTNativeMathWRT.winmd 并将其粘贴在 ReferencesCommonConfigurationNeutral 文件夹中。  
  
     复制 DebugNativeMathWRTNativeMathWRT.pri 并将其粘贴在 ReferencesCommonConfigurationNeutral 文件夹中。  
  
12. \DesignTime\Debug\x86\ 文件夹中创建名为 NativeMathSDK.props，一个文本文件，然后在其中粘贴以下内容：  
  
    [!code-xml[CreatingAnSDKUsingCpp#7](../../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_7.xml)]  
  
13. 在菜单栏上依次选择**视图**，**其他 Windows**，**属性窗口**(键盘：选择 F4 键）。  
  
14. 在中**解决方案资源管理器**，选择**NativeMathWRT.winmd**文件。 在**属性**窗口中，更改**生成操作**属性设置为**内容**，然后将更改**包含在 VSIX** 属性**True**。  
  
     重复此过程**SimpleMath.pri**文件。  
  
     重复此过程**NativeMath.Lib**文件。  
  
     重复此过程**NativeMathSDK.props**文件。  
  
15. 在中**解决方案资源管理器**，选择**NativeMath.h**文件。 在中**属性**窗口中，更改**包含在 VSIX**属性设置为**True**。  
  
     重复此过程**NativeMath.dll**文件。  
  
     重复此过程**NativeMathWRT.dll**文件。  
  
     重复此过程**SDKManifest.xml**文件。  
  
16. 在菜单栏上，依次选择 **“生成”** 、 **“生成解决方案”** 。  
  
17. 在中**解决方案资源管理器**，打开快捷菜单**NativeMathVSIX**项目，，然后选择**在文件资源管理器中打开文件夹**。  
  
18. 在中**文件资源管理器**，导航到 \bin\Debug\ 文件夹，然后运行 NativeMathVSIX.vsix 以开始安装。  
  
19. 选择**安装**按钮，等待安装完成，然后再重新启动 Visual Studio。  
  
## <a name="createSample"></a> 创建示例应用程序使用类库  
  
1. 在菜单栏上，依次选择“文件”  、“新建”  、“项目”  。  
  
2. 在模板列表中，展开**可视化C++** ， **Windows 应用商店**，然后选择**空白应用**。 在中**名称**框中，指定**NativeMathSDKSample**，然后选择**确定**按钮。  
  
3. 在中**解决方案资源管理器**，打开快捷菜单**NativeMathSDKSample**项目，，然后选择**添加**，**引用**。  
  
4. 上**常见属性**，**框架和引用**属性页上，在列表中的引用类型，展开**Windows**，然后选择**扩展**. 在细节窗格中，选择**原生数学 SDK**扩展，然后选择**添加新引用**按钮。  
  
5. 在中**添加引用**对话框中，选择**本机数学 SDK**复选框，，然后选择**确定**按钮。  
  
6. 为 NativeMathSDKSample 显示项目属性。  
  
    添加引用时，已应用 NativeMathSDK.props 中定义的属性。 可以通过检查来验证这**VC + + 目录**项目的属性**配置属性**。  
  
7. 在中**解决方案资源管理器**，打开 MainPage.xaml，并使用以下 XAML 以将其内容为：  
  
    [!code-xml[CreatingAnSDKUsingCppDemoApp#1](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml#1)]  
  
8. 更新 Mainpage.xaml.h 中以匹配此代码：  
  
    [!code-cpp[CreatingAnSDKUsingCppDemoApp#2](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.h#2)]  
  
9. 更新 mainpage.xaml.cpp 中，以匹配此代码：  
  
     [!code-cpp[CreatingAnSDKUsingCppDemoApp#3](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.cpp#3)]  
  
10. 选择 F5 键以运行该应用程序。  
  
11. 在应用中，输入任何两个数字，选择一个操作，然后选择 **=** 按钮。  
  
     将显示正确的结果。  
  
    本演练演示了如何创建和使用扩展 SDK 来调入[!INCLUDE[wrt](../includes/wrt-md.md)]库和非[!INCLUDE[wrt](../includes/wrt-md.md)]库。  
  
## <a name="next-steps"></a>后续步骤  
  
## <a name="see-also"></a>请参阅  
 [演练：创建 SDK 使用C#或 Visual Basic](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)   
 [获取软件开发工具包](../extensibility/creating-a-software-development-kit.md)
