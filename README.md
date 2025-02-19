byedpi для mac os<br>

запускаем launch и вводим флаги для запуска:<br>

------
### описание флагов
```
-i, --ip <ip>
    Прослушиваемый IP, по умолчанию 0.0.0.0

-p, --port <num>
    Прослушиваемый порт, по умолчанию 1080

-s, --split <pos_t>
    Разбить запрос по указанной позиции
    Позиция имеет вид offset[:repeats:skip][+flag1[flag2]]
    Флаги:
        +s: добавить смещение SNI
        +h: добавить смещение Host
        +n: нулевое смещение
    Дополнительные флаги:
        +e: конец; +m: середина
    Примеры: 
        0+sm - разбить запрос в середине SNI
        1:3:5 - разбить по позициям 1, 6 и 11
    Ключ можно указывать несколько раз, чтобы разбить запрос по нескольким позициям
    Если offset отрицательный и не имеет флагов, то к нему прибавляется размер пакета

-d, --disorder <pos_t>
    Подобен --split, но части отправляются в обратном порядке
    
-o, --oob <pos_t>
    Подобен --split, но часть отсылается как OOB данные
    
-q, --disoob <pos_t>
    Подобен --disorder, но часть отсылается как OOB данные

-r, --tlsrec <pos_t>
    Разделить ClientHello на отдельные записи по указанному смещению
    Можно указывать несколько раз

-M, --mod-http <h[,d,r]>
    Всякие манипуляции с HTTP пакетом, можно комбинировать
    hcsmix:
        "Host: name" -> "hOsT: name"
    dcsmix:
        "Host: name" -> "Host: NaMe"
    rmspace:
        "Host: name" -> "Host:name\t"

-K, --proto <t,h,u,i>
    Белый список протоколов: tls,http,udp,ipv4

-H, --hosts <file|:string>
    Ограничить область действия параметров списком доменов
    Домены должны быть разделены новой строкой или пробелом
    
-j, --ipset <file|:str>
    Ограничитель по определенным IP/подсетям

-A, --auto <t,r,s,n>
    Автоматический режим
    Если произошло событие, похожее на блокировку или поломку,
    то будут применены параметры обхода, следующие за данной опцией
    Возможные события:
        torst   : Вышло время ожидания или сервер сбросил подключение после первого запроса
        redirect: HTTP Redirect с Location, домен которого не совпадает с исходящим
        ssl_err : В ответ на ClientHello не пришел ServerHello или SH содержит некорректный session_id
        none    : Предыдущая группа пропущена, например из-за ограничения по доменам или протоколам
    
-L, --auto-mode <0|1>
    0: кешировать IP только если имеется возможность переподключиться
    1: кешировать IP также в том случае, если:
        torst - таймаут/соединение сброшено во время обмена пакетами (т.е. уже после первых данных от сервера)
        ssl_err - совершился лишь один круг обмена данными (запрос-ответ/запрос-ответ-запрос)

-N, --no-domain
    Отбрасывать запросы, если в качестве адреса указан домен
    Т.к. резолвинг выполняется синхронно, то он может замедлить или даже заморозить работу

-U, --no-udp
    Не проксировать UDP 

-g, --def-ttl <num>
    Значение TTL для всех исходящий соединений
    Может быть полезен для обхода обнаружения нестандартного/уменьшенного TTL
                               
-e, --oob-data <char>
    Байт, отсылаемый вне основного потока, по умолчанию 'a'
    Можно указать ASCII или escape символ


```

------

после запуска подсоединяем браузер:<br>
на firefox устанавливаем в настройках socks5 прокси-узел:0000 порт:1080<br>
на chromium браузерах используем расширения вроде foxyproxy или zero omega<br>

автор решения-<a href="https://github.com/hufrea">hufrea</a><br>

p.s файлы должны лежать вместе<br>

apple moment:<br>
если  mac os ругается при попытке открыть launch перейдите в-настройки/конфиденциальность и безопасность,пролестните в самый низ и нажмите:все равно открыть<br>
или добавьте файл в карантин с помощью:xattr -d com.apple.quarantine путь до файла launch
