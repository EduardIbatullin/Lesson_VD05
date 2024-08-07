# Lesson_VD05. Работа с шаблонизатором и HTML шаблоны.

# Описание веб-приложения "Dune Movie Info"

## Стек технологий

- **Flask** - микрофреймворк на Python для создания веб-приложений.
- **Jinja** - шаблонизатор для Python, используемый в Flask для генерации HTML.
- **Bootstrap** - популярный CSS-фреймворк для создания адаптивных и привлекательных веб-страниц.

## Структура приложения

### Файловая структура

```plaintext
dune_movie_info/
├── app.py
├── templates/
│   ├── base.html
│   ├── home.html
│   └── about.html
├── static/
│   ├── css/
│   │   └── styles.css
│   ├── js/
│   │   └── scripts.js
│   └── images/
│       ├── timothee-actor.jpg
│       ├── paul-character.jpg
│       ├── rebecca-actor.jpg
│       ├── jessica-character.jpg
│       ├── oscar-actor.jpg
│       ├── duke-character.jpg
│       ├── josh-actor.jpg
│       ├── gurney-character.jpg
│       ├── stellan-actor.jpg
│       ├── baron-character.jpg
│       ├── dave-actor.jpg
│       ├── rabban-character.jpg
│       ├── zendaya-actor.jpg
│       ├── chani-character.jpg
│       ├── jason-actor.jpg
│       ├── duncan-character.jpg
│       └── javier-actor.jpg
│       └── stilgar-character.jpg
└── requirements.txt
```

### `app.py`

Основной файл приложения, содержащий настройку Flask и маршруты для страниц.

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('home.html')

@app.route('/about')
def about():
    return render_template('about.html')

if __name__ == '__main__':
    app.run(debug=True)
```

### Шаблоны

#### `base.html`

Базовый шаблон, который используется для всех страниц. Содержит общий HTML-каркас, включая заголовок, подключение Bootstrap и стили.

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Фильм Дюна{% endblock %}</title>
    <!-- Bootstrap CSS -->
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    {% block extra_css %}{% endblock %}
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="/">Главная</a>
        <div class="collapse navbar-collapse">
            <ul class="navbar-nav">
                <li class="nav-item">
                    <a class="nav-link" href="/about">О фильме</a>
                </li>
            </ul>
        </div>
    </nav>
    <div class="container">
        {% block content %}
        {% endblock %}
    </div>
    <footer class="footer bg-light mt-auto py-3">
        <div class="container text-center">
            <span class="text-muted">&copy; 2024 Dune Movie Info. Все права защищены.</span>
        </div>
    </footer>
    <!-- Bootstrap JS and dependencies -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.5.4/dist/umd/popper.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
    {% block extra_js %}{% endblock %}
</body>
</html>
```

#### `home.html`

Главная страница, расширяющая `base.html`.

```html
{% extends "base.html" %}

{% block title %}Дюна - Главная{% endblock %}

{% block content %}
    <h1 class="mt-5">Добро пожаловать на страницу фильма "Дюна"!</h1>
    <p class="lead">"Дюна" - это эпический научно-фантастический фильм 2021 года, режиссера Дени Вильнёва.</p>
    <img src="../static/image/dune-poster.jpg" class="img-fluid" alt="Постер Дюны">
    <p class="mt-4">Фильм является адаптацией одноименного романа Фрэнка Герберта 1965 года. Это первая часть из двух частей адаптации, охватывающая примерно первую половину книги. Действие происходит в далеком будущем, история рассказывает о Поле Атрейдесе, чья семья принимает управление пустынной планетой Арракис. Арракис является единственным источником самого ценного вещества во вселенной, "пряности", контроль над которой является предметом ожесточенной борьбы среди благородных семей. После предательства Пол должен отправиться в пустыню, чтобы найти Фременов, коренных жителей планеты, которые станут ключевыми для его выживания.</p>
{% endblock %}
```

#### `about.html`

Страница "О фильме", расширяющая `base.html`. Содержит карточки с актерами и их персонажами в виде слайдов.

