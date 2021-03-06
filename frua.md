> [Главная](README.md)  / Failure to Restrict URL Access 

### <a id="about"></a> [Что такое Failure to Restrict URL Access](#about)
Приложение не проверят права доступа к разным частям сайта. Создатель приложения надеется что никто не сможет угадать его мега секретный url в админку (/nimda) и поэтому счел ненужным делать там авторизацию.

### <a id='vulnerable'></a> [Как определить что приложение уязвимо](#vulnerable)
* Приложение требует авторизации при попытке доступа к чувствительным страницам (напр админка)?
* Любой авторизованый пользователь может получить доступ к этим страницам?
* Проверяются ли права при попытке доступа к этим страницам?

### <a id='example'></a> [Примеры уязвимости](#example)
Разработчик создал «скрытую» от посторонних глаз страницу, на которой может управлять состоянием приложения (админка) и при этом счел что раз никто не знает что она лежит по адресу /mySuperMegaAdminPanel то никто в неё и не попадет.
Вот только современные браузеры (привет google) и системы аналитики (я.метрика) отправляют родителям все страницы на индекс, таким образом ссылка на админку может попасть в поисковые системы.
Ну и никто не отменял хранимый xss, встроил картинку и смотришь по логам httpReferer.

### <a id="protection"></a> [Защита](#protection)
* Использовать RBAC (role based access control)
* Политики RBAC`а должны быть конфигурируемыми чтобы избежать хардкода
* По умолчанию считать что у пользователя нет прав для доступа к странице (система белого списка — white list).