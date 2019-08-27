---
title: 创建 Web 服务测试
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, creating Web service tests
- Web services [Visual Studio ALM], creating
- service tests, Web
ms.assetid: fbcd57ee-06ad-4260-8694-09f8e0f93e39
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3fd640a79a81e2306c8abd1c3c5279b1fc8f335f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62950132"
---
# <a name="how-to-create-a-web-service-test"></a>如何：创建 Web 服务测试

可以使用 Web 性能测试对 Web 服务进行测试。 使用“插入请求”和“插入 Web 服务请求”选项，可以在“Web 性能测试编辑器”中自定义各个请求以查找 Web 服务页。 通常，并不在 Web 应用程序中显示这些页。 因此，必须自定义请求才能访问这些页。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

以下过程使用商务初学者工具包中包含的 Web 服务。 可以从 [ASP.NET Commerce 初学者工具包](http://go.microsoft.com/fwlink/?LinkId=181469)进行下载。

**要求**

Visual Studio Enterprise

## <a name="to-test-a-web-service"></a>测试 Web 服务

1. 创建新的 Web 性能测试。 浏览器打开后，立刻选择“停止”。

2. 在“Web 性能测试编辑器”中右击“Web 性能测试”，然后选择“添加 Web 服务请求”。

3. 在新请求的“Url”属性中，键入 Web 服务的名称，如 http://localhost/storecsvs/InstantOrder.asmx。

4. 打开单独的浏览器会话，在“地址”工具栏中键入 .asmx 页的 URL。 选择要用来测试和检查 SOAP 消息的方法。 该方法包含 `SOAPAction`。

5. 在“Web 性能测试编辑器”中，右击请求并选择“添加标题”，以添加新标题。 在“名称”属性中键入 `SOAPAction`。 在“值”属性中，键入你在 `SOAPAction` 中看到的值，如 `"http://tempuri.org/CheckStatus"`。

6. 在编辑器中展开 URL 节点，选择“字符串正文”节点并在“内容类型”属性中输入 `text/xml` 的值。

7. 返回到步骤 4 中的浏览器，从 Web 服务描述页中选择 SOAP 请求的 XML 部分并将它复制到剪贴板中。

8. XML 内容类似下面的示例：

     ```xml
     <?xml version="1.0" encoding="utf-8"?>
     <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
     <soap:Body>
       <CheckStatus xmlns="http://tempuri.org/">
         <userName>string</userName>
         <password>string</password>
         <orderID>int</orderID>
       </CheckStatus>
     </soap:Body>
     </soap:Envelope>
     ```

9. 返回到“Web 性能测试编辑器”，然后选择“字符串正文”属性中的省略号“(…)”。 将剪贴板中的内容粘贴到该属性中。

10. 为使测试通过，必须用有效值替换 XML 中的所有占位符值。 在前面的示例中，将替换两个 `string` 实例和一个 `int`。 只有注册用户发出请求时才能完成此 Web 服务操作。

11. 右击 Web 服务请求并选择“添加 URL QueryString 参数”。

12. 为查询字符串参数赋予一个名称和值。 在前面的示例中，名称为 `op`，值为 `CheckStatus`。 这标识要执行的 Web 服务操作。

    > [!NOTE]
    > 通过使用 `{{DataSourceName.TableName.ColumnName}}` 语法，可以在 SOAP 体中使用数据绑定，从而用数据绑定值替换所有占位符值。

13. 运行测试。 在“Web 性能测试结果查看器”的顶部窗格中，选择 Web 服务请求。 在下窗格中，选择“Web 浏览器”选项卡。此时将显示 Web 服务返回的 XML 以及任何操作的结果。

## <a name="see-also"></a>请参阅

- [为负载测试创建自定义代码和插件](../test/create-custom-code-and-plug-ins-for-load-tests.md)