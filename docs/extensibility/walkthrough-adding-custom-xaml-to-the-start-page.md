---
title: 演练：将自定义 XAML 添加到开始页 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom start page
- xaml start page
ms.assetid: 9af4d5f9-1cfc-4221-aea7-c8cd3f7571a6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 543faf9cf122e77cce6242f95008b777cd5666b2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322783"
---
# <a name="walkthrough-add-custom-xaml-to-the-start-page"></a>演练：将自定义 XAML 添加到起始页

本演练演示如何创建自定义 Visual Studio 起始页包含的 Web 浏览器。

## <a name="add-custom-xaml"></a>添加自定义 XAML

1. 按照中的说明创建起始页[创建自定义起始页](../extensibility/creating-a-custom-start-page.md)。

2. 在中*MainWindow.xaml*文件中，找到\<网格 > 部分。

3. 添加\<TabControl > 元素和一个\<TabItem > 内\<网格 > 元素，如下面的示例中所示。

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

4. 添加另一个\<TabItem >，使用\<按钮 > 打开一个新项目的元素：

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

## <a name="test-the-custom-start-page"></a>测试自定义起始页

1. 按 F5  。

     Visual Studio 的实验实例随即打开，并安装但未选择的自定义起始页。

2. 在 Visual Studio 的实验实例中，打开**工具/选项 / 环境**页。

3. 选择**启动**。 上**自定义起始页**列表中，选择你 *.xaml*文件，然后单击**确定**。

4. 在“视图”  菜单上，单击“起始页”  。

5. 单击**必应**选项卡。

     应看到的必应 web 页面。

6. 单击**MyButton**选项卡。

     应会看到**MyProject**按钮以打开**新项目**对话框。

7. 关闭实验实例。

若要将自定义起始页上，应用中**工具** > **选项** > **环境**，选择**启动**。 上**自定义起始页**列表中，选择你 *.xaml*文件，然后单击**确定**。

## <a name="next-steps"></a>后续步骤

Visual Studio 起始页现在包含一个 Web 浏览器选项卡和 MyButton 选项卡将显示一个选项卡。可以创建使用具有其他功能的自定义起始页*代码隐藏*模型中添加自定义.dll，如中所示[添加到启动页的用户控件](../extensibility/adding-user-control-to-the-start-page.md)。 通过发布到生成的.vsix 文件，可以与其他用户共享自定义起始页[Visual Studio Marketplace](https://marketplace.visualstudio.com/)网站，或到另一个网站或网络共享。 有关更多信息，请参见 [Deploying Custom Start Pages](../extensibility/deploying-custom-start-pages.md)。

## <a name="see-also"></a>请参阅

- [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)
- [WPF 容器控件](https://msdn.microsoft.com/library/a0177167-d7db-4205-9607-8ae316952566)