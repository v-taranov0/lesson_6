# ДЗ №6 «Сервисный слой и бизнес-логика»
✅ полностью · 🟡 частично · ❌ не выполнено · ⚪ не подтверждено · ➖ бонус не требовался

| Студент | 1 Repository | 2 Service | 3 Исключения | 4 Router | 5 Зависимости | 6 Обработчики | 7 Конфигурация | 8 Документация |
|---|---|---|---|---|---|---|---|---|
| IGladkovsky | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| danilushkina01-lang | 🟡 | ✅ | ✅ | ✅ | ✅ | ⚪ | 🟡 | ❌ |
| sabirovilya2000 | ✅ | ✅ | ✅ | ✅ | 🟡 | ✅ | 🟡 | 🟡 |
| kseorx | 🟡 | ✅ | ✅ | ✅ | ✅ | ✅ | 🟡 | ✅ |
| linaalewii | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| askorsh | 🟡 | ✅ | ✅ | ✅ | ✅ | ✅ | 🟡 | ✅ |
| hawwkps | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Ogur4ick | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| krovinosets | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

---

## IGladkovsky

| 1 Repository | 2 Service | 3 Исключения | 4 Router | 5 Зависимости | 6 Обработчики | 7 Конфигурация | 8 Документация |
| ------------ | --------- | ------------ | -------- | ------------- | ------------- | -------------- | -------------- |
| ✅            | ✅         | ✅            | ✅        | ✅             | ✅             | ✅              | ✅              |

**Что хорошо**

