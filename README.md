Laravel.Smarty
==============
smarty template engine for laravel

[![Build Status](https://travis-ci.org/ytake/Laravel.Smarty.svg?branch=master)](https://travis-ci.org/ytake/Laravel.Smarty)
[![Coverage Status](https://coveralls.io/repos/ytake/Laravel.Smarty/badge.png?branch=master)](https://coveralls.io/r/ytake/Laravel.Smarty?branch=develop)
[![Dependency Status](https://www.versioneye.com/user/projects/541bfc296936193b68000060/badge.svg?style=flat)](https://www.versioneye.com/user/projects/541bfc296936193b68000060)
[![Code Climate](https://codeclimate.com/github/ytake/Laravel.Smarty/badges/gpa.svg)](https://codeclimate.com/github/ytake/Laravel.Smarty)
[![HHVM Status](http://hhvm.h4cc.de/badge/ytake/laravel-smarty.svg)](http://hhvm.h4cc.de/package/ytake/laravel-smarty)  

[![License](https://poser.pugx.org/ytake/laravel-smarty/license.svg)](https://packagist.org/packages/ytake/laravel-smarty)
[![Latest Stable Version](https://poser.pugx.org/ytake/laravel-smarty/v/stable.svg)](https://packagist.org/packages/ytake/laravel-smarty)
[![Total Downloads](https://poser.pugx.org/ytake/laravel-smarty/downloads.svg)](https://packagist.org/packages/ytake/laravel-smarty)
[![Latest Unstable Version](https://poser.pugx.org/ytake/laravel-smarty/v/unstable.svg)](https://packagist.org/packages/ytake/laravel-smarty)

##Basic
laravel4でsmartyを使用できます。  
bladeの構文をそのまま使用することができ、  
それに加え、View Facadeを通じてsmartyのmethodはすべて利用可能です。  
easily use all the methods of smarty  

```php
// laravel blade template render
\View::make('template', ['hello']);
// use smarty method
\View::assign('word', 'hello');  
\View::clearAllAssign(); // smarty method
```

###example
[registerFilter in ServiceProvider](https://gist.github.com/ytake/e8c834e88473ea3f10e7)  
[registerFilter in Controller](https://gist.github.com/ytake/1a6f1d5312b552bc83ff)  
[layout.sample](https://gist.github.com/ytake/11345539)  
[layout.extends.sample](https://gist.github.com/ytake/11345614)
##Install

###for Laravel4.2.*
```json
    "require": {
        "ytake/laravel-smarty": "1.2.*"
    },
```
###for Laravel4.1.*
```json
    "require": {
        "ytake/laravel-smarty": "1.1.*"
    },
```

##Artisan
キャッシュクリア、コンパイルファイルの削除がコマンドラインから行えます。  
smarty's cacheclear, remove compile class from Artisan(cli)
###cache clear
```bash
$ php artisan ytake:smarty-clear-cache
```

| Options  | description |
| ------------- | ------------- |
| --file (-f) | specify file |
| --time (-t) | clear all of the files that are specified duration time |
| --cache_id (-cache) | specified cache_id groups |

###remove compile class
```bash
$ php artisan ytake:smarty-clear-compiled
```

| Options  | description |
| ------------- | ------------- |
| --file (-f) | specify file |
| --compile_id (-compile) | specified compile_id |

###compile
```bash
$ php artisan ytake:smarty-optimize
```
| Options  | description |
| ------------- | ------------- |
| --extension (-e) | specified smarty file extension(default: *.tpl*) |
| --force | compiles template files found in views directory  |

Usage
==================

install後、
app/config配下のapp.phpのproviders配列に以下のnamespaceを追加してください。  
add providers
```php
'providers' => [
    'Ytake\LaravelSmarty\SmartyServiceProvider'
]
```

configファイルをpublishします。  
publish configure
```bash
$ php artisan config:publish ytake/laravel-smarty
```
app/config/packages配下に追加されます。  
publish to app/config/packages


views配下にsmartyファイルがあればそれをテンプレートと使用し、  
なければ通常通りbladeテンプレートかphpファイルを使用します。  

smartyテンプレート内にも*{{app_path()}}*等のヘルパーそのまま使用できます。  
その場合、delimiterをbladeと同じものを指定しない様にしてください。  
