---
title: 团队资源管理器参考
ms.date: 12/04/2018
ms.topic: reference
ms.author: kaelli
author: KathrynEE
ms.manager: jillfra
ms.openlocfilehash: b1a956579b527de9df9d24bd09dda6ae48eff961
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74538576"
---
# <a name="team-explorer-reference"></a>团队资源管理器参考

本文提供关于团队资源管理器中各种功能的 Azure DevOps 文章的链接  。

使用“团队资源管理器”工具窗口与其他团队成员协调代码工作，以开发项目，并管理分配给你、你的团队或项目的工作  。 团队资源管理器将 Visual Studio 连接到 Git 和 GitHub 存储库、Team Foundation 版本控制 (TFVC) 存储库以及 [Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) 或本地 [Azure DevOps Server](/azure/devops/index-all)（以前称为 TFS）上托管的项目  。 你可管理源代码、工作项和生成。

## <a name="home-page"></a>主页

在团队资源管理器中[连接到项目](../connect-team-project.md)后，“项目”部分中提供以下链接   ：

- [克隆存储库](/azure/devops/repos/git/clone)
- [Web 门户](/azure/devops/project/navigation/index)
- [任务板](/azure/devops/boards/sprints/task-board)

根据用户是连接到 [Git](/azure/devops/repos/git/gitquickstart?view=vsts&tabs=visual-studio) 还是 [Team Foundation 版本控制 (TFVC)](/azure/devops/repos/tfvc/overview) 存储库，“开始”页具有不同功能  。

> [!TIP]
> 要比较这两个版本控制系统，请参见[为项目 (Azure DevOps) 选择正确的版本控制](/azure/devops/repos/tfvc/comparison-git-tfvc)。

| Git 附带的**主页** | TFVC 附带的**主页** |
| - | - |
| ![Visual Studio 2019 中使用 Git 的团队资源管理器主页](media/team-explorer-reference/team-explorer-git.png) | ![Visual Studio 中使用 TFVC 的团队资源管理器主页](media/team-explorer-reference/team-explorer-tfvc.png) |

## <a name="changes-page-git"></a>更改页 (Git)

请参阅[通过提交保存工作](/azure/devops/repos/git/commits)。

## <a name="branches-page-git"></a>分支页 (Git)

请参阅[在分支中创建工作](/azure/devops/repos/git/branches)。

## <a name="pull-requests-page-git"></a>拉取请求页面 (Git)

请参阅[通过拉取请求评审代码](/azure/devops/repos/git/pullrequest)。

## <a name="sync-page-git"></a>同步页面 (Git)

请参阅[通过提取和拉取更新代码](/azure/devops/repos/git/pulling)。

## <a name="tags-page-git"></a>标记页 (Git)

请参阅[使用 Git 标记](/azure/devops/repos/git/git-tags)。

## <a name="my-work-page-tfvc"></a>“我的工作”页 (TFVC)

请参阅[暂停/继续工作](/azure/devops/repos/tfvc/suspend-your-work-manage-your-shelvesets)和[代码评审](/azure/devops/repos/tfvc/day-life-alm-developer-suspend-work-fix-bug-conduct-code-review)。

## <a name="pending-changes-page-tfvc"></a>“挂起的更改”页 (TFVC)

请参阅[管理挂起的更改](/azure/devops/repos/tfvc/develop-code-manage-pending-changes)、[查找搁置集](/azure/devops/repos/tfvc/suspend-your-work-manage-your-shelvesets)和[解决冲突](/azure/devops/repos/tfvc/resolve-team-foundation-version-control-conflicts)。

## <a name="source-control-explorer-page-tfvc"></a>源代码管理器页面 (TFVC)

请参阅[添加/查看文件和文件夹](/azure/devops/repos/tfvc/add-files-server)。

## <a name="work-items-page"></a>工作项页面

通过“工作项”页，可以查看[工作项](/azure/devops/boards/work-items/about-work-items)查询  。 请参阅：

- [添加工作项](/azure/devops/boards/backlogs/add-work-items)
- [使用查询编辑器来列出和管理查询](/azure/devops/boards/queries/using-queries)
- [组织查询文件夹并设置查询权限](/azure/devops/boards/queries/set-query-permissions)
- [在 Excel 中打开查询](/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel)
- [在 Project 中打开查询](/azure/devops/boards/backlogs/office/create-your-backlog-tasks-using-project)
- [使用 Outlook 以电子邮件的形式发送查询结果列表](/azure/devops/boards/queries/share-plans)
- [在 Excel 中从查询创建报表](/azure/devops/report/excel/create-status-and-trend-excel-reports)（仅针对 TFS）

::: moniker range=">= vs-2019"

> [!NOTE]
> Visual Studio 2019 中新增[工作项体验](/azure/devops/boards/work-items/set-work-item-experience-vs)。 有关在 Visual Studio 2019 中查看工作项的信息，请参阅[查看和添加工作项](/azure/devops/boards/work-items/view-add-work-items)。

::: moniker-end

## <a name="builds-page"></a>“生成”页

通过“生成”页，可以查看项目的生成定义  。

请参阅：

- [创建生成管道](/azure/devops/pipelines/tasks/index)
- [查看和管理生成](/azure/devops/pipelines/overview)
- [管理生成队列](/azure/devops/pipelines/agents/pools-queues)
- [安装用于 Visual Studio 的持续交付 (CD) 工具](/azure/devops/pipelines/apps/cd/azure/aspnet-core-to-acr#install-continuous-delivery-cd-tools-for-visual-studio-2017)
- [配置和执行应用的持续交付 (CD)](/azure/devops/pipelines/apps/cd/azure/aspnet-core-to-acr#configure-and-execute-continuous-delivery-cd-for-your-app)

## <a name="settings-page"></a>“设置”页

通过“设置”页，可以为项目或项目集合配置管理功能  。 请参阅以下文章：

| 项目 | 项目集合 | 其他 |
| - | - | - |
| [安全性，组成员身份](/azure/devops/organizations/security/set-project-collection-level-permissions)<br/>[安全性，源代码管理 (TFVC)](/azure/devops/organizations/security/set-git-tfvc-repository-permissions)<br/>[工作项区域](/azure/devops/organizations/settings/set-area-paths)<br/>[工作项迭代](/azure/devops/organizations/settings/set-iteration-paths-sprints)<br/>[门户设置](/azure/devops/report/sharepoint-dashboards/configure-or-add-a-project-portal)<br/>[项目警报](/azure/devops/notifications/howto-manage-team-notifications) | [安全性，组成员身份](/azure/devops/organizations/security/set-project-collection-level-permissions)<br/>[源代码管理 (TFVC)](/azure/devops/repos/tfvc/decide-between-using-local-server-workspace)<br/>[过程模板管理器](/azure/devops/boards/work-items/guidance/manage-process-templates) | [Git 全局设置](/azure/devops/repos/git/git-config)<br/>[Git 存储库设置](/azure/devops/repos/git/git-config) |

## <a name="see-also"></a>请参阅

- [连接到团队资源管理器中的项目](../../ide/connect-team-project.md)