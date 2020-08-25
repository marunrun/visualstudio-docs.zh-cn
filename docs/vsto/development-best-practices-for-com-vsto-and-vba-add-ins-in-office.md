---
title: 开发最佳实践： COM、VSTO、Office 中 & VBA 外接程序
ms.date: 07/25/2017
ms.topic: conceptual
dev_langs:
- ''
helpviewer_keywords:
- ''
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d5dd8864484e2b41a1146f1da495251663afdb6a
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801498"
---
# <a name="development-best-practices-for-com-vsto-and-vba-add-ins-in-office"></a>Office 中 COM、VSTO 和 VBA 外接程序的开发最佳做法
  如果要开发适用于 Office 的 COM、VSTO 或 VBA 外接程序，请遵循本文中所述的开发最佳实践。   这有助于确保：

- 不同版本和 Office 部署之间的外接程序的兼容性。
- 降低了用户和 IT 管理员的加载项部署复杂性。
- 外接程序的意外安装或运行时失败不会发生。

>注意：不支持使用 [桌面桥](/windows/uwp/porting/desktop-to-uwp-root) 为 Windows 应用商店准备 COM、VSTO 或 VBA 外接程序。 无法在 Windows 应用商店或 Office 应用商店中分发 COM、VSTO 和 VBA 外接程序。

## <a name="do-not-check-for-office-during-installation"></a>安装期间不检查 Office
 建议你不要在外接程序安装过程中让你的加载项检测是否安装了 Office。 如果未安装 Office，则可以安装外接程序，并且用户在安装 Office 后可以访问它。

## <a name="use-embedded-interop-types-nopia"></a>使用嵌入的互操作类型 (NoPIA) 
如果你的解决方案使用 .NET 4.0 或更高版本，请使用嵌入的互操作类型 (NoPIA) 而不是依赖于 Office 主互操作程序集 (PIA) 可再发行组件。 使用类型嵌入可降低解决方案的安装大小，并可确保将来的兼容性。 Office 2010 是交付 PIA 可再发行组件的最新版本的 Office。 有关详细信息，请参阅 [演练：嵌入类型信息 Microsoft Office 程序集](https://msdn.microsoft.com/library/ee317478.aspx) 和 [类型等效性和嵌入的互操作类型](/windows/uwp/porting/desktop-to-uwp-root)。

如果你的解决方案使用的是早期版本的 .NET，我们建议你将解决方案更新为使用 .NET 4.0 或更高版本。 使用 .NET 4.0 或更高版本可在较新版本的 Windows 上减少运行时必备组件。

## <a name="avoid-depending-on-specific-office-versions"></a>避免根据特定 Office 版本
如果你的解决方案使用的功能只能在新版 Office 中使用，请验证该功能是否存在 (如果可能，请在运行时) 功能级别 (例如，使用异常处理或检查版本) 。 使用对象模型中支持的 Api （如 [Application. Version 属性](<xref:Microsoft.Office.Interop.Excel._Application.Version%2A>)）验证最低版本，而不是特定版本。 不建议你依赖于 Office 二进制元数据、安装路径或注册表项，因为它们可能在安装、环境和版本之间发生更改。

## <a name="enable-both-32-bit-and-64-bit-office-usage"></a>同时启用32位和64位办公室
除非你的解决方案依赖于仅可用于特定位数的库，否则默认生成目标应同时支持32位 (x86) 和64位 (x64) 。 64位版本的 Office 正在采用，尤其是在大数据环境中。 同时支持32位和64位使用户能够更轻松地在 Office 的32位和64位版本之间过渡。

编写 VBA 代码时，请使用64位安全声明语句并根据需要转换变量。 此外，通过提供每个位数的代码，确保可在运行32位或64位版本 Office 的用户之间共享文档。 有关详细信息，请参阅 [应用程序的64位 Visual Basic](/office/vba/Language/Concepts/Getting-Started/64-bit-visual-basic-for-applications-overview)。

## <a name="support-restricted-environments"></a>支持受限环境
解决方案不应要求用户帐户提升或管理员权限。 此外，该解决方案不应依赖于设置或更改：

- 当前工作目录。
- DLL 加载目录。
- 路径变量。

## <a name="change-the-save-location-of-shared-data-and-settings"></a>更改共享数据和设置的保存位置
如果解决方案包含外接程序和 Office 外部的进程，请不要使用用户的应用程序数据文件夹或注册表在外接程序和外部进程之间交换数据或设置。 而应考虑使用用户的临时文件夹、documents 文件夹或解决方案的安装目录。

## <a name="increment-the-version-number-with-each-update"></a>递增每个更新的版本号
设置解决方案中二进制文件的版本号，并将其与每个更新递增。 这会使用户更轻松地识别版本之间的更改并评估兼容性。

## <a name="provide-support-statements-for-the-latest-versions-of-office"></a>为 Office 的最新版本提供支持声明
客户要求 Isv 为在 Office 中运行的 COM、VSTO 和 VBA 外接程序提供支持声明。 列出你的显式支持语句可帮助使用适用于企业的 Microsoft 365 应用程序的客户了解你的支持。

若要为 Office 客户端应用程序提供支持语句 (例如，Word 或 Excel) ，请首先验证外接程序是否在当前 Office 版本中运行，然后在将来的版本中的外接程序中断的情况下提交以提供更新。 当 Microsoft 发布新版本或 Office 更新时，无需测试外接程序。 Microsoft 很少在 Office 中更改 COM、VSTO 和 VBA 扩展性平台，这些更改将会很好地记录下来。

>重要说明： Microsoft 维护了支持的加载项列表，其中列出了准备情况报表和 ISV 联系信息。 若要使外接程序列出，请参阅 [/configmgr/desktop-analytics/ready-for-windows](/configmgr/desktop-analytics/ready-for-windows)。

## <a name="use-process-monitor-to-help-debug-installation-or-loading-issues"></a>使用进程监视器帮助调试安装或加载问题
如果你的外接程序在安装或加载过程中存在兼容性问题，它们可能与文件或注册表访问问题有关。 使用 [进程监视器](/sysinternals/downloads/procmon) 或类似的调试工具来记录和比较工作环境的行为，以帮助确定问题。
