---
title: XAML 错误和警告
ms.date: 03/06/2018
ms.topic: conceptual
ms.assetid: 34eac8a0-7ec5-4c40-b97a-0126ed367931
author: karann-msft
ms.author: karann
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d3ae795b464d8a693371b1ebb9238a897debbf02
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62892611"
---
# <a name="xaml-errors-and-warnings"></a>XAML 错误和警告

创作 XAML 时，Visual Studio 会分析键入的代码。 检测到错误时，代码行上会出现波浪线。 光标悬停在波浪线上可获取错误或警告的详细信息。 对于某些错误和警告，将显示“快速操作”灯泡，使用 Ctrl+.  键盘快捷方式可问题修复选项。

## <a name="error-types"></a>错误类型

多个工具后台并行分析 XAML。 XAML 错误可基于检测到错误的工具分为以下三种类型：

|**检测到错误的工具**|**错误代码格式**|
| - |-----------------|
|XAML 语言服务（XAML 编辑器）|XLSxxxx|
|XAML 设计器|XDGxxxx|
|XAML 编辑并继续|XECxxxx|

> [!Note]
> 并非所有错误或警告都有相应的代码。 此类错误通常是 XAML 设计器错误。

## <a name="suppress-xaml-designer-errors"></a>取消显示 XAML 设计器错误

选择“工具”和“选项”，再选择“文本编辑器”和“XAML”>“其他”，即可打开“选项”对话框。

取消选中“显示 XAML 设计器检测到的错误”复选框。

![取消显示 XAML 设计器错误](../designers/media/suppress_xaml_designer_errors.png)
