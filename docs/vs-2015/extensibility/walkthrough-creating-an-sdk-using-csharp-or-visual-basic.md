---
title: 演练：创建 SDK 使用C#或 Visual Basic |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 44b1083a9de4a5fe3e86ae37814f6df85f8c1e56
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435491"
---
# <a name="walkthrough-creating-an-sdk-using-c-or-visual-basic"></a>演练：使用 C# 或 Visual Basic 创建 SDK
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本演练中，将了解如何使用 Visual C# 创建一个简单的数学库 SDK，然后打包 SDK 作为 Visual Studio 扩展 (VSIX)。 将完成以下过程：  
  
- [若要创建 SimpleMath Windows 运行时组件](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)  
  
- [若要创建 SimpleMathVSIX 扩展项目](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)  
  
- [创建示例应用程序使用类库](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)  
  
## <a name="prerequisites"></a>系统必备  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。  
  
## <a name="createClassLibrary"></a> 若要创建 SimpleMath Windows 运行时组件  
  
1. 在菜单栏上依次选择**文件**，**新建**，**新项目**。  
  
2. 在模板列表中，展开**Visual C#** 或**Visual Basic**，选择**Windows 应用商店**节点，然后选择**Windows 运行时组件**模板。  
  
3. 在中**名称**框中，指定**SimpleMath**，然后选择**确定**按钮。  
  
4. 在中**解决方案资源管理器**，打开快捷菜单**SimpleMath**项目节点，然后选择**属性**。  
  
