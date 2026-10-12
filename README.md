<p align="center">
  <img src="assets/header.svg" width="100%" alt="Anton Zhuravlev — Senior Fullstack / Backend Engineer, Tech Lead, AI/LLM platforms"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3200&pause=900&color=8F7BFF&center=true&vCenter=true&width=820&height=44&lines=%D0%A1%D0%BE%D0%B1%D1%80%D0%B0%D0%BB%20AI-%D1%8F%D0%B4%D1%80%D0%BE%20%D0%B4%D0%BB%D1%8F%2012%2B%20%D0%BF%D1%80%D0%BE%D0%B4%D1%83%D0%BA%D1%82%D0%BE%D0%B2%20ERA2;LLM%20gateway%20%C2%B7%20RAG%20%D0%BD%D0%B0%20pgvector%20%C2%B7%20LangGraph%20%C2%B7%20MCP;Tech%20Lead%20%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D1%8B%208%3A%20%D0%BD%D0%B0%D0%B9%D0%BC%2C%20%D1%80%D0%B5%D0%B2%D1%8C%D1%8E%2C%201%3A1;%D0%9F%D0%BB%D0%B0%D1%82%D0%B5%D0%B6%D0%B8%2C%20highload%2C%20realtime%20%E2%80%94%20%D0%B8%D0%B4%D0%B5%D0%BC%D0%BF%D0%BE%D1%82%D0%B5%D0%BD%D1%82%D0%BD%D0%BE" alt="Собрал AI-ядро для 12+ продуктов ERA2 · LLM gateway, RAG, агенты, MCP · Tech Lead команды 8"/>
</p>

<p align="center">
  <a href="https://t.me/olddeveloper21"><img src="https://img.shields.io/badge/Telegram-@olddeveloper21-26A5E4?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram"/></a>
  <a href="mailto:anton.zhuravlev21@gmail.com"><img src="https://img.shields.io/badge/Email-anton.zhuravlev21@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/></a>
  <img src="https://img.shields.io/badge/Open_to_work-Remote_·_Hybrid-2ea44f?style=for-the-badge" alt="Open to work"/>
</p>

<p align="center">
  <img src="assets/metrics.svg" width="100%" alt="7+ лет в разработке · 12+ AI-продуктов на одном ядре · 90+ моделей за одним шлюзом · 2M+ пользователей Web3-платформы · команда 8 · 95%+ успешных платежей"/>
</p>

Senior Fullstack / Backend и Tech Lead, 7+ лет. Делаю продукты end-to-end — от схемы БД и очередей до интерфейса и релиза — и веду команды. Последние два года: высоконагруженная iGaming-платформа на 170+ инженеров и AI-направление ERA2, где я собрал платформенное ядро для 12+ AI-продуктов и вырос до Tech Lead команды из 8.

## ⚡ AI-ядро

В ERA2 на одном ядре работают 12+ продуктов: единый шлюз над 90+ моделями от 15+ провайдеров, асинхронная очередь генераций, RAG на pgvector и общий кредитный биллинг. Новый продукт подключается конфигом, а не форком сервиса. **LLM-платформа ниже — те же архитектурные идеи в открытом коде**: пять сервисов, которые вместе дают исследовательского агента с честными цитатами и полным учётом расхода. Поднимается одной командой и работает офлайн на детерминированном мок-провайдере.

```mermaid
flowchart LR
    UI["llm-platform-console<br/>React 19 · Hono BFF · SSE"] --> ORCH["agent-orchestrator<br/>LangGraph"]
    UI --> GW["llm-gateway<br/>OpenAI-совместимый /v1"]
    UI --> RAG["rag-pgvector<br/>гибридный поиск"]
    ORCH --> GW
    ORCH --> RAG
    ORCH --> MCP["mcp-tools-server<br/>FastMCP"]
    RAG --> GW
    GW --> P["OpenAI · Anthropic · Ollama<br/>DeepSeek · Qwen · Moonshot"]
```

