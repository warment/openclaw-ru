# OpenClaw — Русская локализация (Russian Locale)

[![PR to OpenClaw](https://img.shields.io/badge/PR%20to%20OpenClaw-%2376184-blue)](https://github.com/openclaw/openclaw/pull/76184)
[![Issue](https://img.shields.io/badge/Issue-%2376178-green)](https://github.com/openclaw/openclaw/issues/76178)
[![License](https://img.shields.io/badge/License-OpenClaw-orange)](LICENSE)

Полноценная русская локализация панели управления [OpenClaw](https://github.com/openclaw/openclaw) Control UI.

## Что включено

- **Полный перевод** всех строк интерфейса на русский язык (1200+ строк)
- **Автоматическое определение** русского языка браузером
- **Интеграция** с системой i18n OpenClaw (lazy loading)

## Что переведено

| Секция | Описание |
|--------|----------|
| Навигация | Чат, Управление, Агент, Настройки |
| Сессии | Активные ключи, токены, сжатие, контрольные точки |
| Каналы | Состояние, конфигурация, профили |
| Агенты | Рабочие пространства, файлы, инструменты, навыки |
| Cron | Расписание, задания, история запусков |
| Настройки | Конфигурация, внешний вид, автоматизация |
| Использование | Токены, стоимость, фильтры, экспорт |
| Сны | Консолидация памяти, дневник, статистика |
| Формы | Уведомления, сообщения об ошибках, валидация |

## Установка

### Вариант 1: Применить патч (рекомендуется)

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
git apply openclaw-ru.patch
pnpm install
pnpm build
npm install -g .
```

### Вариант 2: Ручная установка

Скопируйте файлы:

| Исходник | Назначение |
|----------|------------|
| `src/ui/i18n/locales/ru.ts` | `openclaw/ui/src/i18n/locales/ru.ts` |
| `src/ui/i18n/lib/types.ts` | `openclaw/ui/src/i18n/lib/types.ts` |
| `src/ui/i18n/lib/registry.ts` | `openclaw/ui/src/i18n/lib/registry.ts` |

Добавьте в `scripts/control-ui-i18n.ts`:
```typescript
{ locale: "ru", fileName: "ru.ts", exportName: "ru", languageKey: "ru" },
```

Затем:
```bash
pnpm install
pnpm build
npm install -g .
```

## Использование

1. Откройте панель управления: `openclaw dashboard`
2. Перейдите в **Settings** → **Language**
3. Выберите **Русский (русский)**

Или через CLI:
```bash
openclaw config set ui.language ru
```

## Технические детали

### Изменённые файлы

1. **`ui/src/i18n/locales/ru.ts`** — Новый файл (1200+ строк)
2. **`ui/src/i18n/lib/types.ts`** — Добавлен `"ru"` в тип `Locale`
3. **`ui/src/i18n/lib/registry.ts`** — Добавлен:
   - `"ru"` в массив `LAZY_LOCALES`
   - Регистрация загрузчика в `LAZY_LOCALE_REGISTRY`
   - Автоопределение `ru` в `resolveNavigatorLocale()`
4. **`scripts/control-ui-i18n.ts`** — Добавлен `ru` в `LOCALE_ENTRIES`

### Архитектура

Русский язык загружается по требованию (lazy loading) — файл `ru.ts` (~52 KB) загружается только при выборе языка, не увеличивая основной бандл.

## PR в основной репозиторий

Создан [Pull Request #76184](https://github.com/openclaw/openclaw/pull/76184) для включения русского языка в официальный OpenClaw.

## Лицензия

Перевод распространяется под той же лицензией, что и [OpenClaw](https://github.com/openclaw/openclaw).

## Автор

Перевод создан для проекта ООО «Конструктор» (konstruktor55.ru)
