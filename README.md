# django_test
勉強用

## 手順
`docker-compse.yml`が置かれているディレクトリで下記を実行
`docker-compose up -d`

`docker container ls`
コンテナの確認

`docker container exec -it {CONTAINER_ID | CONTAINER NAME} django-admin startproject {PROJECT_NAME}`
PROJECT_NAMEには半角英数字でプロジェクト名を設定

作成されたプロジェクトディレクトリ内 
`{PROJECT_NAME}/{PROJECT_NAME}/settings.py`の各設定を変更

### DATABASES
```
DATABASES = {
    'default': {
    'ENGINE': 'django.db.backends.postgresql',
    'NAME': 'postgres',
    'USER': 'postgres',
    'HOST': 'db',
    'PORT': 5432,
  }
}
```


### ALLOWED_HOSTS
```
ALLOWED_HOSTS = ['localhost', '192.168.33.15', '[::1]']
```

または特に設定しない場合は
```
ALLOWED_HOSTS = ['*']
```

### Djangoプロジェクト起動
`docker container exec -it {CONTAINER_ID | CONTAINER NAME} python {PROJECT_NAME}/manage.py runserver 0.0.0.0:8000`


### アクセス
`ALLOWED_HOSTS`で設定したIPと
PORTは`docker-compose.yml`で設定してあるもの（今回は8000）でアクセス
`http://192.168.33.15:8000`

### コンテナ停止
`docker stop {CONTAINER_ID | CONTAINER_NAME}`

### コンテナ起動
`docker start {CONTAINER_ID | CONTAINER_NAME}`

### 2つのコンテナを一括起動・停止・操作
起動
`docker-compose start`

停止
`docker-compose stop`

再起動
`docker-compose restart`

### アプリケーション作成
下記コマンドで`manage.py`と同階層に`polls`ディレクトリと関連ファイルが生成

プロジェクトディレクトリに移動（manage.pyと同階層）`cd {PROJECT_NAME}`

アプリ作成`docker exec -it {CONTAINER ID | CONTAINER_NAME} python manage.py startapp polls`

### 参照サイト
https://hodalog.com/run-django-app-using-docker-compose/
