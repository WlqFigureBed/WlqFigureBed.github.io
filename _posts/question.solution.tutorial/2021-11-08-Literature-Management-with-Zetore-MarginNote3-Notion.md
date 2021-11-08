---
layout:     post
title:      "文献管理：Zetore+MarginNote3+Notion"
subtitle:   "Literature Management：Zetore+MarginNote3+Notion"
date:       2021-11-08 16:30:00
author:     "HapppyTsing"
catalog: false
header-style: text
tags:
  - 科研
---

# BackGround

使用Zetore进行文献管理，MarginNote3阅读论文，Notion做笔记，但是三者各自独立，经过一番探索，发现可以使用Zetore作为中枢，连接MN3和Notion，实现跨平台的完美联动。

# Download icons

- [notion.ico](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/202111081503427.ico)
- [marginnote.ico](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/202111081459879.ico)

Download the file to the directory：`~/Zotero/locate`

![locate](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/202111081621710.png)

# Configure engines.json

```shell
cd ~/Zotero/locate
vim engines.json # You can also use：open engines.json
```

Add as following

```json
[

	{
    // Do not change the original configuration, simply add below it
	},
	{
		"_name": "Notion",
		"_alias": "Notion",
		"_description": "Notion",
		"_icon": "file:///Users/happytsing/Zotero/locate/notion.ico",
		"_hidden": false,
		"_urlTemplate": "https://www.notion.so/{z:callNumber}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/202111081503427.ico"
	},
		{
		"_name": "MarginNote3",
		"_alias": "MarginNote3",
		"_description": "MarginNote3",
		"_icon": "file:///Users/happytsing/Zotero/locate/marginnote.ico",
		"_hidden": false,
		"_urlTemplate": "marginnote3app://notebook/{z:extra}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/202111081459879.ico"
	}
]
```

Save `engines.json` and Restart Zetore！

# Get keyword

## Notion

- Select the page you want to link to Zetore
- Copy link：`command + L`

## MarginNote3

- Select the notebook you want to link to Zetore
- Copy link：`复制笔记本URL`

# Link to Zetore

Now we have links to notion and mn3's notes.

Notion link：

```shell
https://www.notion.so/Test-54c46d3e952c443f809e1c904f0e0787
```

MarginNote3 link：

```shell
marginnote3app://notebook/BAEFA408-7373-4D6C-8525-7489690CD1AE
```

Look again at the file `engines.json`：

```shell
"_urlTemplate": "https://www.notion.so/{z:callNumber}"
"_urlTemplate": "marginnote3app://notebook/{z:extra}"
```

So we just need to change the `callNumber` and `extra`field in Zetore：

![Zetore](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/202111081551724.png)

Click on the green arrow above info：

![arrow](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/202111081558429.png)

View our final results：

![result](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/202111081600550.png)

Congratulations and enjoy!
