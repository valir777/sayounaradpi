byedpi для mac os<br>

запускаем launch и вводим флаги для запуска<br>

пример:
```
--split 1 --split 8+s --disoob 1 --tlsrec 6
```

------
### описание флагов
```
--split значение
    разбить запрос по указанной позиции
    позиция имеет вид offset[:repeats:skip][+flag1[flag2]]
    флаги:
        +s: добавить смещение sni
        +h: добавить смещение host
        +n: нулевое смещение
    дополнительные флаги:
        +e: конец 
        +m: середина
    Примеры: 
        0+sm - разбить запрос в середине sni
        1:3:5 - разбить по позициям 1,6,11
    ключ можно указывать несколько раз,чтобы разбить запрос по нескольким позициям
    если offset отрицательный и не имеет флагов,то к нему прибавляется размер пакета

--disorder значение
    подобен --split,но части отправляются в обратном порядке
    
--oob значение
    подобен --split,но часть отсылается как OOB данные
    
--disoob значение
    подобен --disorder,но часть отсылается как OOB данные

--tlsrec значение
    разделить clienthello на отдельные записи по указанному смещению
    можно указывать несколько раз

--mod-http <h[,d,r]>
    всякие манипуляции с http пакетом,можно комбинировать
    hcsmix:
        "Host: name" -> "hOsT: name"
    dcsmix:
        "Host: name" -> "Host: NaMe"
    rmspace:
        "Host: name" -> "Host:name\t"

--proto значение
    белый список протоколов: tls,http,udp,ipv4

--hosts <файл|:домен>
    ограничить область действия параметров списком доменов
    домены должны быть разделены новой строкой или пробелом
пример:--host domen.txt или --hosts ":youtube.com instagram.com twitter.com" 
    
--ipset <файл|:ip>
    ограничитель по определенным ip/подсетям
пример:--ipset ip.txt или --ipset ":127.9.2.59/26 127.9.2.69/19 128.9.2.10/90"

--auto значение
    автоматический режим
    если произошло событие похожее на блокировку или поломку то будут применены параметры обхода следующие за данной опцией
    возможные события:
        torst   : вышло время ожидания или сервер сбросил подключение после первого запроса
        redirect: http redirect с location,домен которого не совпадает с исходящим
        ssl_err : в ответ на clienthello не пришел serverhello или sh содержит некорректный session_id
        none    : предыдущая группа пропущена,например из-за ограничения по доменам или протоколам
    
--auto-mode значение
    0: кешировать ip только если имеется возможность переподключиться
    1: кешировать ip также в том случае, если:
        torst - таймаут/соединение сброшено во время обмена пакетами (т.е. уже после первых данных от сервера)
        ssl_err - совершился лишь один круг обмена данными (запрос-ответ/запрос-ответ-запрос)

--def-ttl значение
    значение ttl для всех исходящий соединений
    может быть полезен для обхода обнаружения нестандартного/уменьшенного ttl
                               
--oob-data значение
    байт,отсылаемый вне основного потока,по умолчанию 'a'
    можно указать ascii или escape символ


```

------

после запуска подсоединяем браузер:<br>
на firefox устанавливаем в настройках сети socks5 прокси-узел:0000 порт:1080<br>
на chromium браузерах используем расширение foxyproxy (создаем socks5 прокси-ip адрес:0000 порт:1080 и подключаемся к нему) или же switchyomega (если хотите больше контроля)<br>

p.s файлы должны лежать вместе<br>

apple moment:<br>
если  mac os ругается при попытке открыть launch перейдите в-настройки/конфиденциальность и безопасность,пролестните в самый низ и нажмите:все равно открыть<br>
или добавьте файл в карантин с помощью:xattr -d com.apple.quarantine путь до файла launch<br>

автор решения-<a href="https://github.com/hufrea">hufrea</a><br>
