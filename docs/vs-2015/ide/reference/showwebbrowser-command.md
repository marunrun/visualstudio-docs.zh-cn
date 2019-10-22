---
title: ShowWebBrowser 命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- view.showwebbrowser
helpviewer_keywords:
- ShowWebBrowser command
- View.ShowWebBrowser command
ms.assetid: c6a4fbd6-8e9d-45cc-8b2f-93990d065e78
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1ecf86bdc7516f05935bd944f23633b3baad2c7c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663519"
---
# <a name="showwebbrowser-command"></a>ShowWebBrowser 命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在集成开发环境 (IDE) 中或 IDE 外部显示在 Web 浏览器窗口中指定的 URL。

## <a name="syntax"></a>语法

```
View.ShowWebBrowser URL [/new][/ext]
```

## <a name="arguments"></a>自变量
 `URL`（必需）。 网站的 URL（统一资源定位器）。

## <a name="switches"></a>开关
 /new 可选。 指定在 Web 浏览器的新实例中显示页。

 /ext（可选）。 指定在 IDE 外部的默认 Web 浏览器中显示页。

## <a name="remarks"></a>备注
 ShowWebBrowser 命令的别名是“导航”或“nav”    。

## <a name="example"></a>示例
 以下示例显示在 IDE 外部的 Web 浏览器中的 MSDN Online 主页。 如果 Web 浏览器的实例已打开，则使用它；否则启动一个新实例。

```
>View.ShowWebBrowser https://msdn.microsoft.com /ext
```

## <a name="see-also"></a>另请参阅
 [Visual studio](../../ide/reference/visual-studio-commands.md) "[命令" 窗口](../../ide/reference/command-window.md)中的["查找/命令" 框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
