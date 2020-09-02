---
title: 在联机 ClickOnce 应用程序中检索查询字符串信息
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, query strings
- query strings, retrieving information
ms.assetid: 48ce098a-a075-481b-a5f5-c8ba11f63120
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d0e177f1d41655ffa6fb6b6bbfa52cfc29d15fd6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85382180"
---
# <a name="how-to-retrieve-query-string-information-in-an-online-clickonce-application"></a>如何：在联机 ClickOnce 应用程序中检索查询字符串信息
*查询字符串* 是 URL 的一部分，它以问号 (?) 开头，并且以 *名称=值*的形式包含任意信息。 假设你有一个在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 上承载的名为 `WindowsApp1` 的 `servername`应用程序，并且要在该应用程序启动时传入变量 `username` 的值。 你的 URL 可能类似于下面这样：

 `http://servername/WindowsApp1.application?username=joeuser`

 以下两个过程演示如何使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序获取查询字符串信息。

> [!NOTE]
> 仅当使用 HTTP（而不是使用文件共享或本地文件系统）启动应用程序时，才能在查询字符串中传递信息。

 第一个过程演示 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序如何使用一小段代码在应用程序启动时读取这些值。

 下一个过程演示如何使用 MageUI.exe 配置 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，以便它可以接受查询字符串参数。 每次发布应用程序时都需要执行此操作。

> [!NOTE]
> 决定启用此功能之前，请参阅本主题后面的“安全性”一节。

 有关如何 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用 *Mage.exe* 或 *MageUI.exe*创建部署的信息，请参阅 [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。

> [!NOTE]
> 从 .NET Framework 3.5 SP1 开始，可以将命令行参数传递给脱机 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 如果要向应用程序提供参数，则可以将参数传入具有 .APPREF-MS 扩展名的快捷方式文件。

### <a name="to-obtain-query-string-information-from-a-clickonce-application"></a>从 ClickOnce 应用程序获取查询字符串信息

1. 将以下代码置于项目中。 为了使此代码正常运行，您必须对 system.web、system.web 和 System.object 都具有对 system.web 的引用以及对该函数的 add `using` 或 `Imports` 指令。

     [!code-csharp[ClickOnceQueryString#1](../deployment/codesnippet/CSharp/how-to-retrieve-query-string-information-in-an-online-clickonce-application_1.cs)]
     [!code-vb[ClickOnceQueryString#1](../deployment/codesnippet/VisualBasic/how-to-retrieve-query-string-information-in-an-online-clickonce-application_1.vb)]

2. 调用以前定义的函数以检索查询字符串参数的 <xref:System.Collections.DictionaryBase.Dictionary%2A> （按名称编制索引）。

### <a name="to-enable-query-string-passing-in-a-clickonce-application-with-mageuiexe"></a>使用 MageUI.exe 在 ClickOnce 应用程序中启用查询字符串传递

1. 打开 .NET 命令提示符并输入：

   ```cmd
   MageUI
   ```

2. 在“文件” **** 菜单中，选择“打开” ****，然后打开 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的部署清单（这是以 `.application` 扩展名结尾的文件）。

3. 在左侧导航窗口中选择“部署选项” **** 面板，然后选中“允许向应用程序传递 URL 参数” **** 复选框。

4. 在“文件” **** 菜单中选择“保存” ****。

> [!NOTE]
> 或者，可以在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]中启用查询字符串传递。 选中“允许向应用程序传递 URL 参数” **** 复选框（可以通过打开“项目属性” ****，选择“发布” **** 选项卡，单击“选项” **** 按钮，然后选择“清单” **** 来找到该复选框）。

## <a name="robust-programming"></a>可靠编程
 使用查询字符串参数时，必须仔细考虑如何安装和激活应用程序。 如果应用程序配置为从 Web 或网络共享安装在用户计算机上，则用户可能只会通过 URL 激活应用程序一次。 之后，用户通常会使用“开始” **** 菜单中的快捷方式激活应用程序。 因此，应用程序确保只会在其生存期中接收查询字符串参数一次。 如果你选择将这些参数存储在用户计算机上以供将来使用，则由你负责以安全稳妥的方式存储它们。

 如果应用程序仅处于联机状态，则它始终通过 URL 进行激活。 但是即使在这种情况下，应用程序也必须编写为可在查询字符串参数丢失或损坏的情况下正常运行。

## <a name="net-framework-security"></a>.NET Framework 安全性
 仅当你计划在使用包含任何恶意字符的输入之前清除它时，才允许向 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序传递 URL 参数。 例如，如果在针对数据库进行的 SQL 查询中未经筛选地使用嵌入有引号、斜杠或分号的字符串，则该字符串可能会执行任意数据操作。 有关查询字符串安全性的详细信息，请参阅[脚本入侵概述](https://msdn.microsoft.com/Library/772c7312-211a-4eb3-8d6e-eec0aa1dcc07)。

## <a name="see-also"></a>另请参阅
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
