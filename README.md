# Тестовое задание на должность backend-разработчика в [ISPsystem](https://www.ispsystem.ru)

Стек - python3<br> 
[Текст задания](https://drive.google.com/file/d/1WNlQlvxHQb0n-F2OuvqjSgsHDNatrJxF/view?usp=sharing)


## Итоговый обзор работы
Для выполнения задания рассматривались три различных варианта:
1) Использование команд <b>wget</b>, <b>tar</b>, <b>ls</b>, <b>rm</b> оболочки <b>bash</b>.<br> 
Так как микросервис предполагается портировать в docker-контейнер, то одним из рассматриваемых вариантов было использование bash-скриптов для выполнения      основого функцианала микросервиса (загрузка архива, распаковка, удаление).
2) Использование фреймворка [FastAPI](https://fastapi.tiangolo.com) для создания микросервиса.<br>
FastAPI - является самым простым и быстрым способом реализации RestAPI-приложений. 
3) Построение обработчика запросов на основе класса <b>BaseHTTPRequestHandler</b> из модуля <b>http.server</b> и реализация сервера на основе класса <b>TCPServer</b> модуля <b>socketserver</b>.</p>
<p>В итоге для реализации был выбран последний вариант. Так как из рассмотренных, первый слабо подходит для продакшена, второй вариант самый лучший для продакшена, но излишне функцианален для поставленной задачи. Третий же вариант представляется мне самым удобным.</p>
<p>В целом по заданию выполнены все пункты основной части, а так же 1-й, 4-й, 6-й из дополнительной части. Микросирвис является асинхронным (реализовано с помощью модуля <b>threading</b>) и состоит из 4-х исполняемых файлов: <b>download.py</b>, <b>my_server.py</b>, <b>main.py</b>, <b>json_pars.py</b>. Рассмотрим исполняемые файлы детальнее.</p>

### download.py
download.py содержит основной класс микросервиса DownloadMaster, который непосредственно и занимается загрузкой, распаковкой, удалением архивов, а так же показывает состояние на каждом этапе обработки архива. <br>
<p>Метод download() занимается непосредственно загрузкой архива по URL-адресу и его распаковкой. На вход метод получает URL-адрес архива, в результате работы записывает  в свойство status состояние downloading с указанием прогресса загрузки. Распаковка производится вызовом метода extract(). В случае получения исключения при загруке,  в свойство status записывается сообщение об исключении. Для работы метода использованы модуль requests, а для обработки исключений использован класс HTTPError из модуля requests.exceptions совместно с конструкцией try .. except.</p>
