---
title: 演练：将自定义 XAML 添加到起始页 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- custom start page
- xaml start page
ms.assetid: 9af4d5f9-1cfc-4221-aea7-c8cd3f7571a6
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7b2de492bd1eddf4bf18e4824cdb64de4241fa5f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65674115"
---
# <a name="walkthrough-adding-custom-xaml-to-the-start-page"></a>演练：将自定义 XAML 添加到起始页
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何创建包含 Web 浏览器的自定义 Visual Studio 起始页。  
  
## <a name="adding-custom-xaml"></a>添加自定义 XAML  
  
1. 按照 [创建自定义起始页](../extensibility/creating-a-custom-start-page.md)中的说明创建起始页。  
  
2. 在 Mainwindow.xaml 文件中，找到 \<Grid> 部分。  
  
3. 在 \<TabControl> 元素内添加元素和 \<TabItem> \< Grid> ，如下面的示例中所示。  
  
    ```xml  
    <Grid>  
        <TabControl>  
            <TabItem Header="Bing" Height="Auto">  
                <Frame Source="http://www.bing.com" />  
            </TabItem>  
        </TabControl>  
    </Grid>  
    ```  
  
4. 添加第二个 \<TabItem> ，其中包含用于 \<Button> 打开新项目的元素：  
  
    ```xml  
    <Grid>  
        <TabControl>  
            <TabItem Header="MyButton" Height="Auto">  
                <Button Name="btnNewProj" Content="New Project"   
                    Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
                    CommandParameter="File.NewProject" >  
                </Button>  
            </TabItem>  
            <TabItem Header="Bing" Height="Auto">  
                <Frame Source="http://www.bing.com" />  
            </TabItem>  
        </TabControl>  
    </Grid>  
    ```  
  
## <a name="testing-the-custom-start-page"></a>测试自定义起始页  
  
1. 按 F5。  
  
     此时将打开 Visual Studio 的实验实例，其中安装了自定义起始页但未选中。  
  
2. 在 Visual Studio 的实验实例中，打开 **Tools/Options/环境** 页。  
  
3. 选择 " **启动**"。 在 " **自定义起始页** " 列表中，选择您的 .xaml 文件，然后单击 **"确定"**。  
  
4. 在“视图” **** 菜单上，单击“起始页” ****。  
  
5. 单击 " **必应** " 选项卡。  
  
     应会看到必应网页。  
  
6. 单击 " **mybutton.src** " 选项卡。  
  
     此时会显示一个 " **MyProject** " 按钮，该按钮将打开 " **新建项目** " 对话框。  
  
7. 关闭实验实例。  
  
## <a name="applying-the-custom-start-page"></a>应用自定义起始页  
  
#### <a name="to-test-the-custom-start-page"></a>测试自定义起始页  
  
1. 在 " **工具/选项/环境**" 中，选择 " **启动**"。 在 " **自定义起始页** " 列表中，选择您的 .xaml 文件，然后单击 **"确定"**。  
  
## <a name="next-steps"></a>后续步骤  
 Visual Studio 起始页现在包含一个选项卡，其中显示了 "Web 浏览器" 选项卡和 "Mybutton.src" 选项卡。通过使用 *代码隐藏* 模型添加自定义 .dll，可以创建具有其他功能的自定义起始页，如 [将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)中所示。 可以通过将生成的 .vsix 文件发布到 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 网站或其他网站或网络共享来与其他用户共享自定义起始页。 有关更多信息，请参见 [Deploying Custom Start Pages](../extensibility/deploying-custom-start-pages.md)。  
  
## <a name="see-also"></a>另请参阅  
 [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)   
 [WPF 容器控件](https://msdn.microsoft.com/a0177167-d7db-4205-9607-8ae316952566)
