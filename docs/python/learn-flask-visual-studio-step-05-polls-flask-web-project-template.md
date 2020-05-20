---
title: 了解 Visual Studio 中的 Flask 教程步骤 5，投票项目模板
titleSuffix: ''
description: Visual Studio 项目上下文中 Flask 基础知识的演练，具体介绍了投票 Flask Web 项目和投票 Flask/Jade Web 项目模板的功能。
ms.date: 01/07/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: c540dfef9d2d46bb621432b3e37438e0b6b07298
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "70154898"
---
# <a name="step-5-use-the-polls-flask-web-project-template"></a>步骤 5：使用投票 Flask Web 项目模板

上一步：[使用完整的 Flask Web 项目模板](learn-flask-visual-studio-step-04-full-flask-project-template.md)

在了解 Visual Studio 的“Flask Web 项目”模板后，现在可以查看第三个 Flask 模板，“投票 Flask Web 项目”，该模板基于相同的代码库构建而成。

在此步骤中，你将了解如何：

> [!div class="checklist"]
> - 从模板创建项目并初始化数据库（步骤 5-1）
> - 了解数据模型（步骤 5-2）
> - 了解后备数据存储（步骤 5-3）
> - 了解投票详情和结果视图（步骤 5-4）

Visual Studio 还提供了“投票 Flask/Jade Web 项目”模板，该模板生成相同的应用，但 Jinja 模板引擎使用的是 Jade 扩展。 有关详细信息，请参阅[步骤 4 - Flask/Jade Web 项目模板](learn-flask-visual-studio-step-04-full-flask-project-template.md#the-flaskjade-web-project-template)。

## <a name="step-5-1-create-the-project"></a>步骤 5-1：创建项目

1. 在 Visual Studio 中，转到解决方案资源管理器，右键单击本教程中之前创建的“LearningFlask”解决方案，并选择“添加” > “新项目”。 （或者，如果想要使用新的解决方案，请改为选择“文件”   > “新建”   > “项目”  。）

1. 在“新项目”对话框中，搜索并选择“投票 Flask Web 项目”模板，调用项目“FlaskPolls”并选择“确定”   。

1. 与 Visual Studio 中的其他项目模板类似，“投票 Flask Web 项目”模板包括 requirements.txt 文件，Visual Studio 会询问在何处安装这些依赖项  。 选择“安装到虚拟环境”  选项，然后在“添加虚拟环境”  对话框中，选择“创建”  以接受默认设置。 （此模板需要 Flask 以及 azure-storage 和 pymongo 包；“投票 Flask/Jade Web 项目”还需要 pyjade。）

1. 在解决方案资源管理器中右键单击“FlaskPolls”项目，然后选择“设为启动项目”，从而将该项目设置为 Visual Studio 解决方案的默认值    。 启动项目（以粗体显示）会在启动调试器时运行。

1. 选择“调试” > “启动调试”(F5) 或使用工具栏上的“Web 服务器”按钮运行服务器：

    ![Visual Studio 中的运行 Web 服务器工具栏按钮](media/django/run-web-server-toolbar-button.png)

1. 该模板创建的应用有三个页面：“主页”、“关于”和“联系信息”，可以使用顶部导航栏在其中进行导航。 花一到两分钟时间检查应用的不同部分（“关于”和“联系信息”页与“Flask Web 项目”非常相似，不再进一步讨论）。

    ![投票 Flask Web 项目应用的完整视图](media/flask/step06-full-app-view.png)

1. 在主页上，“创建样本投票”按钮使用 models/samples.json 页中介绍的三种不同投票来初始化应用的数据存储   。 默认情况下，应用使用内存中数据库（如“关于”页中所示），每当应用重启时，它都会重置。 该应用还包含适用于 Azure 存储和 Mongo DB 的代码，如后文所述。

1. 初始化数据存储后，可以对主页上显示的不同调查进行投票（为简洁起见，省略了导航栏和页脚）：

    ![初始化数据存储后投票应用的视图](media/flask/step06-polls-initialized.png)

1. 选择一个调查，查看其具体选项：

    ![某调查的投票界面](media/flask/step06-polls-voting-interface.png)

1. 投票后，应用随即显示结果页并可再次投票：

    ![投票后的结果视图](media/flask/step06-polls-results.png)

1. 可以在以下各节中使应用保持运行状态。

    若要停止应用并[将更改提交到源代码管理](learn-flask-visual-studio-step-02-create-app.md#commit-to-source-control)，首先打开团队资源管理器中的“更改”页，右键单击虚拟环境的文件夹（可能是 env），然后选择“忽略这些本地项”     。

### <a name="examine-the-project-contents"></a>检查项目内容

如前面所述。 如果已了解 Visual Studio 中的其他项目模板，则应熟悉通过“投票 Flask Web 项目”模板（和“投票 Flask/Jade Web 项目”模板）创建的项目中的大部分内容。 本文中的其他步骤总结了更重要的更改和新增内容，即数据模型和附加视图。

## <a name="step-5-2-understand-the-data-models"></a>步骤 5-2：了解数据模型

应用的数据模型是名为 Poll 和 Choice 的 Python 类，它们在 models/\_\_init\_\_.py 中进行定义。 Poll 表示一个问题，Choice 实例集合表示该问题的可选答案。 Poll 还会保留（任意选项的）总票数，以及统计信息的计算方法（这些信息将用于生成视图）：

```python
class Poll(object):
    """A poll object for use in the application views and repository."""
    def __init__(self, key=u'', text=u''):
        """Initializes the poll."""
        self.key = key
        self.text = text
        self.choices = []
        self.total_votes = None

    def calculate_stats(self):
        """Calculates some statistics for use in the application views."""
        total = 0
        for choice in self.choices:
            total += choice.votes
        for choice in self.choices:
            choice.votes_percentage = choice.votes / float(total) * 100 \
                if total > 0 else 0
        self.total_votes = total

class Choice(object):
    """A poll choice object for use in the application views and repository."""
    def __init__(self, key=u'', text=u'', votes=0):
        """Initializes the poll choice."""
        self.key = key
        self.text = text
        self.votes = votes
        self.votes_percentage = None
```

这些数据模型是泛型抽象，可确保应用视图能在不同类型的后备数据存储情况下正常使用，下一步会介绍这些内容。

## <a name="step-5-3-understand-the-backing-data-stores"></a>步骤 5-3：了解后备数据存储

“投票 Flask Web 项目”模板创建的应用可针对内存中、Azure 表存储或 Mongo DB 数据库中的数据存储运行。

数据存储机制的工作原理如下：

1. 通过 `REPOSITORY_NAME` 环境变量指定存储库类型，可将其设置为“memory”、“azuretablestore”或“mongodb”。 settings.py 中的一段代码检索名称（默认使用“memory”）  。 如果想要更改后备存储，则必须设置环境变量并重启应用。

    ```python
    from os import environ
    REPOSITORY_NAME = environ.get('REPOSITORY_NAME', 'memory')
    ```

1. settings.py 代码随后初始化 `REPOSITORY_SETTINGS` 对象。 如果想要使用 Azure 表存储或 Mondo DB，则必须首先在其他位置初始化这些数据存储，然后设置必需的环境变量，用于告知应用如何连接到存储：

    ```python
    if REPOSITORY_NAME == 'azuretablestorage':
        REPOSITORY_SETTINGS = {
            'STORAGE_NAME': environ.get('STORAGE_NAME', ''),
            'STORAGE_KEY': environ.get('STORAGE_KEY', ''),
            'STORAGE_TABLE_POLL': environ.get('STORAGE_TABLE_POLL', 'polls'),
            'STORAGE_TABLE_CHOICE': environ.get('STORAGE_TABLE_CHOICE', 'choices'),
        }
    elif REPOSITORY_NAME == 'mongodb':
        REPOSITORY_SETTINGS = {
            'MONGODB_HOST': environ.get('MONGODB_HOST', None),
            'MONGODB_DATABASE': environ.get('MONGODB_DATABASE', 'polls'),
            'MONGODB_COLLECTION': environ.get('MONGODB_COLLECTION', 'polls'),
        }
    elif REPOSITORY_NAME == 'memory':
        REPOSITORY_SETTINGS = {}
    else:
        raise ValueError('Unknown repository.')
    ```

1. 在 views.py 中，应用调用工厂方法，使用数据存储名称和设置来初始化 `Repository` 对象：

    ```python
    from FlaskPolls.models import PollNotFound
    from FlaskPolls.models.factory import create_repository
    from FlaskPolls.settings import REPOSITORY_NAME, REPOSITORY_SETTINGS

    repository = create_repository(REPOSITORY_NAME, REPOSITORY_SETTINGS)
    ```

1. 在 models\factory.py 中找到 `factory.create_repository` 方法，该方法只导入相应的存储库模块，然后创建一个 `Repository` 实例：

    ```python
    def create_repository(name, settings):
        """Creates a repository from its name and settings. The settings
        is a dictionary where the keys are different for every type of repository.
        See each repository for details on the required settings."""
        if name == 'azuretablestorage':
            from .azuretablestorage import Repository
        elif name == 'mongodb':
            from .mongodb import Repository
        elif name == 'memory':
            from .memory import Repository
        else:
            raise ValueError('Unknown repository.')

        return Repository(settings)
    ```

1. 特定于每个数据存储的 `Repository` 类的实现可在 models\azuretablestorage.py、models\mongodb.py 和 models\memory.py 中找到    。 Azure 存储实现使用 azure-storage 包；Mongo DB 实现使用 pymongo 包。 如步骤 5-1 中所述，这两个包都包含在项目模板的 requirements.txt 文件中  。 浏览详细信息将作为读者的一个练习。

简言之，`Repository` 类提取数据存储的详细信息，应用在运行时使用环境变量来选择要使用三种实现中的哪一种并进行配置。

如果需要，可通过以下步骤添加对其他数据存储（除项目模板提供的这三种数据存储外）的支持：

1. 将 memory.py 复制到新文件，这样即可拥有 `Repository` 类的基本接口。
1. 修改类的实现，使其适合正在使用的数据存储。
1. 修改 factory.py，添加其他 `elif` 事例，用于识别添加的数据存储的名称，并导入相应模块。
1. 修改 settings.py，识别 `REPOSITORY_NAME` 环境变量中的其他名称，然后相应地初始化 `REPOSITORY_SETTINGS`。

### <a name="seed-the-data-store-from-samplesjson"></a>从 samples.json 设定数据存储种子

任何选定的数据存储最初都没有投票，因此应用的主页会显示消息“没有可用投票”和“创建样本投票”按钮   。 但是，选择按钮后，该视图就会更改为显示可用投票。 通过 templates\index.html 中的条件标记可实现此切换（为简洁起见，省略了一些空白行）  ：

```html
{% extends "layout.html" %}
{% block content %}
<h2>{{title}}.</h2>

{% if polls %}
<table class="table table-hover">
    <tbody>
        {% for poll in polls %}
        <tr>
            <td>
                <a href="/poll/{{poll.key}}">{{poll.text}}</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% else %}
<p>No polls available.</p>
<br />
<form action="/seed" method="post">
    <button class="btn btn-primary" type="submit">Create Sample Polls</button>
</form>
{% endif %}
{% endblock %}
```

模板中的 `polls` 变量来自对 `repository.get_polls` 的调用，在数据存储初始化之前，它不会返回任何内容。

选择“创建样本投票”按钮，导航到 /seed URL  。 在 views.py 中定义该路由的处理程序  ：

```python
@app.route('/seed', methods=['POST'])
def seed():
    """Seeds the database with sample polls."""
    repository.add_sample_polls()
    return redirect('/')
```

`repository.add_sample_polls()` 调用结束，最终将显示所选数据存储的某个特定 `Repository` 实现。 每个实现都调用 models\_\_init\_\_.py 中的 `_load_samples_json` 方法，将 models\samples.json 文件加载到内存中，再循环访问相应数据，以在数据存储中创建必要的 `Poll` 和 `Choice` 对象。

完成此过程后，`seed` 方法中的 `redirect('/')` 语句将返回到主页。 此时，因为 `repository.get_polls` 现在返回一个数据对象，所以 templates\index.html 中的条件标记会呈现一个包含投票的表  。

### <a name="question-how-does-one-add-new-polls-to-the-app"></a>问：如何向应用添加新的投票？

答：通过项目模板提供的应用没有添加或编辑投票的功能。 可通过修改 models\samples.json 来创建新的初始化数据，但这样意味着重置数据存储  。 要实现编辑功能，需要借助某些用于方法来扩展 `Repository` 类接口，创建必要的 `Choice` 和 `Poll` 实例，然后在使用这些方法的其他页中实现 UI。

## <a name="step-5-4-understand-the-poll-detail-and-results-views"></a>步骤 5-4：了解投票详情和结果视图

“投票 Flask Web 项目”和“投票 Flask/Jade Web 项目”模板所生成的大部分视图（例如“关于”和“联系人”页视图）都与你之前在本教程中使用的“Flask Web 项目”（或“Flask/Jade Web 项目”）模板所创建的视图非常相似。 在上一节中，也了解了如何实现主页来显示初始化按钮或投票列表。

剩下的部分将介绍如何查看单个投票的投票（详情）和结果视图。

从主页选择某项投票时，应用将导航至 URL /poll/\<key\>，其中 key 是该项投票的唯一标识符  。 在 views.py 中，可以发现分配了 `details` 函数来处理 GET 和请求的 URL 路由。 还可发现在 URL 路由中使用 `<key>` 同时将该表单的任意路由映射到同一个函数，并生成与其同名称的函数的参数：

```python
@app.route('/poll/<key>', methods=['GET', 'POST'])
def details(key):
    """Renders the poll details page."""
    error_message = ''
    if request.method == 'POST':
        try:
            choice_key = request.form['choice']
            repository.increment_vote(key, choice_key)
            return redirect('/results/{0}'.format(key))
        except KeyError:
            error_message = 'Please make a selection.'

    return render_template(
        'details.html',
        title='Poll',
        year=datetime.now().year,
        poll=repository.get_poll(key),
        error_message=error_message,
    )
```

为显示投票（GET 请求），该函数只调用 templates\details.html，用于循环访问投票的 `choices` 数组，从而为每项创建一个单选按钮。

```html
{% extends "layout.html" %}

{% block content %}

<h2>{{poll.text}}</h2>
<br />

{% if error_message %}
<p class="text-danger">{{error_message}}</p>
{% endif %}

<form action="/poll/{{poll.key}}" method="post">
    {% for choice in poll.choices %}
    <div class="radio">
        <label>
            <input type="radio" name="choice" id="choice{{choice.key}}" value="{{choice.key}}" />
            {{ choice.text }}
        </label>
    </div>
    {% endfor %}
    <br />
    <button class="btn btn-primary" type="submit">Vote</button>
</form>

{% endblock %}
```

“投票”按钮具有 `type="submit"`，因此选中它会生成一个 POST 请求，该请求返回再次路由到 `details` 函数的同一 URL。 不过，此时它从表单数据中提取选项并且重定向到 /results/\<choice\>。

然后，/result/\<key\> URL 将路由到 views.py 中的 `results` 函数，该函数随后调用投票的 `calculate_stats` 方法并使用 templates\results.html 呈现：

```python
@app.route('/results/<key>')
def results(key):
    """Renders the results page."""
    poll = repository.get_poll(key)
    poll.calculate_stats()
    return render_template(
        'results.html',
        title='Results',
        year=datetime.now().year,
        poll=poll,
    )
```

就其而言，results.html 模板只循环访问投票的选项并为每个选项生成一个进度栏  ：

```html
{% extends "layout.html" %}

{% block content %}

<h2>{{poll.text}}</h2>
<br />

{% for choice in poll.choices %}
<div class="row">
    <div class="col-sm-5">{{choice.text}}</div>
    <div class="col-sm-5">
        <div class="progress">
            <div class="progress-bar" role="progressbar" aria-valuenow="{{choice.votes}}" aria-valuemin="0" aria-valuemax="{{poll.total_votes}}" style="width: {{choice.votes_percentage}}%;">
                {{choice.votes}}
            </div>
        </div>
    </div>
</div>
{% endfor %}

<br />
<a class="btn btn-primary" href="/poll/{{poll.key}}">Vote again?</a>

{% endblock %}
```

## <a name="next-steps"></a>后续步骤

> [!Note]
> 如果已在本教程的整个课程中将 Visual Studio 解决方案提交到源代码管理，那么现在是执行另一个提交的好时机。 解决方案应匹配 GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)。

现在，你已经了解了 Visual Studio 中“空白 Flask Web 项目”、“Flask[/Jade] Web 项目”和“投票 Flask[/Jade] Web 项目”模板的全部内容。 学习了 Flask 的所有基础知识，例如使用视图、模板和路由，并已了解如何使用后备数据存储。 现在应该能够使用任何所需的视图和模型来创建自己的 Web 应用。

在开发计算机上运行 Web 应用只是使应用可供客户使用的一个步骤。 后续步骤可能包括以下任务：

- 将 Web 应用部署到生产服务器，如 Azure 应用服务。 请参阅[发布到 Azure 应用服务](publishing-python-web-applications-to-azure-from-visual-studio.md)。

- 添加一个使用其他生产级数据存储的存储库实现，如 PostgreSQL、MySQL 和 SQL Server（它们都可以在 Azure 上托管）。 另外，还可使用 [Azure SDK for Python](/azure/python/)，以便使用表和 blob 等 Azure 存储服务以及 Cosmos DB。

- 在 Azure DevOps 等服务上设置持续集成/持续部署管道。 除了使用源代码管理（通过 Azure Repos、GitHub 或在其他位置）外，还可以将 Azure DevOps 项目配置为自动运行单元测试作为发布的先决条件，并在部署到生产环境之前，将管道配置为部署到暂存服务器以进行附加测试。 此外，Azure DevOps 还与 App Insights 等监视解决方案集成，并使用敏捷规划工具闭合整个周期。 有关详细信息，请参阅[在 Azure DevOps Projects 中为 Python 创建 CI/CD 管道](/azure/devops-project/azure-devops-project-python?view=vsts)以及常规 [Azure DevOps 文档](/azure/devops/?view=vsts)。
