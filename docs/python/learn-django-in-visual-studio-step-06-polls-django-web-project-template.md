---
title: 学习 Visual Studio 中的 Django 教程的第 6 步，为项目模板投票
titleSuffix: ''
description: Visual Studio 项目上下文中 Django 基础知识的演练，具体介绍了投票 Django Web 项目模板的功能，例如管理自定义。
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 5e9220df4f9abdb806495e6108fb6039b28e0b7b
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254384"
---
# <a name="step-6-use-the-polls-django-web-project-template"></a>步骤 6：使用投票 Django Web 项目模板

**上一步：[在 Django 中对用户进行身份验证](learn-django-in-visual-studio-step-05-django-authentication.md)**

在了解 Visual Studio 的“Django Web 项目”模板后，现在可以查看第三个 Django 模板，“投票 Django Web 项目”，该模板基于相同的代码库构建而成，并演示如何使用数据库。

在此步骤中，你将了解如何：

> [!div class="checklist"]
> - 从模板创建项目并初始化数据库（步骤 6-1）
> - 了解数据模型（步骤 6-2）
> - 应用迁移（步骤 6-3）
> - 了解由项目模板创建的视图和页面模板（步骤 6-4）
> - 创建自定义管理界面（步骤 6-5）

使用此模板创建的项目类似于按照 Django 文档中[编写你的第一个 Django 应用](https://docs.djangoproject.com/en/2.0/intro/tutorial01/)教程所获取的项目。此 Web 应用包含公共站点，用户可以在其中查看投票并进行投票，还包含自定义管理界面，可以通过该界面管理投票。 它使用与“Django Web 项目”模板相同的身份验证系统，并通过实现 Django 模型来更加充分地使用数据库，如下面部分所探讨的那样。

## <a name="step-6-1-create-the-project-and-initialize-the-database"></a>步骤 6-1：创建项目并初始化数据库

1. 在 Visual Studio 中，转到解决方案资源管理器，右键单击在本教程前面创建的“LearningDjango”解决方案，并选择“添加” > “新项目”     。 （或者，如果想要使用新的解决方案，请改为选择“文件”   > “新建”   > “项目”  。）

1. 在“新项目”对话框中，搜索并选择“投票 Django Web 项目”模板，调用项目“DjangoPolls”并选择“确定”   。

1. 与 Visual Studio 中的其他项目模板类似，“投票 Django Web 项目”模板包括 requirements.txt 文件，Visual Studio 提示会询问在何处安装这些依赖项  。 选择“安装到虚拟环境”  选项，然后在“添加虚拟环境”  对话框中，选择“创建”  以接受默认设置。

1. 在 Python 完成设置虚拟环境后，按照 readme.html 中显示的说明初始化数据库，并创建 Django 超级用户（即管理员）  。 首先，右键单击解决方案资源管理器中的“DjangoPolls”项目，选择“Python” > “Django 迁移”命令，然后再次右键单击该项目，选择“Python” > “Django 创建超级用户”命令，并按照提示进行操作       。 （如果尝试首先创建超级用户，将看到错误，因为尚未初始化数据库。）

1. 若要将“DjangoPolls”项目设置为 Visual Studio 解决方案的默认值，可以在解决方案资源管理器中右键单击该项目，然后选择“设为启动项目”    。 启动项目（以粗体显示）会在启动调试器时运行。

1. 选择“调试” > “启动调试”(F5) 或使用工具栏上的“Web 服务器”按钮运行服务器     ：

    ![Visual Studio 中的运行 Web 服务器工具栏按钮](media/django/run-web-server-toolbar-button.png)

1. 该模板创建的应用有三个页面：“主页”、“关于”和“联系信息”，可以使用顶部导航栏在其中进行导航。 花一到两分钟的时间检查一下应用的不同部分（“关于”和“联系信息”页与“Django Web 项目”非常相似，不再进一步讨论）。

    ![投票 Django Web 项目应用的完整浏览器视图](media/django/step06-full-app-view.png)

1. 此外，选择导航栏中的“管理”  ，将显示登录屏幕，说明管理界面仅授权给经过身份验证的管理员使用。 使用超级用户凭据后，你将被路由到“/管理员”页，在使用此项目模板时，该页默认启用。

    ![投票 Django Web 项目应用的管理视图](media/django/step06-polls-administrative-interface.png)

1. 可以在以下各节中使应用保持运行状态。

    若要停止应用并[将更改提交到源代码管理](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)，首先打开团队资源管理器中的“更改”页，右键单击虚拟环境的文件夹（可能是 env），然后选择“忽略这些本地项”     。

### <a name="examine-the-project-contents"></a>检查项目内容

如前面所述。 如果已浏览 Visual Studio 中的其他项目模板，则应熟悉“投票 Django Web 项目”模板中所创建项目中的大部分内容。 本文中的其他步骤总结了更重要的更改和新增内容，即数据模型和附加视图。

### <a name="question-what-does-the-django-migrate-command-do"></a>问：Django 迁移命令的作用是什么？

答：“Django 迁移”命令专门运行 `manage.py migrate` 命令，该命令运行 app/migrations 文件夹中以前尚未运行的任何脚本   。 在这种情况下，此命令运行文件夹中的 0001_initial.py 脚本，以便在数据库中设置必要的架构  。

迁移脚本本身由 `manage.py makemigrations` 命令创建，它扫描应用的 models.py 文件，将其与数据库的当前状态进行比较，然后生成必要的脚本来迁移数据库架构以匹配当前模型  。 此 Django 功能非常强大，可以随着时间的推移更新和修改模型。 通过生成和运行迁移，可以轻松地使模型和数据库保持同步。

将在本文后面的步骤 6-3 中处理迁移。

## <a name="step-6-2-understand-data-models"></a>步骤 6-2：了解数据模型

app/models.py 中定义了名为“投票”和“选择”的应用模型  。 每个模型都是派生自 `django.db.models.Model` 的 Python 类，并使用 `models` 类的方法（如 `CharField` 和 `IntegerField`）在模型中定义字段，以此映射到数据库列。

```python
from django.db import models
from django.db.models import Sum

class Poll(models.Model):
    """A poll object for use in the application views and repository."""
    text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

    def total_votes(self):
        """Calculates the total number of votes for this poll."""
        return self.choice_set.aggregate(Sum('votes'))['votes__sum']

    def __unicode__(self):
        """Returns a string representation of a poll."""
        return self.text

class Choice(models.Model):
    """A poll choice object for use in the application views and repository."""
    poll = models.ForeignKey(Poll)
    text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    def votes_percentage(self):
        """Calculates the percentage of votes for this choice."""
        total = self.poll.total_votes()
        return self.votes / float(total) * 100 if total > 0 else 0

    def __unicode__(self):
        """Returns a string representation of a choice."""
        return self.text
```

如你所见，“投票”保留其 `text` 字段中的说明和 `pub_date` 中的发布日期。 这些字段是数据库中投票所有的唯一字段；`total_votes` 字段在运行时进行计算。

“选择”与通过 `poll` 字段实现的“投票”相关，在 `text` 中包含说明，并在 `votes` 中保留该选择的计数。 `votes_percentage` 字段在运行时计算，在数据库中找不到该字段。

字段类型的完整列表包括 `CharField`（受限文本）、`TextField`（不受限制的文本）、`EmailField`、`URLField`、`DateTimeField`、`IntegerField`、`DecimalField`、`BooleanField`、`ForeignKey`，和 `ManyToMany`。 每个字段都采用一些属性，如 `max_length`。 `blank=True` 属性表示字段是可选的；`null=true` 表示值是可选的。 此外还有一个 `choices` 属性，它限制数据值/显示值元组数组中值的值。 （请参阅 Django 文档中的[模型字段引用](https://docs.djangoproject.com/en/2.0/ref/models/fields/)。）

可使用像 [SQLite 浏览器](https://sqlitebrowser.org/)这样的工具检查项目中的 db.sqlite3 文件，从而准确地确认数据库中存储的内容  。 在数据库中，会看到“选择”模型中像 `poll` 这样的外键字段存储为 `poll_id`；Django 会自动处理映射。

一般来说，在 Django 中使用数据库意味着可以以独占方式通过模型进行工作，使 Django 可以代表你管理基础数据库。

### <a name="seed-the-database-from-samplesjson"></a>从 samples.json 设定数据库种子

最初，数据库不包含任何投票。 可使用“/admin”URL 中的管理界面手动添加投票，还可在正在运行的网站上访问“/seed”页面，以便使用应用的 samples.json 文件中定义的投票设定数据库种子  。

Django 项目的 urls.py 已添加 URL 模式 `url(r'^seed$', app.views.seed, name='seed'),`  。 app/views.py 中的 `seed` 视图加载 samples.json 文件并创建必要的模型对象   。 Django 随后会在基础数据库中自动创建匹配记录。

请注意使用 `@login_required` 修饰器来指示视图的授权级别。

```python
@login_required
def seed(request):
    """Seeds the database with sample polls."""
    samples_path = path.join(path.dirname(__file__), 'samples.json')
    with open(samples_path, 'r') as samples_file:
        samples_polls = json.load(samples_file)

    for sample_poll in samples_polls:
        poll = Poll()
        poll.text = sample_poll['text']
        poll.pub_date = timezone.now()
        poll.save()

        for sample_choice in sample_poll['choices']:
            choice = Choice()
            choice.poll = poll
            choice.text = sample_choice
            choice.votes = 0
            choice.save()

    return HttpResponseRedirect(reverse('app:home'))
```

要想看到效果，首先运行应用，查看是否尚不存在投票。 然后访问“/seed”URL，当应用返回到主页时，应会看到投票已变得可用。 同样，可以随时使用 [SQLite 浏览器](https://sqlitebrowser.org/)之类的工具检查原始 db.sqlite3 文件  。

![使用接受种子设定的数据库的投票 Django Web 项目应用](media/django/step06-app-with-seeded-database.png)

### <a name="question-is-it-possible-to-initialize-the-database-using-the-django-administrative-utility"></a>问：是否可以使用 Django 管理实用工具初始化数据库？

答：是的，可以使用 [django-admin loaddata 命令](https://docs.djangoproject.com/en/1.9/ref/django-admin/#loaddata)来完成与应用中的种子设定页相同的任务。 在处理完整的 Web 应用时，可以将以下两种方法结合使用：从命令行初始化数据库，然后将此处的种子页转换为 API，可以向其发送任何其他任意 JSON，而不是依赖于硬编码文件。

## <a name="step-6-3-use-migrations"></a>步骤 6-3：使用迁移

在创建项目后运行 `manage.py makemigrations` 命令时（在 Visual Studio 中使用上下文菜单），Django 创建了 app/migrations/0001_initial.py 文件  。 此文件包含用于创建初始数据库表的脚本。

因为随着时间的推移，会不可避免地对模型进行更改，借助 Django，可以轻松地将基础数据库架构与这些模型保持同步。 一般工作流如下：

1. 对 models.py 文件中的模型进行更改  。
1. 在 Visual Studio 中，右键单击“解决方案资源管理器”  中的项目，并选择“Python”   > “Django 迁移”  命令。 如前面所描述，此命令在 app/migrations 中生成脚本，将数据库从当前状态迁移到新状态  。
1. 若要将脚本应用到实际数据库，再次右键单击项目并选择“Python”   > “Django 迁移”  。

Django 跟踪哪些迁移已经应用到任何给定数据库，这样，在运行迁移命令时，Django 将应用所需的任何迁移。 如果创建一个新的空数据库，例如，运行迁移命令可通过应用每个迁移脚本将其与当前模型保持同步。 同样，如果在一台开发计算机上更改多个模型并生成迁移，可以通过在生产服务器上运行迁移命令将累积迁移应用到生产数据库。 Django 只会再次应用那些自从生产数据库的最后一次迁移以来生成的迁移脚本。

若要查看更改模型的效果，请尝试执行以下步骤：

1. 通过在 `pub_date` 字段后添加以下行来添加一个可选的 `author` 字段，向 app/models.py 中的投票模型添加可选的作者字段  ：

    ```python
    author = models.CharField(max_length=100, blank=True)
    ```

1. 保存文件，然后右键单击解决方案资源管理器中的“DjangoPolls”，并选择“Python” > “Django 迁移”命令     。
1. 选择“项目” > “显示所有文件”命令来查看 migrations 文件夹中新生成的脚本，其名称以 002_auto_ 开头     。 右键单击该文件，然后选择“包括在项目中”  。 然后，可以再次选择“项目”   > “显示所有文件”  以还原原始视图。 （有关此步骤的详细信息，请参阅下面的第二个问题。）
1. 如果需要，请打开该文件以检查 Django 脚本如何从以前的模型状态变更为新状态。
1. 再次右键单击 Visual Studio 项目并选择“Python”   > “Django 迁移”  ，向数据库应用更改。
1. 如果需要，请在相应查看器中打开该数据库以确认更改。

总的来说，Django 的迁移功能意味着你永远不需要手动管理数据库架构。 只需对模型进行更改，生成迁移脚本，并通过迁移命令应用它们。

### <a name="question-what-happens-if-i-forget-to-run-the-migrate-command-after-making-changes-to-models"></a>问：如果在对模型进行更改之后忘记运行迁移命令，会发生什么情况？

答：如果模型不匹配数据库中的内容，Django 会在运行时失败并出现相应的异常情况。 例如，如果忘记迁移上一节中所示的模型更改，会看到错误“没有此类列：app_poll.author”  ：

![未迁移模型更改时显示的错误](media/django/step06-exception-when-forgetting-to-migrate.png)。

### <a name="question-why-doesnt-solution-explorer-show-newly-generated-scripts-after-running-django-make-migrations"></a>问：为什么在运行 Django 迁移后解决方案资源管理器不显示新生成的脚本？

答：尽管新生成的脚本存在于 app/migrations 文件夹中，并在运行“Django 迁移”命令时应用，但它们不会自动显示在解决方案资源管理器中，因为还没有将它们添加到 Visual Studio 项目中    。 若要使其可见，请首先选择“项目”   > “显示所有文件”  菜单命令或下图所示的工具栏按钮。 此命令可使“解决方案资源管理器”  显示项目文件夹中的所有文件，对尚未添加到项目本身的项使用虚线轮廓线图标。 右键单击要添加的文件并选择“包括在项目中”  ，在下一次提交时，也会将文件附加到源代码管理中。

![解决方案资源管理器中的“包括在项目中”命令](media/django/step06-include-migrations-script-in-project.png)

### <a name="question-can-i-see-what-migrations-would-be-applied-before-running-the-migrate-command"></a>问：可在运行迁移命令之前看到要应用的迁移吗？

答：可以，请使用 [django-admin showmigrations 命令](https://docs.djangoproject.com/en/2.0/ref/django-admin/#showmigrations)。

## <a name="step-6-4-understand-the-views-and-page-templates-created-by-the-project-template"></a>步骤 6-4：了解通过项目模板创建的视图和页面模板

“投票 Django Web 项目”模板所生成的大部分视图（例如“关于”和“联系人”页视图）都与你在本教程中使用的“Django Web 项目”模板所创建的视图非常相似。 投票应用的不同之处在于，其主页使用了这些模型，因为有几个附加页用于投票和查看投票结果。

首先，在 urls.py 文件中，Django 项目 `urlpatterns` 数组的第一行不仅仅是简单地路由到应用视图  。 相反，它在应用自己的 urls.py 文件中拉取  ：

```python
from django.conf.urls import url, include
import app.views

urlpatterns = [
    url(r'^', include('app.urls', namespace="app")),
    # ..
]
```

然后，app/urls.py 文件包含一些更有趣的路由代码（添加了说明性注释）  ：

```python
urlpatterns = [
    # Home page routing
    url(r'^$',
        app.views.PollListView.as_view(
            queryset=Poll.objects.order_by('-pub_date')[:5],
            context_object_name='latest_poll_list',
            template_name='app/index.html',),
        name='home'),

    # Routing for a poll page, which use URLs in the form <poll_id>/,
    # where the id number is captured as a group named "pk".
    url(r'^(?P<pk>\d+)/$',
        app.views.PollDetailView.as_view(
            template_name='app/details.html'),
        name='detail'),

    # Routing for <poll_id>/results pages, again using a capture group
    # named pk.
    url(r'^(?P<pk>\d+)/results/$',
        app.views.PollResultsView.as_view(
            template_name='app/results.html'),
        name='results'),

    # Routing for <poll_id>/vote pages, with the capture group named
    # poll_id this time, which becomes an argument passed to the view.
    url(r'^(?P<poll_id>\d+)/vote/$', app.views.vote, name='vote'),
]
```

如果不熟悉此处使用的更复杂的正则表达式，可以将表达式粘贴到 [regex101.com](https://regex101.com/)，用简明的语言进行说明。 （需要在前面添加一个反斜杠 `\` 来转义正斜杠 `/`；在 Python 中不需要进行转义，因为字符串上的 `r` 前缀意味着“原始”）。

在 Django 中，语法 `?P<name>pattern` 创建了一个名为 `name` 的组，它以出现的顺序作为参数传递给视图。 如前面代码所示，`PollsDetailView` 和 `PollsResultsView` 接收名为 `pk` 的参数，`app.views.vote` 接收名为 `poll_id` 的参数。

此外还可以看到，大部分视图并不仅仅是对 app/views.py 中视图函数的直接引用  。 相反，它们引用同一个文件中派生自 `django.views.generic.ListView` 或 `django.views.generic.DetailView` 的类。 基类提供 `as_view` 方法，它采用 `template_name` 参数来标识模板。 在主页中使用的 `ListView` 基类还需要包含数据的 `queryset` 属性和带有变量名的 `context_object_name` 属性，将依据此变量名引用模板中的数据，在本例中为 `latest_poll_list`。

现在可以检查主页的 `PollListView`，它在 app/views.py 中按如下所示定义  ：

```python
class PollListView(ListView):
    """Renders the home page, with a list of all polls."""
    model = Poll

    def get_context_data(self, **kwargs):
        context = super(PollListView, self).get_context_data(**kwargs)
        context['title'] = 'Polls'
        context['year'] = datetime.now().year
        return context
```

在这里要做的就是标识与视图协同工作的模型（投票），并替代 `get_context_data` 方法，将 `title` 和 `year` 值添加到上下文。

模板的核心 (templates/app/index.html) 如下所示  ：

```html
{% if latest_poll_list %}
<table class="table table-hover">
    <tbody>
        {% for poll in latest_poll_list %}
        <tr>
            <td>
                <a href="{% url 'app:detail' poll.id %}">{{poll.text}}</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% else %}
<!-- ... other content omitted ... -->
{% endif %}
```

简单地说，模板接收 `latest_poll_list` 中的投票对象列表，然后循环访问该列表，以使用投票的 `text` 值创建一个表行，其中包含每个投票的一个链接。 在 `{% url %}` 标签中，“app:detail”指的是 app/urls.py 中命名为“detail”的 URL 模式，使用 `poll.id` 作为参数  。 此操作的效果是 Django 使用相应模式创建一个 URL，并将其用于链接。 这一点有待未来考验，意味着可以在任何时候更改 URL 模式，并且生成的链接会自动更新以进行匹配。

app/views.py 中的 `PollDetailView` 和 `PollResultsView` 类（此处未显示）看起来几乎与 `PollListView` 完全相同，只不过它们是派生自 `DetailView`  。 然后它们各自的模板（即 app/templates/details.html 和 app/templates/results.html）在各种 HTML 控件中通过模型放置相应的字段   。 details.html 中的一个独特部分是，投票选择包含在 HTML 表单中，在提交时，该表单将对 /vote URL 执行 POST 操作  。 如前面所示，该 URL 模式路由到 `app.views.vote`，其实现如下所示（请注意 `poll_id` 参数，它也是在此视图的路由中使用的正则表达式中的一个命名组）：

```python
def vote(request, poll_id):
    """Handles voting. Validates input and updates the repository."""
    poll = get_object_or_404(Poll, pk=poll_id)
    try:
        selected_choice = poll.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        return render(request, 'app/details.html', {
            'title': 'Poll',
            'year': datetime.now().year,
            'poll': poll,
            'error_message': "Please make a selection.",
    })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        return HttpResponseRedirect(reverse('app:results', args=(poll.id,)))
```

此处，视图没有自己对应的模板，就像其他页面一样。 相反，它会验证所选投票，如果投票不存在，则显示 404（以防他人输入类似于“vote/1a2b3c”的 URL）。 然后它会确保已投票选择对投票有效。 否则，`except` 块只会再次呈现包含错误消息的详细信息页。 如果选择有效，该视图将统计投票，并会重定向到结果页。

## <a name="step-6-5-create-a-custom-administration-interface"></a>步骤 6-5：创建自定义管理界面

“投票 Django Web 项目”模板的最后一个部分是对默认 Django 管理界面的自定义扩展，如本文前面的步骤 6-1 中所示。 默认界面针对用户和组管理目的而提供，但仅此而已。 投票项目模板还添加可用于管理投票的功能。

首先，Django 项目 urls.py 中的 URL 模式默认包含 `url(r'^admin/', include(admin.site.urls)),`；还包含注释掉的“admin/doc”模式  。

然后，应用包含文件 admin.py，在访问管理界面时 Django 将自动运行该文件，因为 settings.py 的 `INSTALLED_APPS` 数组中包含 `django.contrib.admin`   。 该文件中的代码（正如项目模板所提供的）如下所示：

```python
from django.contrib import admin
from app.models import Choice, Poll

class ChoiceInline(admin.TabularInline):
    """Choice objects can be edited inline in the Poll editor."""
    model = Choice
    extra = 3

class PollAdmin(admin.ModelAdmin):
    """Definition of the Poll editor."""
    fieldsets = [
        (None, {'fields': ['text']}),
        ('Date information', {'fields': ['pub_date']}),
    ]
    inlines = [ChoiceInline]
    list_display = ('text', 'pub_date')
    list_filter = ['pub_date']
    search_fields = ['text']
    date_hierarchy = 'pub_date'

admin.site.register(Poll, PollAdmin)
```

如你所见，`PollAdmin` 类派生自 `django.contrib.admin.ModelAdmin`，并从它所管理的 `Poll` 模型中使用名称来自定义多个字段。 在 Django 文档的 [ModelAdmin 选项](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/#modeladmin-options)上对这些字段进行了说明。

然后，对 `admin.site.register` 的调用将此类连接到模型 (`Poll`) 并将其包含在管理界面上。 总体结果如下所示：

![投票 Django Web 项目应用的管理视图](media/django/step06-polls-administrative-interface.png)

## <a name="next-steps"></a>后续步骤

> [!Note]
> 如果已在本教程的整个课程中将 Visual Studio 解决方案提交到源代码管理，那么现在是执行另一个提交的好时机。 解决方案应匹配 GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)。

现在，你已了解 Visual Studio 中“空白 Django Web 项目”、“Django Web 项目”和“投票 Django Web 项目”模板的全部内容。 你已了解包括使用视图和模板在内的所有 Django 基础知识，并了解了有关路由、身份验证和使用数据库模型的相关内容。 现在应能够使用任何所需的视图和模型来创建你自己的 Web 应用。

在开发计算机上运行 Web 应用只是使应用可供客户使用的一个步骤。 后续步骤可能包括以下任务：

- 将 Web 应用部署到生产服务器，如 Azure 应用服务。 请参阅[发布到 Azure 应用服务](publishing-python-web-applications-to-azure-from-visual-studio.md)。

- 通过创建一个名为 templates/404.html 的模板来自定义 404 页  。 如果存在该模板，Django 会使用此模板而不是其默认模板。 有关详细信息，请参阅 Django 文档中的[错误视图](https://docs.djangoproject.com/en/2.0/ref/views/#error-views)。

- 在 tests.py 中编写单元测试；Visual Studio 项目模板为这些测试提供起始点，若要了解更多信息，可以在 Django 文档的[编写首个 Django 应用，第 5 部分 - 测试](https://docs.djangoproject.com/en/2.0/intro/tutorial05/)和[在 Django 中进行测试](https://docs.djangoproject.com/en/2.0/topics/testing/)中找到  。

- 将应用从 SQLite 更改为生产级数据存储，如 PostgreSQL、MySQL 和 SQL Server（它们都可以在 Azure 上托管）。 如[何时使用 SQLite](https://www.sqlite.org/whentouse.html) (sqlite.org) 中所述，SQLite 适用于低到中等规模的流量站点（一天点击量不足 100K），不建议用于高点击量网站。 此外，它还仅限于一台计算机，因此不能在任何多服务器场景中使用，例如负载均衡和异地复制。 有关 Django 对其他数据库的支持的信息，请参阅[数据库设置](https://docs.djangoproject.com/en/2.0/intro/tutorial02/#database-setup)。 另外，还可以使用 [Azure SDK for Python](/azure/python/)，以便使用 Azure 存储服务，如表和 blob。

- 在 Azure DevOps 等服务上设置持续集成/持续部署管道。 除了使用源代码管理（通过 Azure Repos、GitHub 或在其他位置）外，还可以将 Azure DevOps 项目配置为自动运行单元测试作为发布的先决条件，并在部署到生产环境之前，将管道配置为部署到暂存服务器以进行附加测试。 此外，Azure DevOps 还与 App Insights 等监视解决方案集成，并使用敏捷规划工具闭合整个周期。 有关详细信息，请参阅[在 Azure DevOps 项目中为 Python 创建 CI/CD 管道](/azure/devops-project/azure-devops-project-python?view=vsts)以及常规 [Azure DevOps 文档](/azure/devops/?view=vsts)。
