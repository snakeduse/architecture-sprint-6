# Задание 3. Переход на Event-Driven архитектуру

Документ содержит перичень проблем и рисков, которые связаны с планируемым ростом нагрузки на компоненты `core-app`, `ins-comp-settlement` и `ins-product-aggregator`.

Проблемы:
- Используется синхронное взаимодействие по REST API при обращении к `ins-product-aggregator`, при этом не требуется получать информацию в реальном времени;
- Замедление работы сервиса `ins-product-aggregator` сказывается на производительности на клиентов (`core-app` и `ins-comp-settlement`);
- Доступность сервиса `ins-product-aggregator` сказывается на клиентах (`core-app` и `ins-comp-settlement`);
- Синхронная работа `ins-product-aggregator` может вызывать проблемы с масштабированием этого сервиса для увеличения его RPS;

Риски:
- Несогласованность данных - какое время данные между `core-app`, `ins-comp-settlement` и `ins-product-aggregator` могут быть несогласованны между собой;
- Репликация данных у сервиосов `core-app` и `ins-comp-settlement` может отставать от источника `ins-product-aggregator`;
- Слишком частое изменение данных в `ins-product-aggregator` может значительно усложнить синхронизацию между `ins-product-aggregator` и `core-app`, `ins-comp-settlement`.

Диаграмма с примененным подходом Event-Driven архитектуры находится [тут](./InsureTech_C4_сontainer-diagram.drawio.xml).