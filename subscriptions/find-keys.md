---
title: 在 Visual Studio 订阅中查找和声明产品密钥 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 03/09/2020
ms.topic: conceptual
description: 了解如何在 Visual Studio 订阅中查找、声明和导出产品密钥
ms.openlocfilehash: 984a89f5085867ea7b23735d05d0e22ef51dcfdb
ms.sourcegitcommit: f8e3715c64255b476520bfa9267ceaf766bde3b0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "78937497"
---
# <a name="finding-and-claiming-product-keys-in-visual-studio-subscriptions"></a>在 Visual Studio 订阅中查找和声明产品密钥
本文介绍如何从 https://my.visualstudio.com/productkeys 中查找、声明和导出产品密钥。  有关使用密钥激活产品、密钥的零售和批量许可版本以及每日产品密钥索取上限的详细信息，请访问[产品密钥概述](product-keys.md)。

## <a name="locating-and-claiming-product-keys"></a>查找并索取产品密钥
必须登录你的 Visual Studio 订阅才能查看产品密钥。 可在如下所示的“[下载](https://my.visualstudio.com/downloads)”页中，选择某一特定产品的蓝色“获取密钥”链接来查找单个产品密钥。   所有密钥都可在“[产品密钥](https://my.visualstudio.com/productkeys?wt.mc_id=o~msft~docs)”页查找到。 如果一个产品有多个密钥，会在下载项的“注释”列中显示注释，帮助你确定应使用哪个密钥。
> [!div class="mx-imgBorder"]
> ![从“下载”页获取密钥](_img/product-keys/download-get-key.png)

某些产品将其多个版本捆绑到单次下载中。 在这种情况下，输入的产品密钥决定安装的产品版本。
某些密钥会自动提供，例如“静态”密钥，同一个密钥可以根据需要使用无数次，因为不需要激活。 其他密钥必须通过选择该产品的“获取密钥”链接来索取。 

根据具体的产品，有多种密钥类型可供选择。

### <a name="product-key-types"></a>产品密钥类型

|    键类型           |    描述                                                                                                                                                                                                           |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    不适用                    |    安装此产品不需要密钥。                                                       |
|    零售                     |    零售密钥允许多次激活，适用于产品的零售版本。 在许多情况下，每个密钥允许激活 10 次，不过在同一台计算机中通常允许激活更多次。                                                       |
|    多次激活        |    多次激活密钥 (MAK) 允许使用同一密钥多次安装某产品。 MAK 通常适用于批量许可版本的产品。 通常情况下，一次订阅仅提供一个 MAK 密钥。    |
|    静态激活密钥    |    静态激活密钥提供给不需要激活的产品。 它们可在无限次安装中使用。                                                                                                                  |
|    自定义密钥                 |    自定义密钥提供特殊操作或信息来激活或安装产品。                                                                                                                                                                |
|    VA 1.0                     |    这些是多次激活密钥，与 MAK 类似。                                                                                                                                                                                                 |
|    OEM 密钥                    |    这些是允许多次激活的原始设备制造商密钥。                                                                                                                                                                       |
|    DreamSpark 零售密钥    |    这些是 DreamSpark 的零售密钥，允许一次激活。 DreamSpark 零售密钥按批次签发，主要面向学生消费。                                                                                     |
|    DreamSpark 实验室密钥         |    这些是 DreamSpark 计划的实验室用途的密钥，允许多次激活。 DreamSpark 实验室密钥供高校计算机实验室方案使用。                                                                                       |
|    DreamSpark MAK 密钥         |    这些是面向 DreamSpark 计划消费者的 MAK 密钥。                                                                                                                                                                                                  |
|

可从产品的下载页索取密钥，或者在“[产品密钥](https://my.visualstudio.com/productkeys)”页上搜索所需的密钥。

### <a name="claiming-product-keys"></a>索取产品密钥
只有拥有活动订阅的订阅者才可下载产品和索取产品密钥。  当订阅处于活动状态时，可从“[产品密钥](https://my.visualstudio.com/productkeys)”页导出索取的密钥。

索取产品密钥：
1. 登录到你的 Visual Studio 订阅。  必须登录才能下载产品或索取产品密码。
2. 单击“[产品密钥](https://my.visualstudio.com/productkeys?wt.mc_id=o~msft~docs)”选项卡。
3. 产品密钥根据产品名称按字母顺序列出。  可以向下滚动到所需产品的名称，也可以使用页面顶部的搜索栏进行搜索。
> [!div class="mx-imgBorder"]
> ![搜索产品密钥](_img/product-keys/search-keys.png)
   
在此示例中，我们使用了搜索栏查找 Visual Studio Enterprise 2019 的产品密钥。
正如你所见，这里列出了几个版本。  已为 Visual Studio Enterprise 2019 版本 16.0 和 16.1 各声明了一个密钥。  对于这两个版本，仍然可以使用不同类型的附加密钥。 注意，你可以在“注释”列记录有关已索取的密钥的简短说明。   可以结合“已索取”列中的日期，使用它来跟踪索取的密钥。   例如，可以在使用密钥激活产品的安装时进行记录。

### <a name="exporting-your-claimed-keys"></a>导出已索取的密钥
可以导出所有已索取的密钥以及众多自动标记为“已索取”的静态密钥和其他密钥的列表。

> [!IMPORTANT]
> 如果订阅到期，则无法索取新的密钥或导出已索取的密钥。

若要导出密钥，只需单击“产品密钥”页最右侧的“导出所有密钥”链接  。  此时将创建名为 KeysExport.xml 的 .xml 文件，可选择打开或保存该文件。  你需要使用能够处理 .xml 文件的应用程序来打开此文件。  例如，可以将该文件作为 Excel 中的只读工作簿打开。

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps 文档](https://docs.microsoft.com/azure/devops/)
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>后续步骤
当你准备好下载软件并使用密钥时，请访问 https://my.visualstudio.com/downloads 。  有关下载软件的详细信息，请参阅[下载概述](download-software.md)。