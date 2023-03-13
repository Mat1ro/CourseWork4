# Coursework_4

## Запуск из docker

1. Скачать и установить [docker](https://docs.docker.com/engine/install/)
2. Скачать образ командой `docker pull painassasin/node_cource_project:latest`
3. Запустить контейнер на 80 порту `docker run -p 80:80 painassasin/node_cource_project`

>Образ сконфигурирован таким образом, что он будет ожидать 
> backend на 5000 локальном порту
 
>Чтобы все корректно работало, нам нужно в проект установить еще один пакет
```python

from flask import Flask
from flask_cors import CORS
from flask_restx import Api

from config import Config
from setup_db import db

api = Api(doc='/docs')


def create_app():
    app = Flask(__name__)
    app.config.from_object(get_config(Config))

    db.init_app(app)
    api.init_app(app)

app = create_app(Config())
CORS(app)
```