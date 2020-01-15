---
title: Dotfuscator 的功能
ms.date: 03/28/2019
ms.devlang: dotnet
ms.topic: conceptual
keywords: Dotfuscator, Dotfuscator Community, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, 保护, 社区版, 模糊处理, .NET, 免费, Visual Studio 2017, Visual Studio 2019, Visual Studio
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator Community
- Dotfuscator CE
- Dotfuscator
- obfuscation
- protection
description: 了解 Visual Studio 中包含的免费 Dotfuscator Community 副本的功能。
ms.assetid: 0ee89c58-c900-48fc-a6a2-65ace00e8bab
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 019acd338ab49dd08255e3dc5d174cf2e371b71e
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918408"
---
# <a name="capabilities-of-dotfuscator"></a>Dotfuscator 的功能

本页重点介绍 Dotfuscator Community 的功能，并提供了可通过[升级][upgrades]获取的对高级选项的部分引用。

Dotfuscator Community 是 .NET 应用程序的后期生成  系统。
使用它，Visual Studio 用户可[模糊处理程序集][obfuscation]，还可将[主动防御措施][checks]注入应用程序 - 全部都无需 Dotfuscator 访问原始源代码。
Dotfuscator 以多种方式保护应用程序，并创建了分层保护策略。

Dotfuscator Community 支持各种 .NET 程序集和应用程序类型，包括[通用 Windows 平台 (UWP)][uwp] 和 [Xamarin][xamarin]。

## <a name="intellectual-property-protection"></a>知识产权保护

应用程序的设计、行为和实现是各种形式的知识产权 (IP)。
但是，为 .NET 创建的应用程序实质上是公开透明的；[因其包含高级元数据和中间代码][assemblies]，可以轻松地对 .NET 程序集进行反向工程处理。

Dotfuscator Community 中包括以[重命名][renaming]形式进行的基本 [.NET 模糊处理][obfuscation]。
使用 Dotfuscator 对代码进行模糊处理可降低通过反向工程对源代码进行未经授权访问的风险，因为重要的命名信息将不再公开。
就用户而言，模糊处理还努力保护代码免受检查 - 这在将 IP 作为商业机密进行合法保护过程中非常有价值的一步。

Dotfuscator Community 具有多种[应用程序完整性保护功能](#application-integrity-protection)，从而可进一步阻止反向工程。
例如，不良参与者为了解程序逻辑，可能尝试将调试器附加到正在运行的应用程序实例。
Dotfuscator 可以将[反调试行为][debug]注入应用程序以阻止这种情况。

## <a name="application-integrity-protection"></a>应用程序完整性保护

除了保护源代码，确保按设计使用应用程序也很重要。
攻击者可能会试图劫持应用程序，以避开许可策略（即软件盗版），窃取或操纵应用程序处理的敏感数据，或者更改应用程序的行为。

Dotfuscator Community 可将[应用程序验证代码][checks]插入程序集（包括[防篡改][tamper]、[反调试][debug]和[防取得 root 权限的设备][root]措施）。
检测到无效的应用程序状态时，验证代码可[要求应用程序代码以适当方式处理该情况][check-app]。
或者，如果不想编写代码来处理应用程序的无效使用，Dotfuscator 还可以注入[响应][check-action]行为，无需对源代码进行任何修改。

许多这些相同的方法还可用于针对评估和试用软件，强制实施[使用周期结束的最后期限][shelflife]。

## <a name="see-also"></a>请参阅

[完整 Dotfuscator Community 用户指南中的本主题][full]

<!-- Copyright © 2019 PreEmptive Solutions, LLC -->

[assemblies]:  /dotnet/standard/assembly-format
[uwp]:  https://www.preemptive.com/blog/article/856-uwp-applications-in-dotfuscator-ce/91-dotfuscator-ce
[xamarin]:  https://www.preemptive.com/obfuscating-xamarin-with-dotfuscator

[upgrades]:  upgrades.md

[obfuscation]:  https://www.preemptive.com/dotfuscator/ce/docs/help/obfuscation_overview.html
[renaming]:  https://www.preemptive.com/dotfuscator/ce/docs/help/obfuscation_renaming.html

[checks]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html
[check-app]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html#app-notification
[check-action]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html#action

[tamper]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_tamper.html
[debug]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_debug.html
[root]: https://www.preemptive.com/dotfuscator/ce/docs/help/checks_root.html
[shelflife]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_shelflife.html

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_capabilities.html
