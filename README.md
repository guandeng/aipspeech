#### AipSpeech
百度语音合成可将文字信息转化为声音信息

#### Install
```
composer require "guandeng/aipspeech"
```
publish config

1、在 config/app.php 注册 ServiceProvider 和 Facade (Laravel 5.5 + 无需手动注册)
```
'providers' => [
    // ...
    Overtrue\LaravelWeChat\ServiceProvider::class,
],
```
2、创建配置文件
```
php artisan vendor:publish --provider="Guandeng\Aipspeech\AipSpeechProvider"
```

##### Lumen 应用
1、在 bootstrap/app.php
```
$app->register(Guandeng\Aipspeech\AipSpeechProvider::class);
```

#### Usage
在.env加上你的开发秘钥
```
BAIDU_APP_ID=******
BAIDU_APP_KEY=******
BAIDU_SECRET_KEY =******
```

```
<?php

    $app_id = config('aipspeech.app_id');
    $app_key = config('aipspeech.app_key');
    $secret_key = config('aipspeech.secret_key');
    $client = new AipSpeech($app_id, $app_key, $secret_key);
    $result = $client->synthesis('你好百度。', 'zh', 1, array(
        'vol' => 5,
    ));
// 识别正确返回语音二进制 错误则返回json 参照下面错误码
if(!is_array($result)){
    file_put_contents('audio.mp3', $result);
}
```
详情请参考[百度文档](https://ai.baidu.com/ai-doc/SPEECH/wk38y8og2)
