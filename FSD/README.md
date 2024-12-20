# Feature-Sliced Design

Проект на **FSD** состоит из **слоев** (layers), каждый слой состоит из **слайсов** (slices) и каждый слайс состоит из *
*сегментов** (segments).

![[FSD.canvas]]

## Слои

**Слои** стандартизированы во всех проектах и расположены вертикально. Модули на одном слое могут взаимодействовать лишь
с модулями, находящимися на слоях строго ниже. На данный момент слоев семь (снизу вверх):

1. `shared` — переиспользуемый код, не имеющий отношения к специфике приложения/бизнеса. (например, `UIKit`, `libs`,
   `API`)
2. `entities` (сущности) — бизнес-сущности. (например, User, Product, Order)
3. `features` (фичи) — взаимодействия с пользователем, действия, которые несут бизнес-ценность для пользователя. (
   например, `SendComment`, `AddToCart`, `UsersSearch`)
4. `widgets` (виджеты) — композиционный слой для соединения сущностей и фич в самостоятельные блоки (например,
   `IssuesList`, `UserProfile`).
5. `pages` (страницы) — композиционный слой для сборки полноценных страниц из сущностей, фич и виджетов.
6. ~~`processes`~~ (процессы, устаревший слой) — сложные сценарии, покрывающие несколько страниц. (например,
   авторизация)
7. `app` — настройки, стили и провайдеры для всего приложения.

## Слайсы

Затем есть **слайсы**, разделяющие код по предметной области. Они группируют логически связанные модули, что облегчает
навигацию по кодовой базе. ==Слайсы не могут использовать другие слайсы на том же слое==, что обеспечивает высокий
уровень [
_связности_](https://ru.wikipedia.org/wiki/%D0%A1%D0%B2%D1%8F%D0%B7%D0%BD%D0%BE%D1%81%D1%82%D1%8C_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)) (
cohesion) при низком уровне [
_зацепления_](https://ru.wikipedia.org/wiki/%D0%97%D0%B0%D1%86%D0%B5%D0%BF%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)) (
coupling).

1. user
2. post
3. comment
4. и т.д.

## Сегменты

В свою очередь, каждый слайс состоит из **сегментов**. Это маленькие модули, главная задача которых — разделить код
внутри слайса по техническому назначению. Самые распространенные сегменты — `ui`, `model` (store, actions), `api` и
`lib` (utils/hooks), но в вашем слайсе может не быть каких-то сегментов, могут быть другие, по вашему усмотрению.

1. ui
2. model
3. api
4. и т.д.

В большинстве случаев [рекомендуется](https://github.com/feature-sliced/documentation/discussions/66) располагать `api`
и `config` только в shared-слое.

## Ссылки

- https://feature-sliced.design
- https://feature-sliced.design/examples
- https://github.com/feature-sliced/awesome

### Tools

- https://github.com/feature-sliced/cli
- https://github.com/s4ff0x/fsd-cruise - simple dependency visualization for FSD

### Linter

- https://github.com/feature-sliced/steiger
- https://github.com/feature-sliced/eslint-config
- https://github.com/conarti/eslint-plugin-feature-sliced (community edition)

---

Теги: [[FSD]]