---
title: 开发最佳做法：在 Office 中的 COM、 VSTO 和 VBA 外接程序
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
ms.openlocfilehash: 4689f14a6ce66f509a7af1f4a9a1d50a0f8d37cd
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401420"
---
# <a name="development-best-practices-for-com-vsto-and-vba-add-ins-in-office"></a>在 Office 中的 COM、 VSTO 和 VBA 外接程序的开发最佳实践
  如果你 office 开发 COM、 VSTO 或 VBA 的加载项，请按照本文中所述的开发最佳做法。   这将有助于确保：

- 加载项在不同版本和 Office 的部署之间的兼容性。
- 外接程序部署的用户和 IT 管理员的复杂性较低。
- 不会发生的外接程序的意外的安装或运行时失败。

>注意:使用[桌面桥](/windows/uwp/porting/desktop-to-uwp-root)若要准备您的 COM，VSTO 或 VBA 外接程序不支持 Windows 应用商店。 不能在 Windows 应用商店或 Office 应用商店中分布 COM、 VSTO 和 VBA 加载项。

## <a name="do-not-check-for-office-during-installation"></a>不会检查 office 安装过程
 我们不建议在外接程序检测是否在外接程序安装过程中安装 Office。 如果未安装 Office，您可以安装外接程序和用户将能够访问它后安装 Office。

## <a name="use-embedded-interop-types-nopia"></a>使用嵌入的互操作类型 (NoPIA)
如果你的解决方案使用.NET 4.0 或更高版本，使用嵌入的互操作类型 (NoPIA) 而不是具体取决于 Office 主互操作程序集 (PIA) 可再发行组件。 使用类型嵌入可以减少解决方案的安装大小，并确保将来的兼容性。 Office 2010 是 office 的最新版本随附 PIA 可再发行组件。 有关详细信息，请参见[演练：嵌入 Microsoft Office 程序集中的类型信息](https://msdn.microsoft.com/library/ee317478.aspx)并[类型等效性和嵌入的互操作类型](/windows/uwp/porting/desktop-to-uwp-root)。

如果您的解决方案使用.NET 的早期版本，我们建议你更新你的解决方案使用.NET 4.0 或更高版本。 使用.NET 4.0 或更高版本可减少在较新版本的 Windows 运行时必备组件。

## <a name="avoid-depending-on-specific-office-versions"></a>避免具体取决于特定的 Office 版本
如果您的解决方案使用选项仅适用于较新版本的 Office 的功能，验证在运行时 （例如，使用异常处理或通过检查版本） 的功能存在 （如果可能，请在功能级别）。 验证最小版本中，而不是特定版本中，使用支持的 Api 中的对象模型，如[Application.Version 属性](<xref:Microsoft.Office.Interop.Excel._Application.Version%2A>)。 我们不建议您依赖于 Office 二进制元数据、 安装路径或注册表项的，因为它们可以安装、 环境和版本之间进行更改。

## <a name="enable-both-32-bit-and-64-bit-office-usage"></a>启用 32 位和 64 位 Office 使用情况
在默认的 build 目标应支持 (x86) 32 位和 64 位 (x64)，除非你的解决方案依赖于它们仅适用于特定位数的库。 在采用，尤其是在大数据环境增加 Office 的 64 位版本。 支持 32 位和 64 位简化你的用户的 Office 的 32 位和 64 位版本之间的转换。

编写 VBA 代码时，使用 64 位安全声明语句，并将转换为相应的变量。 此外，请确保可以通过提供有关每个位数的代码运行 32 位或 64 位版本的 Office 的用户之间共享文档。 有关详细信息，请参阅[64 位 Visual Basic 应用程序概述](/office/vba/Language/Concepts/Getting-Started/64-bit-visual-basic-for-applications-overview)。

## <a name="support-restricted-environments"></a>支持受限制的环境
你的解决方案应该不需要用户帐户提升或管理员权限。 此外，该解决方案不应依赖于设置或更改：

- 当前工作目录中。
- 加载 DLL 的目录。
- PATH 变量中。

## <a name="change-the-save-location-of-shared-data-and-settings"></a>将更改保存共享的数据和设置的位置
如果解决方案包含外接程序和进程外部的 Office，不要使用用户的应用程序数据文件夹或注册表来交换数据或外接程序和外部进程之间的设置。 相反，请考虑使用用户的临时文件夹、 文档文件夹或你的解决方案的安装目录。

## <a name="increment-the-version-number-with-each-update"></a>每次更新版本号便会递增
在你的解决方案中设置的二进制文件的版本号，并增加每次更新。 这将使用户更轻松地识别版本之间的更改和评估兼容性。

## <a name="provide-support-statements-for-the-latest-versions-of-office"></a>提供最新版本的 Office 的支持声明
客户询问 Isv 提供其 COM、 VSTO 和 VBA 加载项在 Office 中运行的支持声明。 列出您使用 Office 365 专业增强版的显式支持语句可帮助客户准备工具了解你的支持。

若要提供 Office 客户端应用程序 （例如，Word 或 Excel） 的支持声明，请首先验证加载项在当前的 Office 版本中，运行，然后再提交到如果外接程序中断的未来版本中提供更新。 无需在 Microsoft 发布新的生成或对 Office 的更新时测试加载项。 Microsoft 很少更改在 Office 中的 COM、 VSTO 和 VBA 扩展性平台并妥善记录这些更改。

>重要提示：Microsoft 将维护一组用于准备情况报告和 ISV 的联系信息的加载项支持。 若要获取外接程序列出，请参阅[ https://aka.ms/readyforwindows ](https://aka.ms/readyforwindows)。

## <a name="use-process-monitor-to-help-debug-installation-or-loading-issues"></a>使用进程监视器来帮助调试安装或加载问题
如果外接程序在安装或负载期间存在兼容性问题，它们可能与文件或注册表访问问题。 使用[Process Monitor](/sysinternals/downloads/procmon)或类似的调试工具进行记录和比较行为对工作环境，以帮助识别问题。
