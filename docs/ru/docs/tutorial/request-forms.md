# Данные формы

Когда вам нужно получить поля формы вместо JSON, вы можете использовать `Form`.

/// info | Дополнительная информация

Чтобы использовать формы, сначала установите <a href="https://github.com/Kludex/python-multipart" class="external-link" target="_blank">`python-multipart`</a>.

Например, выполните команду `pip install python-multipart`.

///

## Импорт `Form`

Импортируйте `Form` из `fastapi`:

{* ../../docs_src/request_forms/tutorial001_an_py39.py hl[3] *}

## Определение параметров `Form`

Создайте параметры формы так же, как это делается для `Body` или `Query`:

{* ../../docs_src/request_forms/tutorial001_an_py39.py hl[9] *}

Например, в одном из способов использования спецификации OAuth2 (называемом "потоком пароля") требуется отправить `username` и `password` в виде полей формы.

Данный способ требует отправку данных для авторизации посредством формы (а не JSON) и обязательного наличия в форме строго именованных полей  `username` и `password`.

Вы можете настроить `Form` точно так же, как настраиваете и  `Body` ( `Query`, `Path`, `Cookie`), включая валидации, примеры, псевдонимы (например, `user-name` вместо `username`) и т.д.

/// info | Дополнительная информация

`Form` - это класс, который наследуется непосредственно от `Body`.

///

/// tip | Подсказка

Вам необходимо явно указывать параметр `Form` при объявлении каждого поля, иначе поля будут интерпретироваться как параметры запроса или параметры тела (JSON).

///

## О "полях формы"

Обычно способ, которым HTML-формы (`<form></form>`) отправляют данные на сервер, использует "специальное" кодирование для этих данных, отличное от JSON.

**FastAPI** гарантирует правильное чтение этих данных из соответствующего места, а не из JSON.

/// note | Технические детали

Данные из форм обычно кодируются с использованием "типа медиа" `application/x-www-form-urlencoded`.

Но когда форма содержит файлы, она кодируется как `multipart/form-data`. Вы узнаете о работе с файлами в следующей главе.

Если вы хотите узнать больше про кодировки и поля формы, ознакомьтесь с <a href="https://developer.mozilla.org/ru/docs/Web/HTTP/Methods/POST" class="external-link" target="_blank">документацией <abbr title="Mozilla Developer Network">MDN</abbr> для `POST` на веб-сайте</a>.

///

/// warning | Предупреждение

Вы можете объявлять несколько параметров `Form` в *операции пути*, но вы не можете одновременно с этим объявлять поля `Body`, которые вы ожидаете получить в виде JSON, так как запрос будет иметь тело, закодированное с использованием `application/x-www-form-urlencoded`, а не `application/json`.

Это не ограничение **FastAPI**, это часть протокола HTTP.

///

## Резюме

Используйте `Form` для объявления входных параметров данных формы.