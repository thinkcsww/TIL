									**PHP Firebase composer 설치**

------

1. AWS 서버를 만든 후 터미널로 접속하여 초기 세팅을 한다.

   ```
    sudo yum update -y // Complete! 메시지가 확인된다.
    sudo yum install -y httpd24 php71 php71-mbstring// Complete! 메시지가 확인된다.
    sudo service httpd start // ok 메시지가 확인된다.
   ```

   php 설치 후 php.ini로 들어가서 extension을 추가해 준다.

   ```
   sudo vi /etc/php.ini -> extension=mbstring.so
   ```

2. composer를 설치한다

   ```
   cd ~
   $ sudo curl -sS https://getcomposer.org/installer | sudo php
   $ sudo mv composer.phar /usr/local/bin/composer
   $ sudo ln -s /usr/local/bin/composer /usr/bin/compose
   ```

파이어 베이스 링크에 들어간다.<https://firebase-php.readthedocs.io/en/latest/overview.html>

3.  composer를 이용하여 파이어베이스를 설치한다

```
composer require kreait/firebase-php ^4.18
```

4. 파이어베이스 콘솔로 이동하여 해당 프로젝트의 설정에서 사용자 및 권한을 클릭 -> 서비스 계정 클릭 -> Google cloud platform의 서비스 계정.. 클릭 -> GCP 페이지가 나온다 
5. 계정 이름 중 App Engine default service account 의 옆에 액션 버튼 -> 키 만들기 -> json -> 선택하여 다운로드 받은 json 파일을 aws의 폴더에 secret이라는 폴더 이름을 만들어서 추가한다.
6. 마지막으로 index.php를 다음과 같이 꾸민다.

```
<?php

require_once './vendor/autoload.php';

use Kreait\Firebase\Factory;
use Kreait\Firebase\ServiceAccount;

// 경로를 /secret/json파일이름 으로 바꾼다
$serviceAccount = ServiceAccount::fromJsonFile(__DIR__.'/secret/capstone-d26ae-0a5802d0c607.json');

$firebase = (new Factory)
    ->withServiceAccount($serviceAccount)
    ->create();

$database = $firebase->getDatabase();


```

