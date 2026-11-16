# Архитектура CreatePortal 2.0

Статус: проект, без деплоя.

## Предлагаемый стек
React + TypeScript + Vite + PWA; Python FastAPI; отдельная PostgreSQL с миграциями; фоновый воркер с очередью, повторами и дедупликацией; GitHub REST API и webhook HMAC SHA-256. ИИ через сменные адаптеры, с возможностью работы без платного API.

## Модули
Identity, Projects, Sources, Roadmap, Tasks, GitHub, Director, Memory, Approvals, Audit, Notifications, Jobs.

## Сущности
users, sessions, projects, sources, roadmap_versions, tasks, dependencies, assignments, pull_requests, ci_checks, approvals, decisions, context_snapshots, webhook_deliveries, jobs, audit_events, secret_references.

## Безопасность
Чтение разрешено автоматически; черновики директор создаёт сам. Merge, деплой, смена архитектуры, бюджетов и доступов требуют согласования; удаление данных и секретов требуют отдельного явного подтверждения. Токены только в защищённом серверном хранилище, не в Git, БД, логах или LLM-контексте. UI показывает только статус токена. CI fail-closed, события идемпотентны.

## Изоляция
Новый репозиторий, отдельная БД, отдельный процесс и тестовый URL. Старый CreatePortal, NEXUS и LunexEconom не затрагивать. Миграция только после резервной копии, теста восстановления и согласования владельца.

## Требует проверки
Ресурсы VPS, модель доступа, провайдер ИИ, механизм поиска по памяти и политика безопасных слияний.
