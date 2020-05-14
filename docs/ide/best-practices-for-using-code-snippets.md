---
title: 有关使用代码段的最佳做法
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- code snippets, best practices
- code snippets, security
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 08add20b59e3e14897d1870aa45fd6cce8698d96
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75591705"
---
# <a name="best-practices-for-using-code-snippets"></a>有关使用代码片段的最佳做法

代码片段中的代码仅显示执行某些操作的最基本方法。 对于大多数应用程序，必须修改代码，使其适合应用程序。

## <a name="handling-exceptions"></a>处理异常

通常情况下，代码片段 Try…Catch 块可捕获和重新引发所有异常。 这可能并不适合你的项目。 对于每个异常，可通过几种方法进行响应。 相关示例请参阅[如何：使用 try/catch 处理异常 (C#)](/dotnet/csharp/programming-guide/exceptions/how-to-handle-an-exception-using-try-catch) 和 [Try...Catch...Finally 语句 (Visual Basic)](/dotnet/visual-basic/language-reference/statements/try-catch-finally-statement)。

## <a name="file-locations"></a>文件位置

改写文件位置以使其适合应用程序时，应考虑以下事项：

- 查找可访问的位置。 用户可能无权访问计算机的 Program Files 文件夹，因此可能无法存储包含应用程序文件的文件  。

- 查找安全位置。 将文件存储在根文件夹 (C: *) 中并不安全\\* 。 建议将应用程序数据存储在“应用程序数据”文件夹中  。 对于个人用户数据，应用程序可在“文档”文件夹中为每位用户创建一个文件  。

- 使用有效文件名。 可使用 <xref:System.Windows.Forms.OpenFileDialog> 和 <xref:System.Windows.Forms.SaveFileDialog> 控件降低使用无效文件名的可能性。 请注意，在用户选择文件和代码操作该文件的时间范围内，可能会删除该文件。 此外，用户可能没有写入该文件的权限。

## <a name="security"></a>安全

代码片段的安全程度取决于源代码中使用它的位置以及位于代码中后如何对其进行修改。 以下列表包含几个必须考虑的区域。

- 文件和数据库访问

- 代码访问安全性

- 保护资源（如事件日志、注册表）

- 存储机密

- 验证输入

- 将数据传递到脚本编写技术

有关详细信息，请参阅[保护应用程序](../ide/securing-applications.md)。

## <a name="downloaded-code-snippets"></a>下载的代码片段

由 Visual Studio 安装的 IntelliSense 代码片段就其本身而言并非安全隐患。 但它们会在应用程序中带来安全性风险。 应像任何其他下载内容一样，极其谨慎地对待从 Internet 下载的代码片段。

- 仅从信任的站点下载代码片段，并使用最新的防病毒软件。

- 在 Visual Studio 的记事本或 XML 编辑器中打开所有已下载的代码片段文件，并在安装前仔细检查。 查找以下问题：

  - 如果执行该代码片段，可能会对系统造成损坏。 在运行前请仔细阅读源代码。

  - 代码片段文件的 Help URL 块可以包含执行恶意脚本文件或显示攻击性网站的 URL。

  - 代码片段可能包含以无提示方式添加到项目的引用，并且这些引用可从系统的任何位置加载。 这些引用可能已从下载代码片段的位置下载到了计算机。 随后，代码片段可能会调用执行恶意代码的引用中的方法。 若要避免此类攻击，请检查代码片段文件的 Imports 和 References 块。

## <a name="see-also"></a>另请参阅

- [Visual Basic IntelliSense 代码片段](/dotnet/visual-basic/developing-apps/using-ide/intellisense-code-snippets)
- [保护应用程序](../ide/securing-applications.md)
- [代码片段](../ide/code-snippets.md)
