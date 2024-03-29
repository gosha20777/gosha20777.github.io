---
layout: post
title:  "Что такое FAR и с чем его едят?"
date:   2017-03-13
image: posts/2017_03_13_logo.jpg
category: programs
---
<p class="intro"><span class="dropcap">М</span>еня много раз спрашивали, что за «синей страшной консолью» я пользуюсь, а люди по осведомленный удивленно отмечали: «Ты используешь far? Зачем весь total commander лучше!».</p>

<blockquote>Вот я и решил написать статью об этом великолепном файловом менеджере. На мой взгляд это лучший файловый менеджер!</blockquote>

### Небольшая инструкция.

Тут я приведу инструкцию необходимую для «прохождения начального порога». Другие тонкости и нюансы вы постепенно освоите сами. Новичка может смутить обилие сочетаний клавиш и команд. Но поверьте мне – вы быстро освоитесь, и работа с файлами будет происходить в десятки раз быстрее!

#### #1 Русификация. Подготовительные меры.

<a href="http://www.farmanager.com/download.php?l=ru">Качаем FAR</a>. При установке программы поставьте соответствующую галочку напротив русского языка. Когда FAR установлен жмем <F9> -> “Options” -> Languages и выбираем свой любимый `РУССКИЙ` язык. Локализация тут хорошая плеваться не придется.

<figure>
	<img src="{{ '/assets/img/posts/2017_03_13_00.jpg' | prepend: site.baseurl }}" alt=""> 
	<figcaption>Russian</figcaption>
</figure>

Далее жмем на иконку ФАРа в верхнем углу программы. Свойства -> шрифт. Тут мы можем настроить стандартный шрифт консоли. ФАР запомнит эти настройки для данного ярлыка. Вот мы уже коснулись одного из плюсов FARа. В каком менеджере вы сможете так легко изменить шрифт, цвета и пр? Но об этом потом.

#### #2 Основные команды и понятия.

В FARе есть две панели для работы с файлами. Для переключения между ними надо нажать кнопку TAB. Да ладно шучу! Это же IT блог, и я не буду мучать своих немногочисленных читателей дурацкий информацией. Просто приведу таблицы с командами.

<figure>
	<img src="{{ '/assets/img/posts/2017_03_13_01.jpg' | prepend: site.baseurl }}" alt=""> 
	<figcaption>командамы</figcaption>
</figure>

<figure>
	<img src="{{ '/assets/img/posts/2017_03_13_02.jpg' | prepend: site.baseurl }}" alt=""> 
	<figcaption>командамы</figcaption>
</figure>

<figure>
	<img src="{{ '/assets/img/posts/2017_03_13_03.jpg' | prepend: site.baseurl }}" alt=""> 
	<figcaption>командамы</figcaption>
</figure>

<figure>
	<img src="{{ '/assets/img/posts/2017_03_13_04.jpg' | prepend: site.baseurl }}" alt=""> 
	<figcaption>еще командамы</figcaption>
</figure>

<figure>
	<img src="{{ '/assets/img/posts/2017_03_13_05.jpg' | prepend: site.baseurl }}" alt=""> 
	<figcaption>да сколько можно!</figcaption>
</figure>

#### #3 Главное это ПЛАГИНЫ!

Да, `Александр Пушной` говорил правду. Вот <a href="http://farplugs.sourceforge.net/">этот</a> список незаменимых плагинов для FAR. А <a href="https://github.com/gosha20777/far_by_gosha20777/">тут</a> вы можете скачать мою портативную сборку FARа куда установлено несколько жизненно важных плагинов (только под Win64!). Эта сборка всегда со мной на флешке и не раз спасала мне жизнь).

### Чем так хорош FAR?

Наверное, первое – это <b>КОНСОЛЬ!</b> Да да именно она. На умирающий «винде» не всегда получится запустить Total Commander и уж тем более проводник. С FARом все гораздо проще. Вставили установочный диск в Windows, но секретарша говорит, что забыла скопировать важного ей МИМИМИшного котика? `Shift+F10` => святая консоль => `cd F:` => `far.EXE` и вуаля. Котик спасен, а секретарша прыгает от счастья. Да я признаюсь и сам порой забывал что то сохранить и ФАР спасал меня.

<b>Настраевоемость.</b> FAR очень гибок. Вы можете настроить практически все: от вариантов копирования/переноса файлов (FAR может копировать в обход системы) до внешнего вида.

<b>Root доступ.</b> FAR может делать в ПК практически все. Удалить файл и затереть кластер на диске – пожалуйста `ALT+DEL` и папа-прогремит (или дядя в пагонах) не узнают, что вы скачивали фильмы для взрослых:) Без регистрации и СМС как говорится. Легко можно просматривать/менять системные файлы, блокировать нежелательные процессы, просматривать сеть и многое другое.

<b>Мощный текстовый редактор.</b> Шестнадцатеричные дампы, программирование, и просто набор текста. С помощью пары плагинов можно расширить его возможности, и он станет лучше чем Notepad++! К примеру все мои статьи и этот сайт был написан в FARе.

<b>Плагины!</b> Для фара существует огромное количество расширений. От встроенного плеера (не плохой кстати, но я использую AIMP) до мощных сетевых снифферов и пр. Отдельного внимания заслуживает плагин с говорящим названием «пакетное переименование». Где еще вы сможете в два клика пронумеровать ваши любимые песни и удалить назойливое “zaicev.net”?

И последнее: <b>FAR абсолютно бесплатен и регулярно обновляется.</b>

### Заключение.

`FAR manager` – то что, на мой взгляд, должно быть у каждого на компе. По своему функционалу он приближаются к Операционной Системе. Это как разводной ключ при ремонте (и не только). Я надеюсь, что после этой статьи вы скачаете и попробуете FAR. Уверен вам понравится!

<a href="https://github.com/gosha20777/far_by_gosha20777/">Прикреплю еще и мою сборку FARа</a>.

### Дополнительная литература.

* <a href="http://lumpics.ru/how-to-use-far-manager/">FAR Manager: нюансы использования программы</a>
* <a href="https://www.youtube.com/watch?v=YCKbLzgto24">Видос про достоинства FAR</a>
* <a href="https://www.youtube.com/watch?v=k-wci8PSFKA">Годный видеоурок по FAR</a>