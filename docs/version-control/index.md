---
layout: LandingPage
title: 版本控制
description: Visual Studio 中的版本控制入门指南
keywords: VSTS, TFS, 版本控制
author: steved0x
ms.manager: jillfra
ms.author: sdanie
ms.date: 12/15/2017
ms.topic: landing-page
ms.prod: .net-core
ms.assetid: 2c119a5f-0272-48c0-8d6c-806196944aea
ms.workload:
- multiple
ms.openlocfilehash: 805fe86fcbebdfeb3747dd593d9abbf0f641212d
ms.sourcegitcommit: d4920babfc3d24a3fe1d4bf446ed3fe73b344467
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67160024"
---
# <a name="version-control-in-visual-studio"></a>Visual Studio 中的版本控制

版本控制系统有助于跟踪一段时间内的代码更改。 在用户进行更改的同时，版本控制系统会生成文件快照。 版本控制系统会永久保存此文件快照，以便用户稍后能够根据需要进行查阅。 Visual Studio 提供 [Git](/azure/devops/repos/git/index?view=vsts) 和 [Team Foundation 版本控制 (TFVC)](/azure/devops/repos/tfvc/index?view=vsts)。 若要在这两个系统之间做出选择，请参阅[选择适合项目的版本控制](/azure/devops/repos/tfvc/comparison-git-tfvc?toc=/visualstudio/version-control/toc.json&bc=/azure/devops/repos/git/breadcrumb/vc/toc.json)。

## <a name="git"></a>Git

Git 是现今最常用的版本控制系统，并迅速成为版本控制标准。 Git 是分布式版本控制系统。也就是说，代码的本地副本就是一个完整的版本控制存储库。 使用这些功能齐全的本地存储库，可以轻松开展脱机或远程工作。 先在本地提交工作，再将存储库的副本与服务器上的副本进行同步。 这种范例不同于集中式版本控制，后者要求客户端必须先与服务器同步代码，然后才能创建新版代码。

<!-- markdownlint-disable MD033 -->
<ul class="panelContent cardsFTitle">
    <li>
        <a href="/azure/devops/git/what-is-git">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="Git logo" src="https://docs.microsoft.com/media/common/i_git-mark.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>了解 Git</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="/azure/devops/repos/git/share-your-code-in-git-vs-2017">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="Git logo" src="https://docs.microsoft.com/media/common/i_git-mark.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Visual Studio 中的 Git 入门</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="/azure/devops/repos/git/clone">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="Git logo" src="https://docs.microsoft.com/media/common/i_git-mark.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>克隆现有 Git 存储库</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

## <a name="tfvc"></a>TFVC

Team Foundation 版本控制 (TFVC) 是一个集中式版本控制系统。 通常，团队成员的开发计算机上的每个文件只有一个版本。 历史数据仅在服务器上维护。 分支是基于路径的，并且在服务器上创建。

<ul class="panelContent cardsFTitle">
    <li>
        <a href="/azure/devops/repos/tfvc/overview">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="Visual Studio logo" src="https://docs.microsoft.com/media/logos/logo_visual-studio.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>了解 TFVC</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="/azure/devops/repos/tfvc/share-your-code-in-tfvc-vs">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="Visual Studio logo" src="https://docs.microsoft.com/media/logos/logo_visual-studio.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Visual Studio 中的 TFVC 入门</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
   <li>
        <a href="/azure/devops/repos/tfvc/get-code-reviewed-vs">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="Visual Studio logo" src="https://docs.microsoft.com/media/logos/logo_visual-studio.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>评审代码</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

## <a name="resources"></a>资源

- [《Pro Git》书籍](https://git-scm.com/book/en/v2)
- [计划迁移到 Git](https://docs.microsoft.com/azure/devops/git/centralized-to-git)
- [从 TFVC 迁移到 Git](https://docs.microsoft.com/azure/devops/git/migrate-from-tfvc-to-git)
- [版本控制 (Visual Studio for Mac)](/visualstudio/mac/version-control)