5. 重命名**Class1.cs**到**Arithmetic.cs**并更新它，以匹配下面的代码：  
  
     [!code-csharp[CreatingAnSDKUsingWinRT#3](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrt/cs/winrtmath/arithmetic.cs#3)]
     [!code-vb[CreatingAnSDKUsingWinRT#3](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrt/vb/winrtmath/arithmetic.vb#3)]  
  
6. 在中**解决方案资源管理器**，打开快捷菜单**解决方案 SimpleMath**节点，然后选择**Configuration Manager**。  
  
     **Configuration Manager**对话框随即打开。  
  
7. 在中**活动解决方案配置**列表中，选择**发行**。  
  
8. 在**配置**列中，确认**SimpleMath**行设置为**版本**，然后选择**关闭**按钮以接受更改。  
  
    > [!IMPORTANT]
    > SDK for SimpleMath 组件包括只有一个配置。 此配置中必须是发布版本，或使用该组件的应用程序不会通过认证[!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)]。  
  
9. 在中**解决方案资源管理器**，打开快捷菜单**SimpleMath**项目节点，然后选择**生成**。  
  
## <a name="createVSIX"></a> 若要创建 SimpleMathVSIX 扩展项目  
  
1. 上的快捷菜单**解决方案 SimpleMath**节点，选择**添加**，**新项目**。  
  
2. 在模板列表中，展开**Visual C#** 或**Visual Basic**，选择**扩展性**节点，然后选择**VSIX 项目**模板。  
  
3. 在中**名称**框中，指定**SimpleMathVSIX**，然后选择**确定**按钮。  
  
4. 在中**解决方案资源管理器**，选择**source.extension.vsixmanifest**项。  
  
5. 在菜单栏上，依次选择 **“视图”** 、 **“代码”** 。  
  
6. 现有的 XML 替换为以下 XML:  
  
     [!code-xml[CreatingAnSDKUsingWinRT#1](../../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_2.xml)]
  
7. 在中**解决方案资源管理器**，选择**SimpleMathVSIX**项目。  
  
8. 在菜单栏上依次选择**项目**，**添加新项**。  
  
9. 在列表中**常见项**，展开**数据**，然后选择**XML 文件**。  
  
10. 在中**名称**框中，指定`SDKManifest.xml`，然后选择**添加**按钮。  
  
11. 在中**解决方案资源管理器**，打开快捷菜单`SDKManifest.xml`，选择**属性**，然后将更改的值**包含在 VSIX**属性设置为 **，则返回 true**。  
  
12. 用下列 XML 替换该文件的内容：  
  
     [!code-xml[CreatingAnSDKUsingWinRT#1](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrt/cs/winrtmathvsix/sdkmanifest.xml#1)]
     [!code-xml[CreatingAnSDKUsingWinRT#1](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrt/vb/winrtmathvsix/sdkmanifest.xml#1)]  
  
13. 在中**解决方案资源管理器**，打开快捷菜单**SimpleMathVSIX**项目中，选择**添加**，然后选择**新文件夹**。  
  
14. 重命名该文件夹以`references`。  
  
15. 打开快捷菜单**引用**文件夹中，选择**添加**，然后选择**新文件夹**。  
  
16. 重命名文件夹的子`commonconfiguration`，创建的子文件夹中，并将命名的子文件夹`neutral`。  
  
17. 重复前面的四个步骤，这一次重命名的第一个文件夹到`redist`。  
  
     项目现在包含以下文件夹结构：  
  
    ```  
    references\commonconfiguration\neutral  
    redist\commonconfiguration\neutral  
    ```  
  
18. 在中**解决方案资源管理器**，打开快捷菜单**SimpleMath**项目，，然后选择**在文件资源管理器中打开文件夹**。  
  
19. 在中**文件资源管理器**，导航到 bin\Release 文件夹中，打开 SimpleMath.winmd 文件的快捷菜单，然后选择**副本**。  
  
20. 在中**解决方案资源管理器**，将该文件粘贴到 references\commonconfiguration\neutral 文件夹**SimpleMathVSIX**项目。  
  
21. 重复上一步，将 SimpleMath.pri 文件粘贴到 redist\commonconfiguration\neutral 文件夹**SimpleMathVSIX**项目。  
  
22. 在中**解决方案资源管理器**，选择**SimpleMath.winmd**。  
  
23. 在菜单栏上依次选择**视图**，**属性**(键盘：选择 F4 键）。  
  
24. 在**属性**窗口中，更改**生成操作**属性设置为**内容**，然后将更改**包含在 VSIX** 属性**True**。  
  
25. 在中**解决方案资源管理器**，重复此过程**SimpleMath.pri**。  
  
26. 在中**解决方案资源管理器**，选择**SimpleMathVSIX**项目。  
  
27. 在菜单栏上依次选择**构建**，**生成 SimpleMathVSIX**。  
  
28. 在中**解决方案资源管理器**，打开快捷菜单**SimpleMathVSIX**项目，，然后选择**在文件资源管理器中打开文件夹**。  
  
29. 在中**文件资源管理器**，导航到 \bin\Release 文件夹，然后运行 SimpleMathVSIX.vsix 进行安装。  
  
30. 选择**安装**按钮，等待安装完成，然后再重新启动 Visual Studio。  
  
## <a name="createSample"></a> 创建示例应用程序使用类库  
  
1. 在菜单栏上依次选择**文件**，**新建**，**新项目**。  
  
2. 在模板列表中，展开**Visual C#** 或**Visual Basic**，然后选择**Windows 应用商店**节点。  
  
3. 选择**空白应用**模板，将项目命名**ArithmeticUI**，然后选择**确定**按钮。  
  
4. 在中**解决方案资源管理器**，打开快捷菜单**ArithmeticUI**项目，，然后选择**添加**，**引用**。  
  
5. 在引用类型的列表中，展开**Windows**，然后选择**扩展**。  
  
6. 在细节窗格中，选择**简单数学 SDK**扩展。  
  
    有关 SDK 的其他信息将出现。 你可以选择**详细信息**链接以打开 http://www.msdn.microsoft.com，如在本演练前面在 SDKManifest.xml 文件中指定。  
  
7. 在中**引用管理器**对话框中，选择**简单数学 SDK**复选框，，然后选择**确定**按钮。  
  
8. 在菜单栏上依次选择**视图**，**对象浏览器**。  
  
9. 在中**浏览**列表中，选择**简单的数学运算**。  
  
     你现在可以浏览什么是 SDK 中。  
  
10. 在中**解决方案资源管理器**，打开 MainPage.xaml，并其内容替换为以下 XAML:  
  
     [!code-xml[CreatingAnSDKUsingWinRTDemoApp#1](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/cs/winrtmathtest/mainpage.xaml#1)]
     [!code-xml[CreatingAnSDKUsingWinRTDemoApp#1](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/vb/winrtmathtest/mainpage.xaml#1)]  
  
11. 更新 MainPage.xaml.cs 以匹配下面的代码：  
  
     [!code-csharp[CreatingAnSDKUsingWinRTDemoApp#2](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/cs/winrtmathtest/mainpage.xaml.cs#2)]
     [!code-vb[CreatingAnSDKUsingWinRTDemoApp#2](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/vb/winrtmathtest/mainpage.xaml.vb#2)]  
  
12. 选择 F5 键以运行该应用程序。  
  
13. 在应用中，输入任何两个数字，选择一个操作，然后选择 **=** 按钮。  
  
     将显示正确的结果。  
  
    已成功创建并使用扩展 SDK。  
  
## <a name="see-also"></a>请参阅  
 [演练：SDK 使用创建C++](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)   
 [演练：使用 JavaScript 创建 SDK](walkthrough-creating-an-sdk-using-javascript.md)   
 [获取软件开发工具包](../extensibility/creating-a-software-development-kit.md)
