# SwiftUI Project Template

Стартовый набор `.cursor/rules/` для новых SwiftUI-проектов. Содержит минимум — только то, что **специфично для проекта** и не дублирует мои глобальные User Rules в Cursor.

## Requirements

- **Cursor** — для использования включённых `.cursor/rules/`.
- **Xcode 16+** — соответствует baseline (Swift 6, iOS 17+).
- **SwiftLint** *(опционально)* — для применения `.swiftlint.yml`. Установка: `brew install swiftlint`.

## Stack baseline

- iOS 17+
- Swift 6
- `@Observable` (вместо `ObservableObject` + `@Published`)
- `NavigationStack` (вместо `NavigationView`)
- SwiftData (`@Model`, `@Query`, `ModelContainer`)
- Swift Concurrency (`async/await`, `actor`, `@MainActor`)

## Что внутри

```
.cursor/
  rules/
    00-baseline.mdc       # alwaysApply — версии iOS/Swift, разрешённые/запрещённые API
    10-architecture.mdc   # шаблон под архитектуру (MV / IVO), структура папок
    20-api.mdc            # шаблон под бэкенд (base URL, auth, эндпойнты)
    30-ai-marker.mdc      # alwaysApply — конвенция маркера AI-генерации
.swiftlint.yml             # рабочий конфиг SwiftLint
.gitignore                 # стандартный iOS-вариант
```

## Как использовать в новом проекте

### Вариант 1: клонировать как стартер

```bash
git clone https://github.com/Vladimir-Br/swiftui-project-template.git my-new-app
cd my-new-app
rm -rf .git
git init
git add .
git commit -m "chore: initial commit from swiftui-project-template"
```

### Вариант 2: скопировать только правила в существующий Xcode-проект

```bash
cp -R /path/to/swiftui-project-template/.cursor /path/to/my-existing-app/
cp /path/to/swiftui-project-template/.swiftlint.yml /path/to/my-existing-app/
```

## Что сделать сразу после копирования

1. Открыть `.cursor/rules/00-baseline.mdc` → проверить iOS-таргет и версию Swift под этот проект.
2. Открыть `.cursor/rules/10-architecture.mdc` → отметить выбранный паттерн (MV / IVO), заполнить структуру папок.
3. Открыть `.cursor/rules/20-api.mdc`:
   - Если проект **с сетью** — заполнить base URL, схему авторизации, основные эндпойнты.
   - Если проект **офлайн (без бэкенда)** — **удалить файл целиком**.
4. Проверить `.swiftlint.yml` под нужды проекта (по умолчанию: `line_length: 140`).
5. Убедиться, что `Package.resolved` НЕ игнорируется (для app-проектов он должен коммититься).
6. Удалить блоки `TODO`, которые не относятся к проекту.

## Чего здесь НЕТ намеренно

Эти вещи покрыты моими **глобальными User Rules** в Cursor — нет смысла дублировать:
- паттерны IVO/MV в деталях
- правила SwiftData и Swift Concurrency
- Apple API Design Guidelines
- mentor-persona

Если что-то из этого меняется на уровне конкретного проекта — добавляй override в `.cursor/rules/`.

## Поддержание трекинга AI-кода

Правило `30-ai-marker.mdc` просит ассистента помечать большие AI-сгенерированные файлы. Чтобы найти такие файлы:

```bash
rg "AI-Generated, needs human review" --type swift
```

Сел, разобрался, отрефакторил, удалил маркер — повторяй.

## Источник идеи

Подход «codified project context for LLM» подсмотрен у Яндекса:
- [Habr: За два месяца вместо года](https://habr.com/ru/companies/yandex/articles/1028494/)
- [GitHub: yandex/migration-toolkit-for-swift](https://github.com/yandex/migration-toolkit-for-swift)

Их toolkit сфокусирован на миграции ObjC → Swift; здесь — облегчённый аналог для greenfield SwiftUI-проектов.

## License

MIT — см. [LICENSE](LICENSE).
