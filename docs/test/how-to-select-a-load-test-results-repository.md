---
title: 如何：选择负载测试结果存储库
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.dialog.connectstringmissing
- vs.test.load.dialog.databaseconnectstring
helpviewer_keywords:
- load tests, results repository
- results, load test
- load test results, repository
- Load Test Results Repository
- SQL, Load Test Results Store
ms.assetid: fa0c4dd9-612f-4a57-b8eb-458f129d9cda
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b5b1b13ec6b81536a63a1732e7521dd1e64d007f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653476"
---
# <a name="how-to-select-a-load-test-results-repository"></a>如何：选择负载测试结果存储库

并不局限于使用本地结果存储区。 通常，负载测试是在一组远程代理计算机上运行。 多个代理和一个控制器一起可生成比任何单台计算机更多的模拟负载。 有关详细信息，请参阅[测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)。

代理或本地计算机生成的测试结果可保存到任何已创建负载测试结果存储区的 SQL 服务器中。 在任一情况下，都必须使用“管理测试控制器”窗口标识要存储负载测试结果的存储区  。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="identify-a-results-store-for-load-test-data"></a>标识负载测试数据的结果存储区

1. 在“解决方案资源管理器”中，打开负载测试文件  。

2. 从“负载测试”工具栏中，选择“管理测试控制器”   。 此时将显示“管理测试控制器”对话框  。 如果要远程使用代理，则必须选择一个控制器。

     ![负载测试结果存储区的连接属性](../test/media/loadtestconnectionproperties.png)负载测试结果存储区的连接属性

3. 在“负载测试测结果存储区”中单击“(…)”，以显示“连接属性”对话框    。

4. 在“服务器名称”中，键入在其中运行 `LoadTest` 脚本的服务器的名称  。

    > [!TIP]
    > 如果在本地计算机上将 SQL Express 用于负载测试存储，请输入 \<计算机名>\sqlexpress（例如，MyComputer\sqlexpress）  。

5. 在“登录到服务器”下，可以选择“使用 Windows 身份验证”   。 可以指定用户名和密码，但是如果要指定就必须选择“保存密码”选项  。

6. 在“连接到一个数据库”下，选择“选择或输入一个数据库名”   。 从下拉列表框中选择“LoadTest”  。

7. 选择 **“确定”** 。 可通过选择“测试连接”测试该连接  。

8. 在“管理测试控制器”对话框中，选择“关闭”   。

## <a name="see-also"></a>请参阅

- [管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)
- [测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)