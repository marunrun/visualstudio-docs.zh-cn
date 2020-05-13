---
title: 演练：使用C++创建 SDK |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65643e65490eacb79eea4d76aa49ff10d6cccf66
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697633"
---
# <a name="walkthrough-create-an-sdk-using-c"></a>演练：使用C++创建 SDK
本演练演示如何创建本机C++数学库 SDK，将 SDK 打包为可视化工作室扩展 （VSIX），然后使用它创建应用。 演练分为以下步骤：

- [创建本机和 Windows 运行时库](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)

- [创建本机MathVSIX扩展项目](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)

- [创建使用类库的示例应用](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)

## <a name="prerequisites"></a>先决条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[可视化工作室 SDK](../extensibility/visual-studio-sdk.md)。

## <a name="to-create-the-native-and-windows-runtime-libraries"></a><a name="createClassLibrary"></a>创建本机和 Windows 运行时库

1. 在菜单栏上，选择 **"文件** > **新项目** > **"。**

2. 在模板列表中，展开**VisualC++** > **Windows 通用**，然后选择**DLL（Windows 通用应用）** 模板。 在 **"名称"** 框中，`NativeMath`指定 ，然后选择 **"确定**"按钮。

3. 更新*本机 Math.h*以匹配以下代码。

     [!code-cpp[CreatingAnSDKUsingCpp#1](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_1.h)]

4. 更新*本机 Math.cpp*以匹配此代码：

     [!code-cpp[CreatingAnSDKUsingCpp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_2.cpp)]

5. 在**解决方案资源管理器中**，打开**解决方案"本机数学"** 的快捷菜单，然后选择"**添加新** > **项目**"。

6. 在模板列表中，展开**可视化C++，** 然后选择**Windows 运行时组件**模板。 在 **"名称"** 框中，`NativeMathWRT`指定 ，然后选择 **"确定**"按钮。

7. 更新*Class1.h*以匹配此代码：

     [!code-cpp[CreatingAnSDKUsingCpp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_3.h)]

8. 更新*Class1.cpp*以匹配此代码：

     [!code-cpp[CreatingAnSDKUsingCpp#4](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_4.cpp)]

9. 在菜单栏上，选择 **"生成** > **解决方案**"。

## <a name="to-create-the-nativemathvsix-extension-project"></a><a name="createVSIX"></a>创建本机MathVSIX扩展项目

1. 在**解决方案资源管理器中**，打开**解决方案"本机数学"** 的快捷菜单，然后选择"**添加新** > **项目**"。

2. 在模板列表中，展开**可视化 C#** > **可扩展性**，然后选择**VSIX 项目**。 在 **"名称"** 框中，指定**本机 MathVSIX，** 然后选择 **"确定**"按钮。

3. 在**解决方案资源管理器中**，打开**source.扩展.vsixmanifest 的**快捷菜单，然后选择 **"查看代码**"。

4. 使用以下 XML 替换现有 XML。

    [!code-xml[CreatingAnSDKUsingCpp#6](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_6.xml)]

5. 在**解决方案资源管理器**中，打开**NativeMathVSIX**项目的快捷菜单，然后选择"**Add** > **添加新项**"。

6. 在**可视化 C# 项**列表中，展开**数据**，然后选择**XML 文件**。 在 **"名称"** 框中，`SDKManifest.xml`指定 ，然后选择 **"确定**"按钮。

7. 使用此 XML 替换文件的内容：

     [!code-xml[CreatingAnSDKUsingCpp#5](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_5.xml)]

8. 在**解决方案资源管理器**中，在**本机MathVSIX**项目下，创建此文件夹结构：

    ```xml
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

9. 在**解决方案资源管理器**中，打开**解决方案"本机 Math"** 的快捷方式菜单，然后在**文件资源管理器中选择"打开文件夹**"。

10. 在**文件资源管理器**中，复制 *$SolutionRoot$$_NativeMath_NativeMath.h，* 然后在**解决方案资源管理器**中，在**本机MathVSIX**项目下，将其粘贴到 *$SolutionRoot$$_NativeMathVSIX_设计时间\通用配置\中性\\\包括*文件夹中。

     复制 *$SolutionRoot$$_调试\本机Math_NativeMath.lib*，然后将其粘贴到 *$SolutionRoot$_NativeMathVSIX_设计时间\调试\x86\\*文件夹中。

     复制 *$SolutionRoot$_Debug_NativeMath_NativeMath.dll*并将其粘贴到 *$SolutionRoot$_NativeMathVSIX_Redist_Debug_x86\\*文件夹中。

     复制 *$SolutionRoot$$_调试\本机 MathWRT_NativeMathWRT.dll 并将其*粘贴到 *$SolutionRoot$_NativeMathVSIX_Redist_Debug_x86*文件夹中。
     复制 *$SolutionRoot$$_调试\本机 MathWRT_NativeMathWRT.winmd，* 并将其粘贴到 *$SolutionRoot$_NativeMathVSIX_引用\通用配置\中性*文件夹中。

     复制 *$SolutionRoot$_Debug_NativeMathWRT_NativeMathWRT.pri*并将其粘贴到 *$SolutionRoot$_NativeMathVSIX_引用\通用配置\中性*文件夹中。

11. 在 *$SolutionRoot$$_NativeMathVSIX_DesignTime_Debug_x86\\*文件夹中，创建名为*NativeMathSDK.props*的文本文件，然后粘贴以下内容：

    [!code-xml[CreatingAnSDKUsingCpp#7](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_7.xml)]

12. 在菜单栏上，选择 **"查看** > **其他 Windows** > **属性"窗口**（键盘：选择**F4**键）。

13. 在**解决方案资源管理器**中，选择**本机MathWRT.winmd**文件。 在 **"属性"** 窗口中，将**生成操作**属性更改为**内容**，然后将**VSIX 中的"包括"** 属性更改为**True**。

     对**本机 Math.h**文件重复此过程。

     对**本机 MathWRT.pri**文件重复此过程。

     对**本机 Math.Lib**文件重复此过程。

     对**本机 MathSDK.props**文件重复此过程。

14. 在**解决方案资源管理器中**，选择**本机Math.h**文件。 在 **"属性"** 窗口中，将**VSIX 中的"包括"** 属性更改为**True**。

     对**本机 Math.dll**文件重复此过程。

     对**本机 MathWRT.dll**文件重复此过程。

     对**SDKManifest.xml**文件重复此过程。

15. 在菜单栏上，选择 **"生成** > **解决方案**"。

16. 在**解决方案资源管理器**中，打开**本机MathVSIX**项目的快捷菜单，然后在**文件资源管理器中选择"打开文件夹**"。

17. 在**文件资源管理器中**，导航到 *$SolutionRoot$$_NativeMathVSIX_bin_调试*文件夹，然后运行*本机MathVSIX.vsix*开始安装。

18. 选择 **"安装**"按钮，等待安装完成，然后打开 Visual Studio。

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a>创建使用类库的示例应用

1. 在菜单栏上，选择 **"文件** > **新项目** > **"。**

2. 在模板列表中，展开 **"视窗C++** > **Windows 通用**，然后选择**空白应用**。 在 **"名称"** 框中，指定**本机MathSDKSample，** 然后选择 **"确定**"按钮。

3. 在**解决方案资源管理器**中，打开**NativeMathSDKSample**项目的快捷菜单，然后选择 **"添加** > **参考**"。

4. 在"**添加引用"** 对话框中，在引用类型列表中，展开**通用 Windows，** 然后选择 **"扩展**"。 最后，选择**本机数学 SDK**复选框，然后选择 **"确定**"按钮。

5. 显示本机 MathSDK 采样的项目属性。

    添加引用时，应用了在*NativeMathSDK.props*中定义的属性。 您可以通过检查项目的**配置属性**的**VC# 目录**属性来验证已应用的属性。

6. 在**解决方案资源管理器中**，打开**MainPage.xaml**，然后使用以下 XAML 替换其内容：

    [!code-xml[CreatingAnSDKUsingCppDemoApp#1](../extensibility/codesnippet/Xaml/walkthrough-creating-an-sdk-using-cpp_8.xaml)]

7. 更新*主页.xaml.h*以匹配此代码：

    [!code-cpp[CreatingAnSDKUsingCppDemoApp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_9.h)]

8. 更新*MainPage.xaml.cpp*以匹配此代码：

     [!code-cpp[CreatingAnSDKUsingCppDemoApp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_10.cpp)]

9. 选择**F5**键来运行应用。

10. 在应用中，输入任意两个数字，选择一个操作，然后选择该**=** 按钮。

     将显示正确的结果。

    本演练演示如何创建和使用扩展 SDK 调用[!INCLUDE[wrt](../extensibility/includes/wrt_md.md)]到库和非[!INCLUDE[wrt](../extensibility/includes/wrt_md.md)]库中。

## <a name="next-steps"></a>后续步骤

## <a name="see-also"></a>请参阅
- [演练：使用 C# 或可视化基本功能创建 SDK](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)