- Хранение, бизнес-логика и HTTP разделены. Repository содержит список и последовательный счётчик ID, а проверка `completed` находится в сервисе. Прямые вызовы сервиса проходят без импорта FastAPI. [app/repository.py, строка 1](https://github.com/IGladkovsky/home_work_lesson6/blob/91dc418f5441571f382b3230dc2211ad6e54b281/app/repository.py#L1) [app/service.py, строка 27](https://github.com/IGladkovsky/home_work_lesson6/blob/91dc418f5441571f382b3230dc2211ad6e54b281/app/service.py#L27)
- Первый переход в `completed` разрешён. После него изменение имени, напитка, количества, размера, возврат другого статуса, повторный `completed`, пустой PATCH и DELETE отклоняются. Через API получены 409, после отказов заказ не изменился.
- Исправлены замечания ДЗ 5: ID больше не переиспользуется после удаления, status и `created_at` сохраняются вместе с заказом, фильтр работает, пустое название в PATCH возвращает 422. Поле напитка приведено к drink. [app/repository.py, строка 15](https://github.com/IGladkovsky/home_work_lesson6/blob/91dc418f5441571f382b3230dc2211ad6e54b281/app/repository.py#L15) [app/service.py, строка 22](https://github.com/IGladkovsky/home_work_lesson6/blob/91dc418f5441571f382b3230dc2211ad6e54b281/app/service.py#L22) [app/schemas.py, строка 41](https://github.com/IGladkovsky/home_work_lesson6/blob/91dc418f5441571f382b3230dc2211ad6e54b281/app/schemas.py#L41)
- Изменение `APP_NAME` и `DEFAULT_PAGE_LIMIT` в `.env` отразилось в /info и размере страницы. В Swagger видны семь операций, описания и выбор статуса; выполнен полный сценарий создания, завершения, отказа в изменении и отказа в отмене.

**Где неправильно**

Замечаний по обязательным критериям нет.

**Бонусы**

- ✅ **Пагинация.** limit/offset вынесены в `pagination_params` и `PaginationDep`; значения по умолчанию берутся из настроек. [app/dependencies.py, строка 21](https://github.com/IGladkovsky/home_work_lesson6/blob/91dc418f5441571f382b3230dc2211ad6e54b281/app/dependencies.py#L21) [app/routers/orders.py, строка 16](https://github.com/IGladkovsky/home_work_lesson6/blob/91dc418f5441571f382b3230dc2211ad6e54b281/app/routers/orders.py#L16)
- ➖ **Сортировка.** В проверенной работе ДЗ 5 сортировки не было; её перенос не требовался.

---

## danilushkina01-lang

**В опубликованном коммите приложение не запускается.** Результаты HTTP-проверок ниже относятся к копии с исправленным расположением файлов. ⚪ у обработчиков ошибок означает, что ответы 404/409 подтверждены только после этого исправления.

| 1 Repository | 2 Service | 3 Исключения | 4 Router | 5 Зависимости | 6 Обработчики | 7 Конфигурация | 8 Документация |
|---|---|---|---|---|---|---|---|
| 🟡 | ✅ | ✅ | ✅ | ✅ | ⚪ | 🟡 | ❌ |

**Что хорошо**

- Repository, service, модели и исключения доступны для прямой проверки. Сервис получает repository через конструктор, корректно поднимает `OrderNotFoundError` и `OrderAlreadyCompletedError` и не импортирует FastAPI. Проверки запрета изменений и отмены `completed` проходят на исходном коде. [app/service.py, строка 8](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/service.py#L8) [app/service.py, строка 44](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/service.py#L44)
- В коде эндпоинтов оставлены вызовы методов сервиса; поиск и правило `completed` находятся вне router. [app/orders.py, строка 13](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/orders.py#L13) [app/orders.py, строка 36](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/orders.py#L36)
- `get_repository` и `get_settings` кешируются; цепочка `Depends` и алиасы объявлены. В исходных модулях подтверждены повторное получение того же repository/settings и чтение тестового имени и размера страницы из `.env`. [app/dependencies.py, строка 11](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/dependencies.py#L11) [app/config.py, строка 14](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/config.py#L14)

**Где неправильно**

- **Приложение не запускается из текущей структуры.** Команда из README `fastapi dev app/main.py` завершается ошибкой `Path does not exist app/main.py`: файл `main.py` лежит в корне. Запуск `uvicorn main:app` падает на импорте `from .dependencies` с ошибкой `attempted relative import with no known parent package`. В `app/orders.py` импорт `from ..dependencies` также не соответствует расположению файла и вызывает `attempted relative import beyond top-level package`. Перемести `main.py` в `app/main.py`, `app/orders.py` в `app/routers/orders.py` и добавь пустой `app/routers/__init__.py`. После этих изменений команда из README запускает приложение, а `/`, `/info`, `/orders`, `/docs` и `/openapi.json` возвращают 200. [README.md, строка 9](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/README.md#L9) [main.py, строка 4](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/main.py#L4) [app/orders.py, строка 5](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/orders.py#L5)
- **В repository используется словарь.** В `self._orders` хранится `dict[int, Order]`, хотя в ДЗ 6 прямо требуется список внутри экземпляра. CRUD работает. Замечание относится к требованию хранить список. [app/repository.py, строка 8](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/repository.py#L8)
- **Название /info не берётся из Settings.** В ответ записывается `app.title`. После исправления расположения файлов изменение `APP_NAME` в `.env` не меняет ответ `/info`: он по-прежнему возвращает «Учёт заказов кофейни». Добавь `SettingsDep` в параметры info и используй `settings.app_name`. Сам `get_settings` файл `.env` читает корректно. [main.py, строка 23](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/main.py#L23)
- **Сохранилось замечание ДЗ 5 про пустой напиток.** У drink нет `min_length=1` ни в `OrderCreate`, ни в `OrderUpdate`. После исправления расположения файлов POST с `drink=""` вернул 201, PATCH незавершённого заказа — 200. Добавь ограничение в обе модели. [app/schemas.py, строка 21](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/schemas.py#L21) [app/schemas.py, строка 45](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/schemas.py#L45)

**Бонусы**

- ✅ **Пагинация.** `pagination_params` и `PaginationDep` реализованы. После исправления размещения файлов зависимость подключается, а `DEFAULT_PAGE_SIZE=2` даёт страницу из двух заказов. [app/dependencies.py, строка 20](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/dependencies.py#L20) [app/orders.py, строка 19](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/orders.py#L19)
- ✅ **Сортировка в сервисе.** На допустимых полях drink и `created_at` сортировка выполняется до среза и проходит прямые проверки. Дополнительно ограничь `sort_by` через Enum/Literal: неизвестное поле приводит к `AttributeError`; после исправления запуска запрос с таким полем возвращает 500. [app/service.py, строка 24](https://github.com/danilushkina01-lang/cafe-orders-service/blob/5c29f9fbb3bd2ce67b8d345e53def913a416bb4e/app/service.py#L24)

---

## sabirovilya2000

| 1 Repository | 2 Service | 3 Исключения | 4 Router | 5 Зависимости | 6 Обработчики | 7 Конфигурация | 8 Документация |
|---|---|---|---|---|---|---|---|
| ✅ | ✅ | ✅ | ✅ | 🟡 | ✅ | 🟡 | 🟡 |

**Что хорошо**

- Repository хранит список в экземпляре и назначает неповторяющиеся ID. В сервис вынесены создание, поиск, фильтрация, обновление и отмена; проверка сохранённого `completed` выполняется до записи. [app/repository.py, строка 4](https://github.com/sabirovilya2000/lesson-6/blob/53a3c209098dd60319e7f6311c75f9d2bba836f7/app/repository.py#L4) [app/service.py, строка 36](https://github.com/sabirovilya2000/lesson-6/blob/53a3c209098dd60319e7f6311c75f9d2bba836f7/app/service.py#L36)
- В исходном приложении подтверждены 201 при создании, 204 без тела при отмене незавершённого заказа, 404 для отсутствующего ID и 409 при изменении/удалении `completed`. Прямые проверки без FastAPI и сценарий заказов через Swagger проходят.
- Роутер заказов тонкий, `get_repository` и `get_settings` кешируются, оба обработчика доменных ошибок зарегистрированы в main. [app/routers/orders.py, строка 9](https://github.com/sabirovilya2000/lesson-6/blob/53a3c209098dd60319e7f6311c75f9d2bba836f7/app/routers/orders.py#L9) [app/main.py, строка 15](https://github.com/sabirovilya2000/lesson-6/blob/53a3c209098dd60319e7f6311c75f9d2bba836f7/app/main.py#L15)

**Где неправильно**

- **`GET /info` возвращает 500.** Внутри `get_info` вызывается `get_service()` без аргумента repo. `Depends` подставляет этот аргумент при обработке запроса FastAPI, но не при обычном вызове Python-функции. Получается `TypeError` о недостающем repo. Получай service: `ServiceDep` и settings: `SettingsDep` в сигнатуре /info; количество заказов лучше вернуть отдельным методом сервиса. [app/main.py, строка 39](https://github.com/sabirovilya2000/lesson-6/blob/53a3c209098dd60319e7f6311c75f9d2bba836f7/app/main.py#L39) [app/dependencies.py, строка 16](https://github.com/sabirovilya2000/lesson-6/blob/53a3c209098dd60319e7f6311c75f9d2bba836f7/app/dependencies.py#L16)
- **Размер страницы не использует настройки.** В роутере limit закреплён как 10. После `DEFAULT_PAGE_SIZE=2` список без limit вернул все пять созданных в сценарии заказов. Используй значение из Settings при отсутствии query-параметра; вынесение этих параметров в `PaginationDep` дополнительно выполнит бонус. [app/routers/orders.py, строка 15](https://github.com/sabirovilya2000/lesson-6/blob/53a3c209098dd60319e7f6311c75f9d2bba836f7/app/routers/orders.py#L15) [app/config.py, строка 7](https://github.com/sabirovilya2000/lesson-6/blob/53a3c209098dd60319e7f6311c75f9d2bba836f7/app/config.py#L7)
- **При переносе потеряны примеры полей.** В ДЗ 5 у size, quantity и `customer_name` были examples. В новой `OrderCreate` они убраны. Swagger открывается и позволяет выполнять запросы, но оформление сохранено частично. Верни examples для этих полей. [app/schemas.py, строка 21](https://github.com/sabirovilya2000/lesson-6/blob/53a3c209098dd60319e7f6311c75f9d2bba836f7/app/schemas.py#L21)

**Бонусы**

- ❌ **Пагинация в зависимости.** `pagination_params` / `PaginationDep` не реализованы; limit и offset остались параметрами роутера. Это необязательная часть. [app/routers/orders.py, строка 15](https://github.com/sabirovilya2000/lesson-6/blob/53a3c209098dd60319e7f6311c75f9d2bba836f7/app/routers/orders.py#L15)
- ➖ **Сортировка.** В проверенной работе ДЗ 5 её не было; перенос не требовался.

---

## kseorx

| 1 Repository | 2 Service | 3 Исключения | 4 Router | 5 Зависимости | 6 Обработчики | 7 Конфигурация | 8 Документация |
|---|---|---|---|---|---|---|---|
| 🟡 | ✅ | ✅ | ✅ | ✅ | ✅ | 🟡 | ✅ |

**Что хорошо**

- Сервис не зависит от FastAPI, получает repository через конструктор и корректно проверяет `completed` перед PATCH и DELETE. Прямые вызовы возвращают нужные доменные исключения, сохранённые данные после отказов не меняются. [service.py, строка 7](https://github.com/kseorx/cafe_orders_dz6/blob/ea6f27044b5e22aa98746d20d133e7760f413a92/service.py#L7) [service.py, строка 48](https://github.com/kseorx/cafe_orders_dz6/blob/ea6f27044b5e22aa98746d20d133e7760f413a92/service.py#L48)
- `APIRouter`, `Depends`, кеши и обработчики 404/409 подключены. Создание, получение по ID, частичное обновление, отмена и сценарии `completed` работают. В Swagger выполнен полный сценарий заказов.
- При явных limit и offset проходит полный HTTP-набор: фильтр применяется до среза, ID не переиспользуются, `created_at` сохраняется, невалидные значения отклоняются. Изменённое имя из `.env` отображается в /info.

**Где неправильно**

- **`GET /orders` без параметров возвращает 500.** `pagination_params` возвращает `None` для отсутствующих limit и offset. Затем service.list_orders вычисляет offset + limit. Ошибка воспроизводится без обоих параметров и при пропуске любого одного. `GET /orders?limit=2&offset=0` возвращает 200. Подними `SettingsDep` выше определения зависимости, внедри settings и замени `None` на `settings.default_limit` / `settings.default_offset`. Значения объявлены в config.py, но сейчас не используются. [dependencies.py, строка 19](https://github.com/kseorx/cafe_orders_dz6/blob/ea6f27044b5e22aa98746d20d133e7760f413a92/dependencies.py#L19) [service.py, строка 46](https://github.com/kseorx/cafe_orders_dz6/blob/ea6f27044b5e22aa98746d20d133e7760f413a92/service.py#L46) [config.py, строка 5](https://github.com/kseorx/cafe_orders_dz6/blob/ea6f27044b5e22aa98746d20d133e7760f413a92/config.py#L5)
- **Хранилище выполнено словарём.** `self._orders` — `dict[int, Order]`. В задании 6 прямо требуется список внутри OrderRepository. Операции доступа к данным работают и не содержат проверки `completed`; замечание касается соответствия форме хранилища. [repository.py, строка 6](https://github.com/kseorx/cafe_orders_dz6/blob/ea6f27044b5e22aa98746d20d133e7760f413a92/repository.py#L6)

**Бонусы**

- ✅ **Вынос пагинации.** `pagination_params` и `PaginationDep` подключены, отдельные limit/offset из роутера убраны. Ошибка значений по умолчанию разобрана выше в обязательной части. [dependencies.py, строка 19](https://github.com/kseorx/cafe_orders_dz6/blob/ea6f27044b5e22aa98746d20d133e7760f413a92/dependencies.py#L19) [routers/orders.py, строка 15](https://github.com/kseorx/cafe_orders_dz6/blob/ea6f27044b5e22aa98746d20d133e7760f413a92/routers/orders.py#L15)
- ✅ **Сортировка.** Перенесена в сервис. Сортировка по drink и `created_at` проверена напрямую; через API подтверждена работа вместе с фильтром и пагинацией. [service.py, строка 29](https://github.com/kseorx/cafe_orders_dz6/blob/ea6f27044b5e22aa98746d20d133e7760f413a92/service.py#L29)

---

## linaalewii

| 1 Repository | 2 Service | 3 Исключения | 4 Router | 5 Зависимости | 6 Обработчики | 7 Конфигурация | 8 Документация |
|---|---|---|---|---|---|---|---|
| ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

**Что хорошо**

- Repository хранит список и занимается доступом к данным. Сервис получает repository и настройки, а HTTP-роутер только передаёт разобранные параметры. [app/repository.py, строка 4](https://github.com/linaalewii/dz6_app/blob/f42b39458ebdac89a715da3b466cdf8e186cd718/app/repository.py#L4) [app/service.py, строка 7](https://github.com/linaalewii/dz6_app/blob/f42b39458ebdac89a715da3b466cdf8e186cd718/app/service.py#L7) [app/routers/orders.py, строка 22](https://github.com/linaalewii/dz6_app/blob/f42b39458ebdac89a715da3b466cdf8e186cd718/app/routers/orders.py#L22)
- Проверка `completed` вынесена в общий метод и вызывается перед обновлением и отменой. Все варианты запрещённого PATCH и DELETE дают доменное исключение напрямую и 409 через API; состояние заказа сохраняется. [app/service.py, строка 18](https://github.com/linaalewii/dz6_app/blob/f42b39458ebdac89a715da3b466cdf8e186cd718/app/service.py#L18) [app/service.py, строка 57](https://github.com/linaalewii/dz6_app/blob/f42b39458ebdac89a715da3b466cdf8e186cd718/app/service.py#L57)
- При изменении `.env` название сервиса и размер страницы меняются. /info показывает реальное количество заказов. Кеши и цепочка `Depends` подтверждены; Swagger отображает семь операций и позволяет выполнить полный сценарий.

**Где неправильно**

Замечаний по обязательным критериям нет.

**Бонусы**

- ❌ **Пагинация в зависимости.** limit и offset остались отдельными параметрами эндпоинта; `PaginationDep` не добавлен. Это бонус и на обязательные отметки не влияет. [app/routers/orders.py, строка 28](https://github.com/linaalewii/dz6_app/blob/f42b39458ebdac89a715da3b466cdf8e186cd718/app/routers/orders.py#L28)
- ✅ **Сортировка.** Выполняется в service.list_orders до пагинации, работает по drink и `created_at`. Проверены прямые вызовы и HTTP-запрос с фильтром, limit и offset. [app/service.py, строка 25](https://github.com/linaalewii/dz6_app/blob/f42b39458ebdac89a715da3b466cdf8e186cd718/app/service.py#L25)

---

## askorsh

| 1 Repository | 2 Service | 3 Исключения | 4 Router | 5 Зависимости | 6 Обработчики | 7 Конфигурация | 8 Документация |
|---|---|---|---|---|---|---|---|
| 🟡 | ✅ | ✅ | ✅ | ✅ | ✅ | 🟡 | ✅ |

**Что хорошо**

- Бизнес-правило реализовано в сервисе: `completed` нельзя изменить или отменить. Ошибки отсутствующего заказа и конфликта — собственные Exception; HTTP-коды формируются обработчиками в main. Прямые вызовы без FastAPI и запросы через Swagger проходят. [app/service.py, строка 46](https://github.com/askorsh/lesson_6/blob/bb5468b0dfe5d259b0c5179ec8dff68f5f5285ed/app/service.py#L46) [app/main.py, строка 32](https://github.com/askorsh/lesson_6/blob/bb5468b0dfe5d259b0c5179ec8dff68f5f5285ed/app/main.py#L32)
- Роутер не выполняет поиск и проверку статуса. Кешированный repository сохраняет данные между запросами; ID и `created_at` ведут себя правильно.
- Замечание ДЗ 5 про модель списка исправлено: теперь `GET /orders` объявляет `response_model=list[Order]`. Документация и валидация входных данных работают. [app/routers/orders.py, строка 22](https://github.com/askorsh/lesson_6/blob/bb5468b0dfe5d259b0c5179ec8dff68f5f5285ed/app/routers/orders.py#L22)

**Где неправильно**

- **Repository хранит словарь вместо списка.** В ДЗ 6 нужен список `self._orders`; сейчас используется `dict[int, Order]`. CRUD функционально работает, бизнес-проверок в repository нет. [app/repository.py, строка 6](https://github.com/askorsh/lesson_6/blob/bb5468b0dfe5d259b0c5179ec8dff68f5f5285ed/app/repository.py#L6)
- **`DEFAULT_PAGE_SIZE` не влияет на выдачу.** В роутере стоит Query(default=10). После изменения `DEFAULT_PAGE_SIZE` на 2 запрос без limit вернул пять заказов из тестового набора. При отсутствии limit используй `settings.default_page_size`, полученный через `Depends`. [app/routers/orders.py, строка 32](https://github.com/askorsh/lesson_6/blob/bb5468b0dfe5d259b0c5179ec8dff68f5f5285ed/app/routers/orders.py#L32)
- **В /info всегда ноль заказов.** `orders_count` задан константой 0. Например, после успешного POST с id=2 эндпоинт всё равно вернул ноль. Добавь в сервис `count_orders()`, получай `ServiceDep` в /info и возвращай фактическую длину хранилища. [app/main.py, строка 24](https://github.com/askorsh/lesson_6/blob/bb5468b0dfe5d259b0c5179ec8dff68f5f5285ed/app/main.py#L24)

**Бонусы**

- ❌ **Пагинация в зависимости.** `pagination_params` и `PaginationDep` отсутствуют; limit/offset остались в роутере. Это необязательный пункт.
- 🟡 **Сортировка.** В сервисе сортировка по drink и `created_at` работает, но эндпоинт не принимает и не передаёт `sort_by`. GET с `sort_by=drink` продолжает использовать порядок по `created_at`: в проверке второй элемент оказался «Латте» вместо «Капучино». Передай параметр в сервис. В ДЗ 5 сортировки не было, поэтому это замечание к новой дополнительной возможности. [app/service.py, строка 28](https://github.com/askorsh/lesson_6/blob/bb5468b0dfe5d259b0c5179ec8dff68f5f5285ed/app/service.py#L28) [app/routers/orders.py, строка 27](https://github.com/askorsh/lesson_6/blob/bb5468b0dfe5d259b0c5179ec8dff68f5f5285ed/app/routers/orders.py#L27)

---

## hawwkps

| 1 Repository | 2 Service | 3 Исключения | 4 Router | 5 Зависимости | 6 Обработчики | 7 Конфигурация | 8 Документация |
|---|---|---|---|---|---|---|---|
| ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

**Что хорошо**

- Все три слоя отделены. Repository содержит список и счётчик ID, сервис выполняет бизнес-операции, router вызывает по одному методу сервиса. Прямые проверки работают без FastAPI. [app/repository.py, строка 4](https://github.com/hawwkps/hw_6/blob/3f3e4156bfbf666bfb649d0dae392203e1b9a3c3/app/repository.py#L4) [app/service.py, строка 6](https://github.com/hawwkps/hw_6/blob/3f3e4156bfbf666bfb649d0dae392203e1b9a3c3/app/service.py#L6)
- Общий _get_editable_order проверяет существование заказа и сохранённый статус перед записью и удалением. PATCH/DELETE `completed` возвращают 409, чтение после отказа показывает прежний заказ. [app/service.py, строка 39](https://github.com/hawwkps/hw_6/blob/3f3e4156bfbf666bfb649d0dae392203e1b9a3c3/app/service.py#L39)
- В репозитории есть `.env.example`. После изменения настроек в `.env` `/info` показывает новое имя, а список без limit содержит два заказа. Кеши и `Depends` работают; Swagger и полный сценарий заказов проверены.

**Где неправильно**

Замечаний по обязательным критериям нет.

**Бонусы**

- ✅ **Пагинация.** `pagination_params` получает настройки через `SettingsDep`, `PaginationDep` используется в роутере. [app/dependencies.py, строка 28](https://github.com/hawwkps/hw_6/blob/3f3e4156bfbf666bfb649d0dae392203e1b9a3c3/app/dependencies.py#L28) [app/routers/orders.py, строка 17](https://github.com/hawwkps/hw_6/blob/3f3e4156bfbf666bfb649d0dae392203e1b9a3c3/app/routers/orders.py#L17)
- ✅ **Сортировка.** Перенесена в сервис и выполняется до среза. Проверены drink/`created_at`, фильтр и offset/limit; неверный `sort_by` отклоняется с 422. [app/service.py, строка 20](https://github.com/hawwkps/hw_6/blob/3f3e4156bfbf666bfb649d0dae392203e1b9a3c3/app/service.py#L20)

---

## Ogur4ick

| 1 Repository | 2 Service | 3 Исключения | 4 Router | 5 Зависимости | 6 Обработчики | 7 Конфигурация | 8 Документация |
|---|---|---|---|---|---|---|---|
| ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

**Что хорошо**

- Repository инкапсулирует список, выдаёт отдельные копии объектов и проверяет модель до сохранения изменения. Проверка `completed` при этом находится в сервисе. [app/repository.py, строка 4](https://github.com/Ogur4ick/lesson-6/blob/e286140d085717306e48e9e88802aa4f5a6bf9da/app/repository.py#L4) [app/repository.py, строка 27](https://github.com/Ogur4ick/lesson-6/blob/e286140d085717306e48e9e88802aa4f5a6bf9da/app/repository.py#L27) [app/service.py, строка 32](https://github.com/Ogur4ick/lesson-6/blob/e286140d085717306e48e9e88802aa4f5a6bf9da/app/service.py#L32)
- Подтверждены CRUD, неповторяющиеся ID, сохранение `created_at`, частичные обновления, 404 отсутствующих заказов и запрет всех изменений/отмены `completed`. Прямые проверки сервиса проходят без FastAPI.
- Зависимости и оба кеша собраны правильно. `APP_NAME` и `DEFAULT_PAGE_SIZE` из изменённой `.env` используются в API, /info считает реальные заказы. Swagger и выбор статуса работают, сценарий `completed` проверен через Try it out.

**Где неправильно**

Замечаний по обязательным критериям нет.

**Бонусы**

- ✅ **Пагинация.** Вынесена в `pagination_params` / `PaginationDep`. Параметры передаются в сервис через объект Pagination; настройки задают размер страницы и смещение. [app/dependencies.py, строка 20](https://github.com/Ogur4ick/lesson-6/blob/e286140d085717306e48e9e88802aa4f5a6bf9da/app/dependencies.py#L20) [app/routers/orders.py, строка 13](https://github.com/Ogur4ick/lesson-6/blob/e286140d085717306e48e9e88802aa4f5a6bf9da/app/routers/orders.py#L13)
- ✅ **Сортировка.** Выполняется в сервисе после фильтра и до среза. Проверены drink/`created_at` и составной HTTP-запрос; недопустимое поле даёт 422. [app/service.py, строка 22](https://github.com/Ogur4ick/lesson-6/blob/e286140d085717306e48e9e88802aa4f5a6bf9da/app/service.py#L22)

---

## krovinosets

| 1 Repository | 2 Service | 3 Исключения | 4 Router | 5 Зависимости | 6 Обработчики | 7 Конфигурация | 8 Документация |
|---|---|---|---|---|---|---|---|
| ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

**Что хорошо**

- Repository хранит список в экземпляре и возвращает глубокие копии моделей. Новый ID берётся из отдельного счётчика; изменение проходит проверку Order до записи. Бизнес-правило отсутствует в repository и реализовано в сервисе. [app/repository.py, строка 6](https://github.com/krovinosets/lesson-6/blob/b71a1af495044a22d3220f105c344c5d4a38d328/app/repository.py#L6) [app/repository.py, строка 27](https://github.com/krovinosets/lesson-6/blob/b71a1af495044a22d3220f105c344c5d4a38d328/app/repository.py#L27)
- Повторные изменения `completed`, включая пустой PATCH и попытку вернуть pending, а также DELETE отклоняются без изменения данных. Собственные исключения проверены прямыми вызовами без FastAPI, HTTP-обработчики возвращают 404/409. [app/service.py, строка 35](https://github.com/krovinosets/lesson-6/blob/b71a1af495044a22d3220f105c344c5d4a38d328/app/service.py#L35) [app/main.py, строка 20](https://github.com/krovinosets/lesson-6/blob/b71a1af495044a22d3220f105c344c5d4a38d328/app/main.py#L20)
- Настройки из `.env`, фактический счётчик /info, кеширование и `Depends` работают. В Swagger сохранены метаданные, теги и summary; дополнительно описаны ошибки 404/409. Через интерфейс пройден полный сценарий заказов. [app/routers/orders.py, строка 8](https://github.com/krovinosets/lesson-6/blob/b71a1af495044a22d3220f105c344c5d4a38d328/app/routers/orders.py#L8)

**Где неправильно**

Замечаний по обязательным критериям нет.

**Бонусы**

- ✅ **Пагинация.** `pagination_params` и `PaginationDep` подключены. Размер страницы и смещение берутся из настроек, когда клиент их не указал. [app/dependencies.py, строка 28](https://github.com/krovinosets/lesson-6/blob/b71a1af495044a22d3220f105c344c5d4a38d328/app/dependencies.py#L28)
- ✅ **Сортировка.** Находится в сервисе, порядок операций — фильтр, сортировка, срез. Прямые и HTTP-проверки пройдены; неверный `sort_by` даёт 422. [app/service.py, строка 23](https://github.com/krovinosets/lesson-6/blob/b71a1af495044a22d3220f105c344c5d4a38d328/app/service.py#L23)
