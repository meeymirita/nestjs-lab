# NestJS Lab — Helpdesk API с нуля

![NestJS](nest.png)

**Статус: ⚪ методичка готова, прохождение впереди.**
**Сложность: высокая.** Нужны пройденные Vue Lab (тот же Helpdesk-домен — бэкенд, который там был дан готовым, здесь собирается с нуля) и сессия 1 TypeScript-лабы (классы, интерфейсы, типы); из Чистого JS нужна сессия 5 (event loop, async/await).

## О чём

Тот же Helpdesk (тикеты, роли `agent`/`customer`, live-обновления), что в Vue Lab — только теперь backend строится слой за слоем, и на каждом шаге видно, что именно скрывает декоратор `@Injectable()`, когда его пишут не глядя: `reflect-metadata` под капотом, DI и provider scopes, DTO/Pipes/валидация, Prisma и N+1, Guards/JWT/refresh-токены, WebSocket Gateway, тестирование.

## Стек

NestJS 10 + TypeScript, Prisma + PostgreSQL 16, class-validator, Passport + JWT, `@nestjs/websockets` (Socket.IO), Jest + `@nestjs/testing`. Всё в Docker.

## Формат

Методичка [`NestJS_Lab_Plan.html`](NestJS_Lab_Plan.html) — открывается в браузере, прогресс по чекбоксам сохраняется локально.

## Что внутри (6 сессий)

- **Сессия 1** — стенд и наивная версия; декораторы руками без Nest (`reflect-metadata`, `emitDecoratorMetadata`); первый настоящий модуль (Controller/Service/DI)
- **Сессия 2** — provider scopes и singleton-ловушка; `useFactory` и токены; `PrismaService` с lifecycle hooks; N+1 — измерить, не декларировать
- **Сессия 3** — DTO и `ValidationPipe`; свой Pipe; exception filter; полный CRUD тикетов и комментариев
- **Сессия 4** — JWT-стратегия и логин; `AuthGuard` под капотом; `RolesGuard` и свой декоратор; refresh-токены и ротация
- **Сессия 5** — WebSocket Gateway и комнаты; эмит из сервиса через `forwardRef`; auth на handshake
- **Сессия 6** — unit-тест с мок Prisma; e2e-тест контроллера; "Production Hell" — финальный сценарий без подсказок

Разделы 1–7 методички — теория (декораторы и reflect-metadata, Modules и DI, DTO/Pipes, Prisma/N+1, Guards/JWT, WebSocket Gateway, тестирование), раздел 8 — шесть сессий заданий, разделы 9–12 — чек-лист, глоссарий, вопросы для собеседования, что дальше. Следующий шаг после этой лабы — отдельная GraphQL-лаба на том же backend'е.

---

Часть сборного репозитория лабораторных работ — [submodule-group-lab](https://github.com/meeymirita/submodule-group-lab).
