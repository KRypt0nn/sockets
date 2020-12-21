<h1 align="center">🚀 Sockets</h1>

**sockets** - небольшая библиотека для работы с сокетами на PHP 7.4+

## Установка

```
composer require observer/sockets
```

## Пример работы

Клиент:

```php
<?php

use Observer\Sockets\SocketClient as Client;

$client = new Client;
$client->connect ('127.0.0.1', 53874);

while (true)
    $client->send (readline ('> '));
```

Сервер:

```php
<?php

use Observer\Sockets\SocketListener as Listener;

$listener = new Listener (53874);

$i = 0;
$client = $listener->acceptAsync()->call(function () use (&$i)
{
    if (++$i == 10)
        return false;
    
    echo 'Waiting for connections... ('. $i .')' . PHP_EOL;
    sleep (1);

    return true;
});

if ($client === null)
    die ('Client not connected');

echo 'Client connected'. PHP_EOL;

while (true)
{
    foreach ($client->read () as $message)
        echo '> '. $message . PHP_EOL;

    sleep (1);
}
```

Автор: [Подвирный Никита](https://vk.com/technomindlp). Специально для [Enfesto Studio Group](https://vk.com/hphp_convertation)
