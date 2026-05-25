# iOS Build — ПрофКвест СКФ МТУСИ

## Требования

- macOS (обязательно для Xcode)
- Xcode 15+ ([App Store](https://apps.apple.com/app/xcode/id497799835))
- Node.js 18+ (`brew install node`)
- CocoaPods (`sudo gem install cocoapods`)
- Apple Developer аккаунт (для реального устройства / публикации)

---

## Шаг 1 — Установка зависимостей

```bash
cd d:/AI/projects/F.W.A/profkvest
npm install
```

---

## Шаг 2 — Инициализация Capacitor iOS платформы

```bash
npx cap add ios
```

Это создаст папку `ios/` с полным Xcode-проектом.

---

## Шаг 3 — Синхронизация веб-файлов

```bash
npx cap copy ios
npx cap sync ios
```

Выполнять **каждый раз** после изменений в `index.html`.

---

## Шаг 4 — Открыть в Xcode

```bash
npx cap open ios
```

---

## Шаг 5 — Настройка в Xcode

### 5.1 Иконка приложения
- В Xcode: `Assets.xcassets → AppIcon`
- Добавить иконку 1024×1024px (фон #372579, белый текст ПрофКвест + 🎓)
- Инструмент для генерации всех размеров: [appicon.co](https://appicon.co)

### 5.2 Splash Screen
- `App → Info → Custom iOS Target Properties`
- Уже настроен через `capacitor.config.json`

### 5.3 Bundle Identifier
- Target → Signing & Capabilities
- Bundle Identifier: `ru.mtuci.skf.profkvest`
- Team: выбери свой Apple Developer Team

### 5.4 Display Name
- Уже задан `ПрофКвест` в `capacitor.config.json`

---

## Шаг 6 — Сборка и запуск

### Симулятор
```
Xcode → Product → Run (⌘R)
```
Выбрать симулятор: iPhone 15 / iPhone 16

### Реальное устройство
1. Подключить iPhone
2. В Xcode выбрать устройство в топбаре
3. `Product → Run`

---

## Шаг 7 — Публикация в App Store

### 7.1 Сборка архива
```
Xcode → Product → Archive
```

### 7.2 Загрузка в App Store Connect
```
Xcode Organizer → Distribute App → App Store Connect
```

### 7.3 App Store Connect
- Создать новое приложение на [appstoreconnect.apple.com](https://appstoreconnect.apple.com)
- Bundle ID: `ru.mtuci.skf.profkvest`
- Заполнить описание, скриншоты (6.7" и 6.1")
- Отправить на Review

---

## Скриншоты для App Store

Сделать на симуляторе iPhone 15 Pro Max (6.7"):
1. Главный экран с RIASEC-описанием
2. Экран симуляции (задача программиста)
3. Экран с объяснением ответа
4. Экран результатов (радар-график)
5. Экран достижений

---

## Быстрый rebuild после правок

```bash
# Каждый раз когда изменяешь index.html:
npm run ios:sync
# Потом в Xcode: ⌘R
```

---

## Info.plist — дополнительные настройки

Добавить в `ios/App/App/Info.plist` если нужно:

```xml
<!-- Разрешение на доступ к сети -->
<key>NSAppTransportSecurity</key>
<dict>
  <key>NSAllowsArbitraryLoads</key>
  <false/>
</dict>

<!-- Отключить масштабирование -->
<key>UIViewControllerBasedStatusBarAppearance</key>
<false/>
```

---

## Структура проекта после `cap add ios`

```
profkvest/
├── index.html          ← основной файл приложения
├── package.json
├── capacitor.config.json
└── ios/
    └── App/
        ├── App/
        │   ├── AppDelegate.swift
        │   ├── Info.plist
        │   └── Assets.xcassets/  ← иконки сюда
        ├── App.xcodeproj
        └── Podfile
```
