<h1 align="center">flysystem-oss </h1>

<p align="center">:floppy_disk:  Flysystem adapter for the oss storage.</p>

<p align="center">
<a href="https://github.com/iiDestiny/flysystem-oss"><img src="https://travis-ci.org/iiDestiny/flysystem-oss.svg?branch=master"></a>
<a href="https://github.com/iiDestiny/flysystem-oss"><img src="https://github.styleci.io/repos/163501119/shield"></a>
<a href="https://github.com/iiDestiny/flysystem-oss"><img src="https://poser.pugx.org/iidestiny/flysystem-oss/v/stable.svg"></a>
<a href="https://github.com/iiDestiny/flysystem-oss"><img src="https://poser.pugx.org/iidestiny/flysystem-oss/v/unstable.svg"></a>
<a href="https://github.com/iiDestiny/flysystem-oss"><img src="https://poser.pugx.org/iidestiny/flysystem-oss/downloads"></a>
<a href="https://scrutinizer-ci.com/g/iiDestiny/flysystem-oss/?branch=master"><img src="https://scrutinizer-ci.com/g/iiDestiny/flysystem-oss/badges/quality-score.png?b=master"></a>
<a href="https://github.com/iiDestiny/flysystem-oss"><img src="https://poser.pugx.org/iidestiny/flysystem-oss/license"></a>

</p>

## Requirement

- PHP >= 7.0

## Installation

```shell
$ composer require "iidestiny/flysystem-oss" -vvv
```

## Usage

```php
use League\Flysystem\Filesystem;
use Iidestiny\Flysystem\Oss\OssAdapter;
use Iidestiny\Flysystem\Oss\Plugins\FileUrl;

$accessKeyId = 'xxxxxx';
$accessKeySecret = 'xxxxxx';
$endpoint= 'oss.iidestiny.com';
$bucket = 'bucket';
$isCName = true; // 如果 isCname 为 false，endpoint 应配置 oss 提供的域名如：`oss-cn-beijing.aliyuncs.com`，cname 或 cdn 请自行到阿里 oss 后台配置并绑定 bucket

$adapter = new OssAdapter($accessKeyId, $accessKeySecret, $endpoint, $bucket, $isCName);

$flysystem = new Filesystem($adapter);

```

## API

```php
bool $flysystem->write('file.md', 'contents');

bool $flysystem->write('file.md', 'http://httpbin.org/robots.txt', ['options' => ['xxxxx' => 'application/redirect302']]);

bool $flysystem->writeStream('file.md', fopen('path/to/your/local/file.jpg', 'r'));

bool $flysystem->update('file.md', 'new contents');

bool $flysystem->updateStream('file.md', fopen('path/to/your/local/file.jpg', 'r'));

bool $flysystem->rename('foo.md', 'bar.md');

bool $flysystem->copy('foo.md', 'foo2.md');

bool $flysystem->delete('file.md');

bool $flysystem->has('file.md');

string|false $flysystem->read('file.md');

array $flysystem->listContents();

array $flysystem->getMetadata('file.md');

int $flysystem->getSize('file.md');

string $flysystem->getAdapter()->getUrl('file.md'); 

string $flysystem->getMimetype('file.md');

int $flysystem->getTimestamp('file.md');
```

## Plugins

Get oss file visit url

```php
use Iidestiny\Flysystem\Oss\Plugins\FileUrl

$flysystem->addPlugin(new FileUrl());

string $flysystem->getUrl('file.md');
```

## Integration

- Laravel 5：[iidestiny/laravel-filesystem-oss](https://github.com/iiDestiny/laravel-filesystem-oss)

## reference

- [overtrue/flysystem-qiniu](https://github.com/overtrue/flysystem-qiniu)

## License

MIT