# OpenClaw — Русская локализация (Russian Locale)

Добавляет полноценную русскую локализацию в панель управления OpenClaw Control UI.

## Что включено

- **Полный перевод** всех строк интерфейса на русский язык (1200+ строк)
- **Автоматическое определение** русского языка браузером
- **Интеграция** с системой i18n OpenClaw (lazy loading)

## Установка

### Вариант 1: Применить патч к исходникам

1. Клонируйте репозиторий OpenClaw:
   ```bash
   git clone https://github.com/openclaw/openclaw.git
   cd openclaw
   ```

2. Примените патч:
   ```bash
   git apply openclaw-ru.patch
   ```

3. Установите зависимости и соберите:
   ```bash
   pnpm install
   pnpm build
   ```

4. Установите глобально:
   ```bash
   npm install -g .
   ```

### Вариант 2: Ручная установка файлов

Скопируйте файлы из `src/` в соответствующие директории исходного кода OpenClaw:

| Файл из этого репозитория | Куда скопировать |
|---------------------------|------------------|
| `src/ui/i18n/locales/ru.ts` | `openclaw/ui/src/i18n/locales/ru.ts` |
| `src/ui/i18n/lib/types.ts` | `openclaw/ui/src/i18n/lib/types.ts` |
| `src/ui/i18n/lib/registry.ts` | `openclaw/ui/src/i18n/lib/registry.ts` |

Затем добавьте запись в `scripts/control-ui-i18n.ts`:
```typescript
{ locale: "ru", fileName: "ru.ts", exportName: "ru", languageKey: "ru" },
```

## Использование

После установки:

1. Откройте панель управления OpenClaw (`openclaw dashboard`)
2. Перейдите в **Settings** → **Language**
3. Выберите **Русский (русский)**

Или установите язык через CLI:
```bash
openclaw config set ui.language ru
```

## Что переведено

- Все секции: навигация, чат, сессии, каналы, агенты, крон-задания
- Настройки: конфигурация, внешний вид, автоматизация
- Журналы, отладка, использование
- Формы, уведомления, сообщения об ошибках

## Технические детали

### Изменённые файлы

1. **`ui/src/i18n/locales/ru.ts`** — Новый файл, полный перевод всех строк
2. **`ui/src/i18n/lib/types.ts`** — Добавлен `"ru"` в тип `Locale`
3. **`ui/src/i18n/lib/registry.ts`** — Добавлен:
   - `"ru"` в массив `LAZY_LOCALES`
   - Регистрация загрузчика в `LAZY_LOCALE_REGISTRY`
   - Автоопределение `ru` в `resolveNavigatorLocale()`
4. **`scripts/control-ui-i18n.ts`** — Добавлен `ru` в `LOCALE_ENTRIES`

### Архитектура

Русский язык загружается по требованию (lazy loading) — файл `ru.ts` (~52 KB) загружается только при выборе языка, не увеличивая основной бандл.

## Скриншот

![Russian locale screenshot](screenshot.png)

## Лицензия

Перевод распространяется под той же лицензией, что и OpenClaw.

## Автор

Перевод создан для проекта ООО «Конструктор» (konstruktor55.ru)
