---
layout: post
title:  "Собственный Git на Windows"
date:   2018-01-05
image: posts/2018_01_05_00.png
categories: tutorial
---
<p class="intro"><span class="dropcap">Н</span>у вот наступил <code>11111100010</code> год ии у меня появилось свободная минутка, чтобы написать тут что-то полезное:-)</p>

<blockquote>Случилось так, что понадобился приватный  <b>git</b> репозиторий, а покупать VIP аккаунт на github не хотелось, да и политика безопасности компании, для которой разрабатывается проект, не позволяет это делать. По этому было принято решение о развертывании собственного git-сервера. Так как я <b>C# developer</b>, то речь пойдет конечно же о <b>Windows Server</b> и <b>IIS Server</b>. Пользователям Linux скажу, что там установка этого "богатства" еще проще и состоит из пары команд в терминале.</blockquote>

### Немного о платформе.

Данный `git-server` был написан на `C#` на `ASP.NET` и представляет собой Web приложение. Все исходные коды доступны <a href="https://github.com/jakubgarfield/Bonobo-Git-Server">тут</a>. Все желающие могут ознакомиться и оценить <strike>кривизну</strike> кода) А мы поехали дальше -)

### Как его ставить?

Для успешной установки нам нужны

 1. Сам сервер на *Windows Server 2008 R2/2012/2012 R2/2016* (кто-то сидит на ней?)
 2. Internet Information Services (IIS) 7 или 8
 3. <a href="https://www.microsoft.com/en-gb/download/details.aspx?id=48130">.NET Framework 4.6</a>
 4. visual redist 2012/2015 и CLR
 5. <a href="https://bonobogitserver.com/Git">Server дистрибутив</a>

Быстро пробежимся по основным пунктам. У меня стоит Windows Server 2012 R2. И показывать я буду на ней. Для Windows Server 2008 все примерно также. Предполагается, что Виндасервер у вас сконфигурирован и настроен. Если это не так – идите к   <a href="https://msdn.microsoft.com/ru-ru/library/hh801901(v=ws.11).aspx">документации</a>)

#### IIS Сервер + .NET Framework.

Запускаем ***Server Manager*** (диспетчер серверов) -> ***Manage*** (Управление) -> Add Roles and Features (Добавить роли и компоненты) …

<figure>
	<img src="{{ '/assets/img/posts/2018_01_05_01.JPG' | prepend: site.baseurl }}" alt=""> 
	<figcaption>да да у меня виндосервер на русском...</figcaption>
</figure>

Выбрать ***Role-based or Feature-based Installation*** (установка ролей или компонентов)

Далее выбираем наш сервер

<figure>
	<img src="{{ '/assets/img/posts/2018_01_05_02.JPG' | prepend: site.baseurl }}" alt=""> 
	<figcaption>...</figcaption>
</figure>

В ролях выбираем ***Web Server (IIS)***.

<figure>
	<img src="{{ '/assets/img/posts/2018_01_05_03.JPG' | prepend: site.baseurl }}" alt=""> 
	<figcaption>...</figcaption>
</figure>

В компонентах жмякаем на ***.NET framework 4.5*** и на последнем шаге выбираем нужные настройки.

Установка… Потребует перезагрузки сервера. Загружаем <a href="https://www.microsoft.com/en-gb/download/details.aspx?id=48130">.NET Framework 4.6</a> и ставим его. Все теперь можно ребутиться.

Для любителей консоли...

{% highlight bash%}
Start /w pkgmgr /iu:IIS-WebServerRole;
IIS-WebServer;
IIS-CommonHttpFeatures;
IIS-StaticContent;
IIS-DefaultDocument;
IIS-DirectoryBrowsing;
IIS-HttpErrors;
IIS-HealthAndDiagnostics;
IIS-HttpLogging;
IIS-LoggingLibraries;
IIS-RequestMonitor;
IIS-Security;
IIS-RequestFiltering;
IIS-HttpCompressionStatic;
IIS-WebServerManagementTools;
IIS-ManagementConsole;
WAS-WindowsActivationService;
WAS-ProcessModel;
WAS-NetFxEnvironment;
WAS-ConfigurationAPI
{% endhighlight %}

#### Git Server

Всё, теперь можно перейти к непосредственно развёртыванию git сервера. Разархивируем содержимое <a href="https://bonobogitserver.com/Git">дистрибутива</a> в `wwwroot` IIS-сервера (`C:\inetpub\wwwroot`) и даём права учетной записи `IIS_IUSERS` на модификацию каталога `App_Data`.

<figure>
	<img src="{{ '/assets/img/posts/2018_01_05_05.png' | prepend: site.baseurl }}" alt=""> 
	<figcaption>...</figcaption>
</figure>

Запускаем **IIS Manager** и конвертируем Git в приложение.

<figure>
	<img src="{{ '/assets/img/posts/2018_01_05_06.png' | prepend: site.baseurl }}" alt=""> 
	<figcaption>...</figcaption>
</figure>

После конвертации жмем **Action** – **Browse** (Управление приложением – обзор) и у нас должен открыться сайтик с формой для входа. Теперь он доступен по адресу `IP сервера\git` в локальной сети. При желании его можно вывезти во внешнюю сеть и вообще делать с ним все что душе угодно!

### Настройка.

По стандарту логин пароль для входа **admin\admin**.

<figure>
	<img src="{{ '/assets/img/posts/2018_01_05_07.png' | prepend: site.baseurl }}" alt=""> 
	<figcaption>...</figcaption>
</figure>

В настройках можно указать другой путь для хранения файлов, изменить язык и вообще сделать много полезного)

<figure>
	<img src="{{ '/assets/img/posts/2018_01_05_04.JPG' | prepend: site.baseurl }}" alt=""> 
	<figcaption></figcaption>
</figure>

Можно добавлять новых пользователей и осуществлять контроль видимости репозиториев, выдавать исключительные права пользователям. Также можно объединять пользователей в команды и управлять ими. На пример команде `Core Developers` будут доступны **все ветки** в репозитории, а команде `Testers` только ветка **Master**.

#### P.s.

Я надеюсь данная статья была полезна для вас. Ставьте Like за встроенный редактор кода и подсветку синтаксиса))) Приятного кодинга!
