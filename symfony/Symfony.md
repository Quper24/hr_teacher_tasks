# Symfony

## Ваша задача
Вам необходимо описать решение задачи, что описана ниже (решать не обязательно), т.е. описать, что и как должно быть использовано для решения всех ее пунктов.
Например: Какие классы, какие подходы, какие компоненты фреймворка необходимо использовать. Возможно, предоставить конкретный порядок действий в некоторых сложных ситуациях. На какие нюансы необходимо будет обратить внимание студенту при решении этой задачи. Какие шаги для более оптимальной организации кода стоит предпринять для решения этой задачи. Советы, рекомендации, доп. ссылки при необходимости.

При этом, студент должен писать только backend код. Вопросами запуска приложения, его оформлением, версткой и js студент не занимается. Считаем, что все настроено и готово. Для реализации используюстся стандартные возможности фреймворка, там где это возможно, шаблонизация, создание сервисов, маршрутизация, валидация и т.д. При этом студент прошел все эти стандартные темы и может их использовать на практике.

# Описание задания для студента
Необходимо разработать новостной сайт с админкой. Для внешнего вида рекомендуется использовать фреймворк *bootstrap*, например можно взять [этот шаблон](https://github.com/StartBootstrap/startbootstrap-modern-business). Качество визуального исполнения не имеет значения.

## Состав страниц
- Главная - список новостей
- Детальная страница новости
- Административный раздел с новостями
- Страница авторизации

### Главная страница
На главной странице выводятся только опубликованные новости сайта в порядке убывания даты публикации с возможностью перейти на детальную страницу этой новости. 

### Детальная страница
Ссылка на детальную страницу формируется по символьному коду новости. На этой странице отображаются: Название новости, текст новости и дата публикации новости. Если новости не опубликована то вместо новости должна отобразиться 404 страница.

### Административный раздел
В административном разделе располагается список новостей и все страницы для управления статьями (реализуем простой CRUD). В административный раздел имеет доступ только авторизованный пользователь на сайте. Регистрация новых пользователей недоступна.

При создании и изменения новости осуществляется ее валидация. При возникновении ошибок должен быть выведен текст ошибок валидации. Правила валидации описаны в *Модели хранения данных*. Можно менять все поля, кроме даты создания и даты изменения.

### Авторизация
Выводится форма для авторизации с вводом email и пароля. Ссылки на регистрацию и восстановление пароля не отображаются. Администратор должен быть создан посредством *миграции*/*фикстуры*/*консольной команды* (выберите, что считаете удобным).

## Модель хранения данных

У новостей должны быть следующие поля:
- **название** - строка, не менее 3-х символов
- **символьный код** - уникальная строка
- **текст новости** - текст, не менее 5 символов
- **дата публикации** - дата со временем
- **дата создания** - дата со временем
- **дата изменения** - дата со временем

## Сервис Markdown преобразователь
Текст новости можно формировать в разметке **markdown**. Необходимо создать отдельный сервис `MarkdownConverterService`, который сконвертирует markdown в html, который можно отобразить на сайте. 

Сервис `MarkdownConverterService` должна иметь настройку, определяемую переменной окружения `MARKDOWN_DISABLE_BOLD` - заменять выделение жирным на выделение курсивом. По умолчанию `false`. Если эта опция установлена в `true`, то перед преобразованием происходит замена жирных выделителей на курсивные (заменяются две звездочки **\*\*** на одну **\***)