| Сервис | Что внутри | CI |
|---|---|---|
| [**llm-gateway**](https://github.com/INTERpol21/llm-gateway) | Один OpenAI-совместимый `/v1` к шести провайдерам: маршрутизация с алиасами и цепочками фолбэков, ретраи с full-jitter backoff, circuit breakers, точный и семантический кеш, rate limits и стоимость по ключам, обратимое вырезание персональных данных до провайдера, телеметрия в Postgres и Prometheus | ![ci](https://github.com/INTERpol21/llm-gateway/actions/workflows/ci.yml/badge.svg) |
| [**rag-pgvector**](https://github.com/INTERpol21/rag-pgvector) | Поиск с цитатами `[n]`: гибридный ретривал (pgvector + BM25 / Postgres FTS) со слиянием convex или RRF, реранкер, evals с LLM-as-a-judge | ![ci](https://github.com/INTERpol21/rag-pgvector/actions/workflows/ci.yml/badge.svg) |
| [**agent-orchestrator**](https://github.com/INTERpol21/agent-orchestrator) | Исследовательский агент на LangGraph: plan → execute → reflect → synthesize, параллельный сбор улик, трасса каждого шага, деградация без 500-х, чекпоинты в Postgres | ![ci](https://github.com/INTERpol21/agent-orchestrator/actions/workflows/ci.yml/badge.svg) |
| [**mcp-tools-server**](https://github.com/INTERpol21/mcp-tools-server) | MCP-сервер на FastMCP: веб-поиск, read-only SQL, файловая песочница, `fetch_url` с защитой от SSRF; stdio и streamable HTTP из одной кодовой базы | ![ci](https://github.com/INTERpol21/mcp-tools-server/actions/workflows/ci.yml/badge.svg) |
| [**llm-platform-console**](https://github.com/INTERpol21/llm-platform-console) | Консоль платформы: чат с живой трассой агента по SSE, каталог моделей, расход и стоимость, база знаний; весь стек одной командой | ![ci](https://github.com/INTERpol21/llm-platform-console/actions/workflows/ci.yml/badge.svg) |

## 🚀 Продукты в проде

| Продукт | Что это | Ссылка |
|---|---|---|
| **ERA2** | Экосистема 12+ AI-продуктов в вебе и Telegram на общем ядре | [era2.ai](https://era2.ai) |
| **NeyroHub** | Агрегатор 90+ нейросетей: текст, изображения, видео | [neyrohub.io](https://neyrohub.io) |
| **+Вайб** | ИИ-фотостудия: нейрофотосессия по вашим фото | [vibeplus.ai](https://vibeplus.ai) |
| **iVox Studio** | AI-озвучка и клон голоса: 200+ голосов, 70+ языков | [voice.era2.ai](https://voice.era2.ai) |
| **Music Era2** | Генерация песен и музыки | [music.era2.ai](https://music.era2.ai) |
| **Kefirium** | Первый рублёвый NFT-маркетплейс в РФ | [kefirium.ru](https://kefirium.ru) |
| **Meta Force Space** | Web3-платформа на Polygon, 2M+ пользователей | — |
| **PayQR.Global** | Платёжная B2B-платформа: P2P-сделки, 3+ шлюза | — |
| **Upravhouse · Leverans** | CRM для ЖКХ и доставка еды с CRM колл-центра — соло, от схемы БД до деплоя | — |

## 🧭 Опыт

**Volta Tech · ERA2** — Senior Fullstack → Team Lead → Tech Lead команды 8 · *июль 2025 — июнь 2026*
- Собрал платформенное ядро для 12+ AI-продуктов: gateway на FastAPI над 90+ моделями (роутинг, structured output, tool calling, MCP, фолбэки — неуспешных генераций меньше 1%), асинхронный слой на Celery и Redis/RabbitMQ — отклик API быстрее в 3–4 раза.
- RAG на PostgreSQL + pgvector: HNSW, гибридный поиск с реранкером, evals LLM-as-a-judge — ~120 тыс. чанков, p95 retrieval ~120 мс, точность на эталонном наборе с ~70% до ~90%.
- Кредитный биллинг на 90+ тарифов с ЮKassa и СБП: леджер на PostgreSQL с row-level locking и идемпотентностью, 95%+ успешных транзакций.
- iGaming-платформа: 4 000+ игр от 50+ провайдеров, интеграции с 10+ микросервисами, шина RabbitMQ/Kafka, Redis-кеш — ключевые экраны быстрее на 30–40%; миграция Vue 2 → 3, Playwright + Allure на 100+ сценариев.
- Team Lead Frontend трёх кросс-функциональных команд, затем Tech Lead ERA2: найм, перформанс-ревью, 1:1, архитектура, релизный процесс.

**Competent IT** — Senior Fullstack → Team Lead · *июль 2024 — июль 2025*
- Web3-платформа Meta Force Space (2M+ пользователей, Polygon): fullstack-архитектура на React 18, Vue 3, NestJS и PostgreSQL, MVP в прод меньше чем за 4 месяца.
- Корпоративная дизайн-система на React/Next.js, Tailwind и Storybook: 40+ компонентов, 3+ команды-потребителя, сборка типовых интерфейсов в 2 раза быстрее.

**PR-группа Буржуй** — Fullstack → Tech Lead · *апрель 2022 — июнь 2024*
- Kefirium: highload NFT-маркетплейс на Nuxt (SSR/PWA) и Node.js, смарт-контракты на Solidity, IPFS; ключевые страницы грузятся быстрее 2,5 с.
- Live-аукцион Soda AVS: ставки по WebSocket быстрее 300 мс при сотнях одновременных участников, консистентность через транзакции и row-level блокировки.
- PayQR.Global: транзакционный слой P2P-сделок — ACID, статусные машины, идемпотентные вебхуки, сверки, 3+ платёжных шлюза.

**Routeam** — Frontend (React), проектный контракт · *октябрь 2021 — апрель 2022*
- Модуль склада федеральной аптечной сети: до прода за 7 месяцев, 5 000+ пользователей в сутки, 100 000+ позиций, загрузка быстрее на 40%+.

**ИП Полуэктов** — Fullstack (Vue / Node.js), соло · *август 2020 — октябрь 2021*
- Два продукта от схемы БД до деплоя: CRM для ЖКХ Upravhouse и доставка еды Leverans; Telegram-бот снял с колл-центра ~40% нагрузки.

**Asmart-group** — Frontend · *июнь 2019 — август 2020*
- B2B/B2C-сайты, туристический портал и e-commerce на Vue и Nuxt: Lighthouse 85+, initial bundle меньше на ~40%.

## 🛠 Стек

| | |
|---|---|
| **Backend** | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) ![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![Celery](https://img.shields.io/badge/Celery-37814A?style=flat-square&logo=celery&logoColor=white) ![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white) ![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=flat-square&logo=laravel&logoColor=white) ![gRPC](https://img.shields.io/badge/gRPC-244c5a?style=flat-square&logo=grpc&logoColor=white) ![WebSocket](https://img.shields.io/badge/WebSocket-010101?style=flat-square&logo=socketdotio&logoColor=white) |
| **AI / LLM** | ![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=flat-square&logo=langchain&logoColor=white) ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white) ![MCP](https://img.shields.io/badge/MCP-FastMCP-6E40C9?style=flat-square) ![OpenAI](https://img.shields.io/badge/OpenAI_API-412991?style=flat-square&logo=openai&logoColor=white) ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat-square&logo=anthropic&logoColor=white) ![Ollama](https://img.shields.io/badge/Ollama-000000?style=flat-square&logo=ollama&logoColor=white) ![pgvector](https://img.shields.io/badge/pgvector-RAG-336791?style=flat-square&logo=postgresql&logoColor=white) ![Evals](https://img.shields.io/badge/Evals-LLM--as--a--judge-8A2BE2?style=flat-square) |
| **Frontend** | ![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white) ![Vue](https://img.shields.io/badge/Vue_3-35495E?style=flat-square&logo=vuedotjs&logoColor=4FC08D) ![Nuxt](https://img.shields.io/badge/Nuxt_3-00DC82?style=flat-square&logo=nuxt&logoColor=white) ![Pinia](https://img.shields.io/badge/Pinia-FFD859?style=flat-square&logo=pinia&logoColor=black) ![Redux](https://img.shields.io/badge/Redux_Toolkit-764ABC?style=flat-square&logo=redux&logoColor=white) ![TanStack](https://img.shields.io/badge/TanStack_Query-FF4154?style=flat-square&logo=reactquery&logoColor=white) ![Tailwind](https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white) ![Storybook](https://img.shields.io/badge/Storybook-FF4785?style=flat-square&logo=storybook&logoColor=white) ![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white) |
| **Данные** | ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white) ![ClickHouse](https://img.shields.io/badge/ClickHouse-FFCC01?style=flat-square&logo=clickhouse&logoColor=black) ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white) ![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white) ![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white) ![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white) ![TypeORM](https://img.shields.io/badge/TypeORM-FE0803?style=flat-square&logo=typeorm&logoColor=white) ![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-D71F00?style=flat-square&logo=sqlalchemy&logoColor=white) |
| **Инфраструктура** | ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white) ![GitLab CI](https://img.shields.io/badge/GitLab_CI-FC6D26?style=flat-square&logo=gitlab&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white) ![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat-square&logo=cloudflare&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) |
| **Наблюдаемость и качество** | ![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white) ![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white) ![Sentry](https://img.shields.io/badge/Sentry-362D59?style=flat-square&logo=sentry&logoColor=white) ![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white) ![Jest](https://img.shields.io/badge/Jest-C21325?style=flat-square&logo=jest&logoColor=white) ![Pytest](https://img.shields.io/badge/Pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white) ![Unleash](https://img.shields.io/badge/Unleash-feature_flags-1A4049?style=flat-square) |
| **Web3** | ![Solidity](https://img.shields.io/badge/Solidity-363636?style=flat-square&logo=solidity&logoColor=white) ![Ethers](https://img.shields.io/badge/ethers.js-2535A0?style=flat-square&logo=ethereum&logoColor=white) ![WalletConnect](https://img.shields.io/badge/WalletConnect-3B99FC?style=flat-square&logo=walletconnect&logoColor=white) ![IPFS](https://img.shields.io/badge/IPFS-65C2CB?style=flat-square&logo=ipfs&logoColor=white) ![Polygon](https://img.shields.io/badge/Polygon-7B3FE4?style=flat-square&logo=polygon&logoColor=white) |

## 🧪 Инженерные проекты

| Проект | Что показывает | Стек |
|---|---|---|
| [**Realtime Support Desk**](https://github.com/INTERpol21/realtime-support-desk) | Чат «клиент ↔ оператор» в реальном времени: Centrifugo, история в PostgreSQL, восстановление состояния после перезагрузки, индикатор набора, счётчики непрочитанных | NestJS 11 · Prisma 7 · Next.js 16 · React 19 |
| [**Call Center Platform**](https://github.com/INTERpol21/call-center-platform) | Выдача контактов в PL/pgSQL с `FOR UPDATE SKIP LOCKED` — 20 конкурентных воркеров без единого дубля; вебхуки телефонии с HMAC, изоляция организаций через RLS, LLM-разбор звонка стримом в UI с продолжением по `Last-Event-ID` | FastAPI · asyncpg · PostgreSQL 16 · React |
| [**Notification Hub**](https://github.com/INTERpol21/notification-hub) | Микросервисы доставки уведомлений с гарантиями на каждом шаге: publisher confirms, manual ack, ретраи с backoff, DLQ, идемпотентность по UUID | NestJS · RabbitMQ · Telegram Bot API |
| [**Pawnshop Ledger**](https://github.com/INTERpol21/pawnshop-ledger) | Деньги считает сервер: проценты по тарифу, а e2e-тест на гонку гарантирует, что из пяти параллельных выкупов проходит ровно один | NestJS · TypeORM · PostgreSQL · React |
| [**AB-lab**](https://github.com/INTERpol21/ab-lab) | Лаборатория AI-экспериментов: один Zod-контракт на весь монорепо, Redis-кеш с тегами и атомарной инвалидацией через Lua, Demo Runner на SSE | NestJS 11 · Next.js 16 · Zod · Redis |
| [**Freight Auctions**](https://github.com/INTERpol21/freight-auctions) | SPA грузовых торгов: OpenAPI-контракт и Zod на границе, Feature-Sliced Design, MSW с живым состоянием | React 19 · TanStack Router/Query · Zustand |

## 🧠 Как я работаю

- **Архитектура осознанно.** Решения с последствиями фиксирую в ADR, контракт пишу первым — OpenAPI, Zod, Pydantic — и только потом код по обе стороны. Границы модулей держу по clean architecture на бэке и Feature-Sliced Design на фронте.
- **Надёжность по умолчанию.** Деньги, вебхуки и очереди проектирую под повторы и гонки: транзакции и row-level locking, ключи идемпотентности, ретраи с jitter, circuit breakers, DLQ. Упавшая зависимость портит один шаг, а не весь запрос.
- **Наблюдаемость до прода.** Метрики в Prometheus и Grafana, ошибки и релизы в Sentry, трасса каждого шага там, где логики много. Алерт появляется раньше первого инцидента.
- **Качество, которое проверяется.** Unit, integration и e2e; конкурентные сценарии — отдельными тестами; Playwright и visual regression на фронте; для AI-фич — эталонные наборы и evals, а не «на глаз».
- **Безопасность в дизайне.** RBAC, JWT и OAuth2/OIDC, защита от SSRF, маскирование персональных данных до внешнего провайдера, секреты вне кода.
- **Поставка без героизма.** CI/CD, feature flags, семантические версии и changelog: релиз — рутина, а не событие.
- **Команда.** Найм и собеседования, 1:1 и перформанс-ревью, менторинг, декомпозиция и оценка. Код-ревью — способ растить людей, а не фильтр.
- **AI-native с ответственностью.** Claude Code и Cursor каждый день: агенту — задачу с контекстом и критериями приёмки, результату — ревью и прогон тестов. За итог отвечает инженер.

## 📈 Активность

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/INTERpol21/INTERpol21/output/snake-dark.svg"/>
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/INTERpol21/INTERpol21/output/snake-light.svg"/>
  <img alt="Contribution snake" src="https://raw.githubusercontent.com/INTERpol21/INTERpol21/output/snake-light.svg" width="100%"/>
</picture>

<p align="center">
  <img src="assets/footer.svg" width="100%" alt="Senior Fullstack / Backend · Tech Lead · AI / LLM platforms"/>
</p>

<p align="center">Открыт к ролям <b>Senior Fullstack / Backend</b> и <b>Tech Lead</b>, удалённо или гибрид. Быстрее всего — в <a href="https://t.me/olddeveloper21">Telegram</a>.</p>
