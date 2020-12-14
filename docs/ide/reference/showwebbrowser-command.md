---
title: ShowWebBrowser 命令
description: 了解显示 Web 浏览器命令，以及它如何在 IDE 中或 IDE 外部的 Web 浏览器窗口中显示指定的 URL。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- view.showwebbrowser
helpviewer_keywords:
- ShowWebBrowser command
- View.ShowWebBrowser command
ms.assetid: c6a4fbd6-8e9d-45cc-8b2f-93990d065e78
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 026878bdc2158d803f191cf2d28c8eb52f0b6e09
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2020
ms.locfileid: "96616312"
---
# <a name="showwebbrowser-command"></a>ShowWebBrowser 命令

在集成开发环境 (IDE) 中或 IDE 外部显示在 Web 浏览器窗口中指定的 URL。

## <a name="syntax"></a>语法

```cmd
View.ShowWebBrowser URL [/new][/ext]
```

## <a name="arguments"></a>自变量
`URL`

必需。 网站的 URL（统一资源定位器）。

## <a name="switches"></a>交换机
/new

可选。 指定在 Web 浏览器的新实例中显示页。

/ext

可选。 指定在 IDE 外部的默认 Web 浏览器中显示页。

## <a name="remarks"></a>备注
ShowWebBrowser 命令的别名是“导航”或“nav”。

## <a name="example"></a>示例
以下示例显示在 IDE 外部的 Web 浏览器中的 Microsoft Docs 主页。 如果 Web 浏览器的实例已打开，则使用它；否则启动一个新实例。

```cmd
>View.ShowWebBrowser https://docs.microsoft.com /ext
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)