```html
{% extends "base.html" %}

{% block title %}Дюна - О фильме{% endblock %}

{% block content %}
    <h1 class="mt-5">О фильме "Дюна"</h1>
    <p class="lead">"Дюна" - это фильм 2021 года, режиссера Дени Вильнёва, основанный на романе Фрэнка Герберта 1965 года.</p>
    <h2>Краткое содержание</h2>
    <p>Действие происходит в далеком будущем, в огромной межзвездной империи. "Дюна" рассказывает историю молодого Пола Атрейдеса, чья благородная семья принимает управление пустынной планетой Арракис. Арракис является единственным источником меланжа, или "пряности", наркотика, который продлевает жизнь и повышает умственные способности. Он также необходим для навигации в космосе, требующей некоего многомерного восприятия и предвидения, которое обеспечивает пряность. В то время как фракции борются за контроль над Арракисом, Полу предстоит справляться с политическими интригами и выживать в враждебной пустынной среде.</p>

    <h2>Актерский состав</h2>
    <div class="row">
        <div class="col-md-4">
            <div class="card mb-4">
                <div id="carouselTimothee" class="carousel slide" data-ride="carousel">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img src="../static/image/timothee-actor.jpg" class="d-block w-100" alt="Тимоти Шаламе">
                        </div>
                        <div class="carousel-item">
                            <img src="../static/image/paul-character.jpg" class="d-block w-100" alt="Пол Атрейдес">
                        </div>
                    </div>
                    <a class="carousel-control-prev" href="#carouselTimothee" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#carouselTimothee" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                    </a>
                </div>
                <div class="card-body">
                    <h5 class="card-title">Тимоти Шаламе</h5>
                    <p class="card-text">Пол Атрейдес</p>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="card mb-4">
                <div id="carouselRebecca" class="carousel slide" data-ride="carousel">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img src="../static/image/rebecca-actor.jpg" class="d-block w-100" alt="Ребекка Фергюсон">
                        </div>
                        <div class="carousel-item">
                            <img src="../static/image/jessica-character.jpg" class="d-block w-100" alt="Леди Джессика">
                        </div>
                    </div>
                    <a class="carousel-control-prev" href="#carouselRebecca" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#carouselRebecca" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                    </a>
                </div>
                <div class="card-body">
                    <h5 class="card-title">Ребекка Фергюсон</h5>
                    <p class="card-text">Леди Джессика</p>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="card mb-4">
                <div id="carouselOscar" class="carousel slide" data-ride="carousel">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img src="../static/image/oscar-actor.jpg" class="d-block w-100" alt="Оскар Айзек">
                        </div>
                        <div class="carousel-item">
                            <img src="../static/image/duke-character.jpg" class="d-block w-100" alt="Герцог Лето Атрейдес">
                        </div>
                    </div>
                    <a class="carousel-control-prev" href="#carouselOscar" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#carouselOscar" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                    </a>
                </div>
                <div class="card-body">
                    <h5 class="card-title">Оскар Айзек</h5>
                    <p class="card-text">Герцог Лето Атрейдес</p>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="card mb-4">
                <div id="carouselJosh" class="carousel slide" data-ride="carousel">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img src="../static/image/josh-actor.jpg" class="d-block w-100" alt="Джош Бролин">
                        </div>
                        <div class="carousel-item">
                            <img src="../static/image/gurney-character.jpg" class="d-block w-100" alt="Гурни Халлек">
                        </div>
                    </div>
                    <a class="carousel-control-prev" href="#carouselJosh" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#carouselJosh" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                    </a>
                </div>
                <div class="card-body">
                    <h5 class="card-title">Джош Бролин</h5>
                    <p class="card-text">Гурни Халлек</p>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="card mb-4">
                <div id="carouselStellan" class="carousel slide" data-ride="carousel">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img src="../static/image/stellan-actor.jpg" class="d-block w-100" alt="Стеллан Скарсгард">
                        </div>
                        <div class="carousel-item">
                            <img src="../static/image/baron-character.jpg" class="d-block w-100" alt="Барон Владимир Харконнен">
                        </div>
                    </div>
                    <a class="carousel-control-prev" href="#carouselStellan" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#carouselStellan" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                    </a>
                </div>
                <div class="card-body">
                    <h5 class="card-title">Стеллан Скарсгард</h5>
                    <p class="card-text">Барон Владимир Харконнен</p>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="card mb-4">
                <div id="carouselDave" class="carousel slide" data-ride="carousel">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img src="../static/image/dave-actor.jpg" class="d-block w-100" alt="Дэйв Батиста">
                        </div>
                        <div class="carousel-item">
                            <img src="../static/image/rabban-character.jpg" class="d-block w-100" alt="Глоссу Раббан">
                        </div>
                    </div>
                    <a class="carousel-control-prev" href="#carouselDave" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#carouselDave" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                    </a>
                </div>
                <div class="card-body">
                    <h5 class="card-title">Дэйв Батиста</h5>
                    <p class="card-text">Глоссу Раббан</p>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="card mb-4">
                <div id="carouselZendaya" class="carousel slide" data-ride="carousel">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img src="../static/image/zendaya-actor.jpg" class="d-block w-100" alt="Зендея">
                        </div>
                        <div class="carousel-item">
                            <img src="../static/image/chani-character.jpg" class="d-block w-100" alt="Чани">
                        </div>
                    </div>
                    <a class="carousel-control-prev" href="#carouselZendaya" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#carouselZendaya" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                    </a>
                </div>
                <div class="card-body">
                    <h5 class="card-title">Зендея</h5>
                    <p class="card-text">Чани</p>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="card mb-4">
                <div id="carouselJason" class="carousel slide" data-ride="carousel">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img src="../static/image/jason-actor.jpg" class="d-block w-100" alt="Джейсон Момоа">
                        </div>
                        <div class="carousel-item">
                            <img src="../static/image/duncan-character.jpg" class="d-block w-100" alt="Дункан Айдахо">
                        </div>
                    </div>
                    <a class="carousel-control-prev" href="#carouselJason" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#carouselJason" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                    </a>
                </div>
                <div class="card-body">
                    <h5 class="card-title">Джейсон Момоа</h5>
                    <p class="card-text">Дункан Айдахо</p>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="card mb-4">
                <div id="carouselJavier" class="carousel slide" data-ride="carousel">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img src="../static/image/javier-actor.jpg" class="d-block w-100" alt="Хавьер Бардем">
                        </div>
                        <div class="carousel-item">
                            <img src="../static/image/stilgar-character.jpg" class="d-block w-100" alt="Стилгар">
                        </div>
                    </div>
                    <a class="carousel-control-prev" href="#carouselJavier" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#carouselJavier" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                    </a>
                </div>
                <div class="card-body">
                    <h5 class="card-title">Хавьер Бардем</h5>
                    <p class="card-text">Стилгар</p>
                </div>
            </div>
        </div>
    </div>

    <h2>Видение режиссера</h2>
    <p>Дени Вильнёв стремился создать верную адаптацию романа Герберта, одновременно сделав историю доступной для современной аудитории. Он сосредоточился на визуальных и тематических элементах пустынной планеты Арракис и политических и социальных сложностях вселенной, созданной Гербертом.</p>
{% endblock %}
```

### Статические файлы

#### `styles.css`

Дополнительные стили для улучшения внешнего вида приложения.

```css
/* styles.css */
body {
    padding-top: 56px;
}

.footer {
    position: fixed;
    bottom: 0;
    width: 100%;
}
```

#### `scripts.js`

JavaScript-файл для дополнительных скриптов (если потребуется).

```javascript
// scripts.js
// Дополнительные скрипты
```

### `requirements.txt`

Список зависимостей для установки через `pip`.

```
Flask==2.0.1
```

## Запуск приложения

1. Установите зависимости:

    ```bash
    pip install -r requirements.txt
    ```

2. Запустите приложение:

    ```bash
    python app.py
    ```

3. Откройте браузер и перейдите по адресу [http://127.0.0.1:5000/](http://127.0.0.1:5000/) для просмотра приложения.

## Заключение

Это веб-приложение предоставляет информацию о фильме "Дюна", используя Flask, Jinja и Bootstrap для создания красивого и удобного интерфейса. Оно включает главную страницу с общим описанием и страницу "О фильме" с подробной информацией и карточками актёров, выполненными в виде слайдов.
 
