

### jekyll基本用法：

##### jekyll build 

​	-->当前文件夹中的内容将会生成到 ./_site文件夹中

##### jekyll build --destination <destination>

​	=> 当前文件夹中的内容将会生成到目标文件夹<destination>中。

##### jekyll build --source <source> --destination <destination>

​	=> 指定源文件夹<source>中的内容将会生成到目标文件夹<destination>中

##### jekyll build --watch

​	=> 当前文件夹中的内容将会生成到 ./_site 文件夹中，
  		查看改变，并且自动再生成。

##### jekyll serve
​	 => 一个开发服务器将会运行在 http://localhost:4000/
​	 Auto-regeneration（自动再生成文件）: 开启。使用 `--no-watch` 来关闭。

##### jekyll serve --no-watch

​	=> 和 `jekyll serve` 一样，但不会监测变化。

##### Jekyll 网站的目录结构

一个基本的 Jekyll 网站的目录结构一般是像这样的：

```
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html
```



| `_config.yml`                                        | 保存[配置](http://jekyllcn.com/docs/configuration/)数据。很多配置选项都可以直接在命令行中进行设置，但是如果你把那些配置写在这儿，你就不用非要去记住那些命令了。 |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| `_drafts`                                            | drafts（草稿）是未发布的文章。这些文件的格式中都没有 `title.MARKUP` 数据。学习如何 [使用草稿](http://jekyllcn.com/docs/drafts/). |
| `_includes`                                          | 你可以加载这些包含部分到你的布局或者文章中以方便重用。可以用这个标签 `{% include file.ext %}` 来把文件 `_includes/file.ext` 包含进来。 |
| `_layouts`                                           | layouts（布局）是包裹在文章外部的模板。布局可以在 [YAML 头信息](http://jekyllcn.com/docs/frontmatter/)中根据不同文章进行选择。 这将在下一个部分进行介绍。标签 `{{ content }}` 可以将content插入页面中。 |
| `_posts`                                             | 这里放的就是你的文章了。文件格式很重要，必须要符合:`YEAR-MONTH-DAY-title.MARKUP`。 [永久链接](http://jekyllcn.com/docs/permalinks/) 可以在文章中自己定制，但是数据和标记语言都是根据文件名来确定的。 |
| `_data`                                              | 格式化好的网站数据应放在这里。jekyll 的引擎会自动加载在该目录下所有的 yaml 文件（后缀是 `.yml`, `.yaml`, `.json` 或者 `.csv` ）。这些文件可以经由 ｀site.data｀ 访问。如果有一个 `members.yml` 文件在该目录下，你就可以通过 `site.data.members` 获取该文件的内容。 |
| `_site`                                              | 一旦 Jekyll 完成转换，就会将生成的页面放在这里（默认）。最好将这个目录放进你的 `.gitignore` 文件中。 |
| `.jekyll-metadata`                                   | 该文件帮助 Jekyll 跟踪哪些文件从上次建立站点开始到现在没有被修改，哪些文件需要在下一次站点建立时重新生成。该文件不会被包含在生成的站点中。将它加入到你的 `.gitignore` 文件可能是一个好注意。 |
| `index.html` and other HTML, Markdown, Textile files | 如果这些文件中包含 [YAML 头信息](http://jekyllcn.com/docs/frontmatter/) 部分，Jekyll 就会自动将它们进行转换。当然，其他的如 `.html`, `.markdown`, `.md`, 或者 `.textile` 等在你的站点根目录下或者不是以上提到的目录中的文件也会被转换。 |
| Other Files/Folders                                  | 其他一些未被提及的目录和文件如 `css` 还有 `images` 文件夹，`favicon.ico` 等文件都将被完全拷贝到生成的 site 中。这里有一些[使用 Jekyll 的站点](http://jekyllcn.com/docs/sites/)，如果你感兴趣就来看看吧。 |

##### _config.yml配置

| **Site Source**修改 Jekyll 读取文件的路径                    | `source: DIR``-s, --source DIR`                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Site Destination**修改 Jekyll 写入文件的路径               | `destination: DIR``-d, --destination DIR`                    |
| **Safe**禁用 [自定义插件](http://jekyllcn.com/docs/plugins/)。 | `safe: BOOL``--safe`                                         |
| **Exclude**转换时排除某些文件、文件夹                        | `exclude: [DIR, FILE, ...]`                                  |
| **Include**转换时强制包含某些文件、文件夹。`.htaccess` 是个典型的例子，因为默认排除 . 开头的文件。 | `include: [DIR, FILE, ...]`                                  |
| **Keep files**当生成站点时，保留选择的文件。对文件不是由 jekyll 生成是有用的。例如由你的构建工具生成的文件或者资源。路径是相对于 `destination` 。 | `keep_files: [DIR, FILE, ...]`                               |
| **Time Zone**设置时区，这个设置作用于 `TZ` 变量， Ruby 用它来处理日期和时间。 [IANA Time Zone Database](http://en.wikipedia.org/wiki/Tz_database) 里边的都有效，比如 `America/New_York` 。默认值为操作系统的时区。 | `timezone: TIMEZONE`                                         |
| **Encoding**设置文件的编码，仅 Ruby 1.9 以上可用。2.0.0　版本以后默认值为 utf-8，之前版本默认值为 nil，使用 Ruby 默认的 `ASCII-8BIT`。可以用命令 `ruby -e 'puts Encoding::list.join("\n")'` 查看 Ruby 可用的编码。 | `encoding: ENCODING`                                         |
| **Defaults**设置 [YAML 头信息](http://jekyllcn.com/docs/frontmatter/) 的默认值。 | [详细](http://jekyllcn.com/docs/configuration/#front-matter-defaults) |

###### 编译选项

| **Regeneration**允许文件修改时自动重新生成网站。             | `-w, --watch`                          |
| ------------------------------------------------------------ | -------------------------------------- |
| **Configuration**手动设置配置文件，可设置多个，且后边的配置会覆盖前边的。 | `--config FILE1[,FILE2,...]`           |
| **Drafts**处理草稿                                           | `--drafts`                             |
| **Environment**build　时使用特定的环境变量。                 | `JEKYLL_ENV=production`                |
| **Future**用将来的日期发布文章                               | `future: BOOL``--future`               |
| **LSI**为相关文章生成索引                                    | `lsi: BOOL``--lsi`                     |
| **Limit Posts**限制文章的数量                                | `limit_posts: NUM``--limit_posts NUM`  |
| **Force polling**强制使用轮询。                              | `--force_polling`                      |
| **Verbose output**显示详细输出。                             | `-V, --verbose`                        |
| **Silence Output**在编译期间不显示的正常输出。               | `-q, --quiet`                          |
| **Incremental build**启用实验特性 incremental build。Incremental build 只重建修改过的 posts 和 pages，对大型网站有显著的性能提升，但在特定情况下也会影响网站生成。 | `incremental: BOOL``-I, --incremental` |
| **Liquid profiler**生成一个Liquid概述文档来帮助你发现性能瓶颈 | `profile: BOOL``--profile`             |

###### 服务选项

除了下边的选项， `serve` 命令还可以接收 `build` 的选项，当运行网站服务之前的编译时候使用。

| 设置                                                         | 选项 和 标记                      |
| ------------------------------------------------------------ | --------------------------------- |
| **Local Server Port**监听所给的端口                          | `port: PORT``--port PORT`         |
| **Local Server Hostname**监听所给的主机名                    | `host: HOSTNAME``--host HOSTNAME` |
| **Base URL**网站的根路径                                     | `baseurl: URL``--baseurl URL`     |
| **Detach**从终端命令行中分离出来                             | `detach: BOOL``-B, --detach`      |
| **Skips the initial site build.**跳过服务器启动之前，网站的初始化。 | `--skip-initial-build`            |
| **X.509 (SSL) Private Key**SSL私钥                           | `--ssl-key`                       |
| **X.509 (SSL) Certificate**SSL公证                           | `--ssl-cert`                      |



##### 头信息：

######  [YAML](http://yaml.org/) 头信息

``````
---
layout: post
title: Blogging Like a Hacker
---
``````



###### 预定义的全局变量

你可以在页面或者博客的头信息里设置这些已经预定义好的全局变量。

| 变量名称    | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| `layout`    | 如果设置的话，会指定使用该模板文件。指定模板文件时候不需要文件扩展名。模板文件必须放在 `_layouts` 目录下。 |
| `permalink` | 如果你需要让你发布的博客的 URL 地址不同于默认值 `/year/month/day/title.html`，那你就设置这个变量，然后变量值就会作为最终的 URL 地址。 |
| `published` | 如果你不想在站点生成后展示某篇特定的博文，那么就设置（该博文的）该变量为 false。 |

###### 在文章中预定义的变量

在文章中可以使用这些在头信息变量列表中未包含的变量。

| 变量名称               | 描述                                                         |
| ---------------------- | ------------------------------------------------------------ |
| `date`                 | 这里的日期会覆盖文章名字中的日期。这样就可以用来保障文章排序的正确。日期的具体格式为`YYYY-MM-DD HH:MM:SS +/-TTTT`；时，分，秒和时区都是可选的。 |
| `category``categories` | 除过将博客文章放在某个文件夹下面外，你还可以指定博客的一个或者多个分类属性。这样当你的站点生成后，这些文章就可以根据这些分类来阅读。`categories` 可以通过 [YAML list](http://en.wikipedia.org/wiki/YAML#Lists)，或者以逗号隔开的字符串指定。 |
| `tags`                 | 类似分类 `categories`，一篇文章也可以给它增加一个或者多个标签。同样，`tags` 可以通过 YAML 列表或者以逗号隔开的字符串指定。 |

##### 提示™: 不要重复

如果你不想重复设置你常用的头信息变量，只需为它们定义[默认值](http://jekyllcn.com/docs/configuration/#front-matter-defaults)，仅在必要的时候（或者从不）覆盖它们即可。这种方式对预定义变量和自定义变量都有效。



###### 文章文件夹

​		在目录结构介绍中说明过，所有的文章都在 _posts 文件夹中。这些文件可以用 Markdown 编写，也可以用 Textile 格式编写。**只要文件中有 YAML 头信息**，**它们就会从源格式转化成 HTML 页面**，从而成为你的静态网站的一部分。

创建文章的文件Permalink
发表一篇新文章，你所需要做的就是在 _posts 文件夹中创建一个新的文件。文件名的命名非常重要。Jekyll 要求一篇文章的文件名遵循下面的格式：

```
年-月-日-标题.MARKUP
```

###### 引用图片和其它资源

很多时候，你需要在文章中引用图片、下载或其它数字资源。尽管 Markdown 和 Textile 在链接这些资源时的语法并不一样，但你只需要关心在站点的哪些地方保存这些文件。

由于 Jekyll 的灵活性，有很多方式可以解决这个问题。一种常用做法是在工程的根目录下创建一个文件夹，命名为　assets 或者 downloads，将图片文件，下载文件或者其它的资源放到这个文件夹下。然后在任何一篇文章中，它们都可以用站点的根目录来进行引用。这和你站点的域名/二级域名和目录的设置相关，下面有一些例子（Markdown 格式）来演示怎样利用 site.url 变量来解决这个问题。

在文章中引用一个图片

… 从下面的截图可以看到：
![有帮助的截图]({{ site.url }}/assets/screenshot.jpg)





###### 文章的目录

所有文章都在一个目录中是没有问题的，但是如果你不将文章列表列出来博客文章是不会被人看到。在另一个页面上创建文章的列表（或者使用模版）是很简单的。感谢 Liquid 模版语言和它的标记，下面是如何创建文章列表的简单例子：

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
当然，你可以完全控制怎样（在哪里）显示你的文章，如何管理你的站点。如果你想了解更多你需要读一下 Jekyll 的模版是怎样工作的这篇文章。

请注意，post 变量仅在 for 循环中存在。如果你希望使用当前呈现的页面/博文中的变量（在 for 循环中的博文/页面的变量），请使用 page 变量来替代它。