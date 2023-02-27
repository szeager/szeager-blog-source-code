---
title: JenkinsX问题汇总
urlname: ohq67x
date: '2019-05-06 23:14:18 -0700'
tags: []
categories: []
---

1、secrets "jenkins" not found

```
$: jx ns jx
```

2、X Sorry, your reply was invalid: GET https://api.github.com/repos/xxx/jxtest01: 401 Bad credentials

```
➜  ~ jx delete git token -n GitHub admin
➜  ~ jx create git token -n GitHub szeager
Please generate an API Token for github server GitHub
Click this URL https://github.com/settings/tokens/new?scopes=repo,read:user,read:org,user:email,write:repo_hook,delete_repo

Then COPY the token and enter in into the form below:

? API Token: *****************************************
Created user szeager API Token for Git server GitHub at https://github.com
```

![1](/images/yuque/JenkinsX问题汇总/1.png)
