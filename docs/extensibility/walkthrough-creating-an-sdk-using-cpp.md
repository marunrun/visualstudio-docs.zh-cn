---
title: 演练：创建 SDK 使用C++|Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a60194c6512b67e1e3e90389b0221b6cdb8a5226
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312686"
---
# <a name="walkthrough-create-an-sdk-using-c"></a>演练：使用 SDK 创建C++
本演练演示如何创建一个本机C++数学库 SDK，打包 SDK 作为 Visual Studio 扩展 (VSIX)，并使用它创建的应用程序。 本演练分为以下步骤：

- [若要创建的本机和 Windows 运行时库](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)

- [若要创建 NativeMathVSIX 扩展项目](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)

- [创建示例应用程序使用类库](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)

## <a name="prerequisites"></a>系统必备
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="createClassLibrary"></a> 若要创建的本机和 Windows 运行时库

1. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。

2. 在模板列表中，展开**可视化C++**   >  **Windows Universal**，然后选择**DLL （Windows 通用应用）** 模板。 在中**名称**框中，指定`NativeMath`，然后选择**确定**按钮。

3. 更新*NativeMath.h*以匹配下面的代码。

     [!code-cpp[CreatingAnSDKUsingCpp#1](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_1.h)]

4. 更新*NativeMath.cpp*以匹配此代码：

     [!code-cpp[CreatingAnSDKUsingCpp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_2.cpp)]

5. 在**解决方案资源管理器**，打开快捷菜单**解决方案 NativeMath'** ，然后选择**添加** > **新项目**.

6. 在模板列表中，展开**可视化C++** ，然后选择**Windows 运行时组件**模板。 在中**名称**框中，指定`NativeMathWRT`，然后选择**确定**按钮。

7. 更新*Class1.h*以匹配此代码：

     [!code-cpp[CreatingAnSDKUsingCpp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_3.h)]

8. 更新*Class1.cpp*以匹配此代码：

     [!code-cpp[CreatingAnSDKUsingCpp#4](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_4.cpp)]

9. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

## <a name="createVSIX"></a> 若要创建 NativeMathVSIX 扩展项目

1. 在**解决方案资源管理器**，打开快捷菜单**解决方案 NativeMath'** ，然后选择**添加** > **新项目**.

2. 在模板列表中，展开**Visual C#**  > **扩展性**，然后选择**VSIX 项目**。 在中**名称**框中，指定**NativeMathVSIX**，然后选择**确定**按钮。

3. 在中**解决方案资源管理器**，打开快捷菜单**source.extension.vsixmanifest**，然后选择**查看代码**。

4. 使用以下 XML 替换现有的 XML。

    [!code-xml[CreatingAnSDKUsingCpp#6](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_6.xml)]

5. 在中**解决方案资源管理器**，打开快捷菜单**NativeMathVSIX**项目，，然后选择**添加** > **新项**.

6. 在列表中**Visual C# 项**，展开**数据**，然后选择**XML 文件**。 在中**名称**框中，指定`SDKManifest.xml`，然后选择**确定**按钮。

7. 使用此 XML 文件的内容替换为：

     [!code-xml[CreatingAnSDKUsingCpp#5](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_5.xml)]

8. 在中**解决方案资源管理器**下**NativeMathVSIX**项目中，创建此文件夹结构：

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

9. 在中**解决方案资源管理器**，打开快捷菜单**解决方案 NativeMath'** ，然后选择**在文件资源管理器中打开文件夹**。

10. 在中**文件资源管理器**，复制 *$SolutionRoot$\NativeMath\NativeMath.h*，然后在**解决方案资源管理器**下**NativeMathVSIX**项目中，将其粘贴 *$SolutionRoot$ \NativeMathVSIX\DesignTime\CommonConfiguration\Neutral\Include\\* 文件夹。

     复制 *$SolutionRoot$\Debug\NativeMath\NativeMath.lib*，然后将其在粘贴 *$SolutionRoot$ \NativeMathVSIX\DesignTime\Debug\x86\\* 文件夹。

     复制 *$SolutionRoot$\Debug\NativeMath\NativeMath.dll*并将其粘贴 *$SolutionRoot$ \NativeMathVSIX\Redist\Debug\x86\\* 文件夹。

     复制 *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.dll*并将其粘贴 *$SolutionRoot$ \NativeMathVSIX\Redist\Debug\x86*文件夹。
     复制 *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.winmd*并将其粘贴 *$SolutionRoot$ \NativeMathVSIX\References\CommonConfiguration\Neutral*文件夹。

     复制 *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.pri*并将其粘贴 *$SolutionRoot$ \NativeMathVSIX\References\CommonConfiguration\Neutral*文件夹。

11. 在中 *$SolutionRoot$ \NativeMathVSIX\DesignTime\Debug\x86\\* 文件夹中，创建名为的文本文件*NativeMathSDK.props*，然后将在其中粘贴以下内容：

    [!code-xml[CreatingAnSDKUsingCpp#7](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_7.xml)]

12. 在菜单栏上依次选择**视图** > **其他 Windows** > **属性窗口**(键盘：选择**F4**密钥)。

13. 在中**解决方案资源管理器**，选择**NativeMathWRT.winmd**文件。 在**属性**窗口中，更改**生成操作**属性设置为**内容**，然后将更改**包含在 VSIX** 属性**True**。

     重复此过程**NativeMath.h**文件。

     重复此过程**NativeMathWRT.pri**文件。

     重复此过程**NativeMath.Lib**文件。

     重复此过程**NativeMathSDK.props**文件。

14. 在中**解决方案资源管理器**，选择**NativeMath.h**文件。 在中**属性**窗口中，更改**包含在 VSIX**属性设置为**True**。

     重复此过程**NativeMath.dll**文件。

     重复此过程**NativeMathWRT.dll**文件。

     重复此过程**SDKManifest.xml**文件。

15. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

16. 在中**解决方案资源管理器**，打开快捷菜单**NativeMathVSIX**项目，，然后选择**在文件资源管理器中打开文件夹**。

17. 在中**文件资源管理器**，导航到 *$SolutionRoot$ \NativeMathVSIX\bin\Debug*文件夹，然后运行*NativeMathVSIX.vsix*以开始安装。

18. 选择**安装**按钮，等待安装完成，并打开 Visual Studio。

## <a name="createSample"></a> 创建示例应用程序使用类库

1. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。

2. 在模板列表中，展开**可视化C++**   >  **Windows Universal** ，然后选择**空白应用**。 在中**名称**框中，指定**NativeMathSDKSample**，然后选择**确定**按钮。

3. 在中**解决方案资源管理器**，打开快捷菜单**NativeMathSDKSample**项目，，然后选择**添加** > **引用**.

4. 在中**添加引用**对话框中，引用类型的列表中展开**通用 Windows**，然后选择**扩展**。 最后，选择**原生数学 SDK**复选框，，然后选择**确定**按钮。

5. 为 NativeMathSDKSample 显示项目属性。

    在中定义的属性*NativeMathSDK.props*添加引用时应用。 你可以验证已通过检查应用的属性**VC + + 目录**项目的属性**配置属性**。

6. 在中**解决方案资源管理器**，打开**MainPage.xaml**，然后使用以下 XAML 将其内容为：

    [!code-xml[CreatingAnSDKUsingCppDemoApp#1](../extensibility/codesnippet/Xaml/walkthrough-creating-an-sdk-using-cpp_8.xaml)]

7. 更新*Mainpage.xaml.h*以匹配此代码：

    [!code-cpp[CreatingAnSDKUsingCppDemoApp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_9.h)]

8. 更新*mainpage.xaml.cpp 中*以匹配此代码：

     [!code-cpp[CreatingAnSDKUsingCppDemoApp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_10.cpp)]

9. 选择**F5**键运行应用程序。

10. 在应用中，输入任何两个数字，选择一个操作，然后选择 **=** 按钮。

     将显示正确的结果。

    本演练演示了如何创建和使用扩展 SDK 来调入[!INCLUDE[wrt](../extensibility/includes/wrt_md.md)]库和非[!INCLUDE[wrt](../extensibility/includes/wrt_md.md)]库。

## <a name="next-steps"></a>后续步骤

## <a name="see-also"></a>请参阅
- [演练：创建 SDK 使用C#或 Visual Basic](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)
