> [Главная](README.md)  /  Broken Authentication and Session Management

### <a id="about"></a> [Что такое  Broken Authentication and Session Management](#about)
Суть уязвимости заключается в том, что были допущены ошибки в архитектуре аутентификации и управления сессиями.

### <a id='vulnerable'></a> [Как определить что приложение уязвимо](#vulnerable)
* Данные аутентификации пользователя хранятся в незащищенном виде?
* Критичная информация может быть выдана через слабые функции управления аккаунтом (восстановление пароля, регистрация, слабые сессии)?
* Id сессии передается в URL?
* Id сессии подвержены атаке фиксации?
* Id сессии не имеет таймаута либо удаляется только на стороне пользователя?
* Сессия не обновляется после успешного логина?
* Пароли, сессии, и прочая критичная информация передается по открытому каналу?



### <a id='example'></a> [Пример уязвимости](#example)
#### Пример 1
Приложение умеет обрабатывать id сессии либо записывает их в get параметрах  `http://example.com/sale/saleitems?sessionid=268544541`
Таким образом поделившись ссылкой пользователь автоматически авторизовывет от своего имени всех кто по ней перейдет.
Злоумышленник может выставить пользователю известный ему id сессии и затем получить доступ к его аккаунту

#### Пример 2
Приложение не контролирует время жизни сессии.
Пользователь зашел на сайт с публичной точки доступа и авторизовался на нем. Но вместо того чтобы нажать «выйти» пользователь просто закрыл вкладку и ушел. Таким образом следующий кто зайдет на сайт с этой точки доступа будет авторизован от имени первого пользователя.

#### Пример 3
Злоумышленник получил доступ к БД в которой хранятся все пароли и логины пользователей в открытом виде.
Таким образом он получил все на блюдечке с голубой каемочкой. 


### <a id="protection"></a> [Защита](#protection)
* Необходимо защитить сайт от XSS
* Использовать надежную систему авторизации учитывая пункты на слайде «Как определить что приложение уязвимо»
* Соблюдать стандарты «[OWASP’s Application Security Verification Standard](https://www.owasp.org/index.php/ASVS)» ((ASVS) areas V2 (Authentication) and V3 (Session Management))
* Использовать простые интерфейсы для разработчиков