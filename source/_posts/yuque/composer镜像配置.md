
---

title: composer镜像配置

date: 2019-01-24 23:04:26 +0800

tags: [composer,php]

categories: PHP

---


<a name="KxNHb"></a>
# 使用laravel-china的镜像文件
<a name="9eMX3"></a>
## 如何使用?
使用 Composer 镜像加速有两种选项：

- 选项一：全局配置，这样所有项目都能惠及（推荐）；
- 选项二：单独项目配置；

选项一、全局配置（推荐）

```powershell
$ composer config -g repo.packagist composer https://packagist.laravel-china.org
```
选项二、单独使用<br />如果仅限当前工程使用镜像，去掉 -g 即可，如下：

```powershell
$ composer config repo.packagist composer https://packagist.laravel-china.org
```
取消镜像

```powershell
composer config -g --unset repos.packagist
```
<a name="J6DYM"></a>
## 遇到问题？
`composer` 命令后面加上 -vvv （是 3 个 v）可以打印出调错信息，命令如下：

```powershell
$ composer -vvv create-project laravel/laravel blog
$ composer -vvv require psr/log
```


