# NestJS Lab — Helpdesk API с нуля

![NestJS](https://raw.githubusercontent.com/meeymirita/works-lab/main/images/nestjs.png)

> **24.09.2026 — старая версия методички (5 сессий) вычитана и исправлена.** Содержимое с тех пор полностью переписано (см. ниже), запись оставлена для истории — [fixes/backend/nestjs.md](https://github.com/meeymirita/lab-fixes/blob/main/backend/nestjs.md) репозитория `lab-fixes`.

**Статус: 🟡 перестройка 5→14 сессий дописана 15.10.2026 (37 шагов, список ниже готов полностью), но отдельного прохода построчной вычитки и прогона в Docker по новым сессиям 2–14 ещё не было** (сессия 1 вычитана по месту написания 12.10). Содержание не вычитывалось владельцем.
**Сложность: высокая.** Проект полностью самостоятельный — отдельный репозиторий, ничего не импортирует из других лаб. TypeScript-минимум, нужный для Nest (декораторы, generics, `satisfies`), объясняется по ходу в сессии 1. Полное изучение NestJS с нуля как отдельной технологии: домен Helpdesk похож на Vue Lab только по смыслу (тикеты, роли `agent`/`customer`, live-обновления), прохождение Vue Lab не требуется.

## О чём

Helpdesk API собирается с нуля слой за слоем — и на каждом шаге видно, что скрывает декоратор `@Injectable()`, когда его пишут не глядя: свой мини-DI контейнер и метаданные декораторов, границы модулей и provider scopes, DTO и `ValidationPipe`, Prisma и транзакции, JWT-ротация refresh-токенов с обнаружением повторного использования (reuse detection), RBAC и владение через `TicketPolicy`, доменные события, WebSocket-шлюз с комнатами и своей авторизацией на handshake, свой динамический модуль, Swagger, unit- и e2e-тесты.

## Стек

NestJS 11 + TypeScript (strict), Prisma 7 + PostgreSQL 18, class-validator/class-transformer, `@nestjs/passport` + `passport-jwt` + `@nestjs/jwt` + argon2, `@nestjs/event-emitter`, `@nestjs/websockets` (Socket.IO), `@nestjs/swagger`, helmet + `@nestjs/throttler`, `@nestjs/terminus`, Jest + supertest. Всё в Docker.

## Формат

Методичка [`nestjs.html`](nestjs.html) ([открыть на сайте](https://anitech.meeymirita.ru/works/nestjs.html)) — открывается в браузере, прогресс по чекбоксам сохраняется локально.

## Что внутри (14 сессий, 37 шагов — написаны все, вычитка не пройдена)

- **Сессия 1** — TypeScript для Nest и как на самом деле работает DI: декораторы и метаданные, мини-DI-контейнер руками, первый настоящий модуль
- **Сессия 2** — модули, конфигурация, провайдеры: границы модулей, `ConfigModule` с валидацией env, `useValue`/`useFactory`
- **Сессия 3** — PostgreSQL и Prisma: Docker Compose, схема, первая миграция, `PrismaService`, тестовые данные
- **Сессия 4** — DTO и `ValidationPipe`, CRUD тикетов
- **Сессия 5** — ошибки Prisma в HTTP, транзакции, слои приложения (история изменений)
- **Сессия 6** — регистрация и хэши (argon2), логин и `JwtStrategy`
- **Сессия 7** — guards, `@Public()`/`@CurrentUser()`, как Reflector читает метаданные
- **Сессия 8** — refresh-токены: ротация и обнаружение повторного использования (reuse detection)
- **Сессия 9** — роли и владение ресурсом (`TicketPolicy`), доменные события
- **Сессия 10** — комментарии и внутренние заметки
- **Сессия 11** — WebSocket-шлюз: комнаты, авторизация на handshake
- **Сессия 12** — middleware, interceptors, Swagger, безопасность (CORS, helmet, rate limit)
- **Сессия 13** — unit- и e2e-тесты
- **Сессия 14** — свой динамический модуль (аудит), health-чеки, graceful shutdown, Docker, "Production Hell" — финальный сценарий без подсказок

Разделы 1–8 методички — теория (разбор задачи, как NestJS устроен внутри, итоговая архитектура, стек и структура, access/refresh-аутентификация, сценарий жизненного цикла тикета, Pipes/Guards/Interceptors/Filters, real-time и доменные события), раздел 9 — сессии заданий, разделы 10–13 — чек-лист, глоссарий, вопросы для собеседования, что дальше.

## Лицензия и авторство

Код — MIT, тексты — CC BY 4.0, обложки и иллюстрации не покрыты (см. [LICENSE](LICENSE)). Кто что сделал: [NOTICE](NOTICE).

---

Часть сборного репозитория лабораторных работ — [anitech-performance](https://github.com/meeymirita/anitech-performance).
