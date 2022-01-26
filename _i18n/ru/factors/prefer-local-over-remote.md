В последние годы некоторые группы разработчиков начали использовать подходы, которые требуют меньше усилий по разработке, за счет снижение качества *user experience*, перенеся больше логики на бэкэнд и сделав приложение iOS тонким клиентом, показывающим результаты сервера. Такой подход приводит к разочарованию пользователя, когда приложение используется в ситуации с неидеальным подключением к Интернету (например, в метро, ​​лифте или неровном WiFi).

**Приложение должно выполнять как можно больше бизнес-логики и вычислений на устройстве** по целому ряду причин:

- Конфиденциальность: избегайте отправки данных на удаленный сервер
- Скорость: отправка данных на сервер и ожидание ответа требует времени и может привести к сбою (например, плохой WiFi)
- Использование данных: пользователи часто имеют месячные лимиты данных
- Масштабирование: если ваше приложение становится популярным, вы несете ответственность за расширение масштабов бэкэнд-сервисов
- Срок службы батареи: использование мобильных данных обходится дорого
- Надежность: в некоторых странах все еще плохое соединения LTE / 3G

Большинству приложений iOS требуется какой-то бэкэнд для определенных задач, таких как аутентификация, более сложные вычисления или хранение контента.

**Ограничьте количество задач, выполняемых на сервере, до минимума, чтобы повысить удобство работы пользователя и защитить его конфиденциальность.**

Все части приложения, которым не обязательно **требуют** подключение к Интернету (например, логин), должны работать вообще без подключения к Интернету:

- Экрану запуска вашего приложения([которого не должно существовать](https://developer.apple.com/ios/human-interface-guidelines/icons-and-images/launch-screen/)) никогда не следует ждать первого успешного ответа от бека, так как это вызывает плохой UX для пользователей с нестабильным подключением к Интернету.
- Если вашему приложению требуется подключение к Интернету для всего функционала (например, приложение для социальных сетей или приложение для обмена поездками), оно должно по-прежнему работать (в режиме только для чтения) без подключения к Интернету для доступа к историческим данным (например, недавние поездки, недавние прямые сообщения).
- Любая функция вашего приложения, для которой требуется работающее подключение к Интернету, должна отображать четкое сообщение об ошибке, что сервер не может быть достигнут.
- Поскольку для точек доступа WiFi может потребоваться вход в систему или подтверждение каких-либо действий (например, в отеле или в аэропорту), запросы HTTPS часто зависают и время ожидания истекает примерно через минуту. Пока Apple не решит эту проблему на системном уровне, мы, как разработчики, должны быть в состоянии должным образом справиться с этими ситуациями.
- Никогда не думайте, что у пользователя есть работающее интернет-соединение при первом запуске приложения. Пользователь может установить ваше приложение, а затем не открывает его, пока он не будет в пути без подключения к интернету. Вы несете ответственность за доставку своего приложения в состоянии, когда оно работает «из коробки» с самой актуальной информацией во время деплоя. Это непосредственно играет вместе с еженедельными "release trains", описанными в факторе [Развертывания](/deployment).