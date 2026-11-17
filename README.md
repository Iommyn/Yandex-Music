# Yandex Music Visualizer for hexlet
Яндекс Музыка в визуализации Хекслета

Yandex Music Visualizer - это веб-приложение для прослушивание музыки в визуализации Хекслета. Пет-проект будет состоять из экосистемы хекслета и подстроен под ui/ux hexlet

Приложение будет делать следующее: Статистика, что было прослушено. Доступ к экосистеме хекслета. Музыка для технарей). Авторизация/Регистрации и выбор вкуса.
Песни будут статически, то есть всего будет 15 песен на разные вкусы


Структура проекта (FSD). Будет архитектура Figute Sliced Design, нужно для того, чтобы была четкая иерархия, на подобие чистой архитектуры. В будущем будет удобно расширять функционал проекта

src/
├── app/                          # Инициализация: провайдеры, роутер, глобальные стили
│   ├── providers/                # AuthProvider (гидратация из localStorage), ThemeProvider
│   ├── styles/                   # Глобальные CSS-переменные Хекслета, reset
│   ├── router/                   # Конфигурация маршрутов + ProtectedRoute
│   └── index.tsx                 # Точка входа
│
├── pages/                        # Страницы-маршруты
│   ├── login/                    # /login — форма входа
│   │   ├── ui/LoginPage.tsx
│   │   └── index.ts
│   ├── register/                 # /register — форма регистрации
│   │   ├── ui/RegisterPage.tsx
│   │   └── index.ts
│   ├── taste-selection/          # /taste — выбор вкуса
│   │   ├── ui/TasteSelectionPage.tsx
│   │   └── index.ts
│   ├── player/                   # /player — плеер + список треков
│   │   ├── ui/PlayerPage.tsx
│   │   └── index.ts
│   ├── stats/                    # /stats — дашборд статистики
│   │   ├── ui/StatsPage.tsx
│   │   └── index.ts
│   └── not-found/                # 404
│       └── ui/NotFoundPage.tsx
│
├── widgets/                      # Крупные блоки, композиция фич и сущностей
│   ├── header/                   # Шапка в стиле Хекслета: лого, навигация, профиль
│   │   ├── ui/Header.tsx
│   │   └── index.ts
│   ├── track-list/               # Список треков выбранного вкуса
│   │   ├── ui/TrackList.tsx
│   │   └── index.ts
│   ├── player-bar/               # Нижняя панель плеера (play/pause, прогресс, громкость)
│   │   ├── ui/PlayerBar.tsx
│   │   └── index.ts
│   ├── stats-summary/            # Карточки: всего треков, время, топ-3
│   │   ├── ui/StatsSummary.tsx
│   │   └── index.ts
│   └── listening-history/        # Таблица последних прослушиваний
│       ├── ui/ListeningHistory.tsx
│       └── index.ts
│
├── features/                     # Действия пользователя
│   ├── auth-by-email/            # Логин: форма, валидация, запись в localStorage
│   │   ├── ui/LoginForm.tsx
│   │   ├── model/useLogin.ts
│   │   └── index.ts
│   ├── register-user/            # Регистрация: форма, валидация, создание пользователя
│   │   ├── ui/RegisterForm.tsx
│   │   ├── model/useRegister.ts
│   │   └── index.ts
│   ├── select-taste/             # Выбор вкуса: карточки вкусов, сохранение выбора
│   │   ├── ui/TasteCard.tsx
│   │   ├── model/useSelectTaste.ts
│   │   └── index.ts
│   ├── player-controls/          # Управление аудио: play, pause, seek, volume, next/prev
│   │   ├── ui/PlayButton.tsx
│   │   ├── ui/ProgressBar.tsx
│   │   ├── model/useAudio.ts     # Единственное место работы с HTML5 Audio
│   │   └── index.ts
│   ├── track-progress/           # Отслеживание события timeupdate → запись в статистику
│   │   ├── model/useTrackProgress.ts
│   │   └── index.ts
│   └── toggle-like/              # Лайк/дизлайк трека (опционально)
│       ├── ui/LikeButton.tsx
│       ├── model/useLike.ts
│       └── index.ts
│
├── entities/                     # Бизнес-сущности (данные + базовая UI)
│   ├── user/                     # Пользователь: email, имя, выбранный вкус
│   │   ├── model/user.ts         # Zod-схема, тип
│   │   ├── model/userStore.ts    # Zustand  стор + гидратация из localStorage
│   │   └── index.ts
│   ├── track/                    # Трек id, title, artist, taste, duration, src
│   │   ├── model/track.ts        # Zod-схема, тип
│   │   ├── ui/TrackRow.tsx
│   │   └── index.ts
│   ├── taste/                    # Вкус id, name, description, cover
│   │   ├── model/taste.ts
│   │   ├── ui/TasteBadge.tsx
│   │   └── index.ts
│   └── listening-session/        # Сессия прослушивания trackId, timestamp, duration
│       ├── model/session.ts      # Zod схема
│       ├── model/sessionStore.ts # Zustand стор истории прослушиваний
│       └── index.ts
│
└── shared/                       # Инфраструктура без знания о домене
    ├── ui/                       # UI-кит в стиле Хекслета: Button, Card, Input, Spinner
    │   ├── button/
    │   ├── card/
    │   ├── input/
    │   └── index.ts
    ├── lib/                      # Утилиты: formatDuration, formatDate, groupBy
    │   ├── date/
    │   ├── format/
    │   └── index.ts
    ├── config/                   # Константы: тема Хекслета, список треков, вкусы, ключи localStorage
    │   ├── theme.ts              # Цвета, шрифты, отступы
    │   ├── tracks.ts             # 15 треков с метаданными
    │   ├── tastes.ts             # Список вкусов
    │   ├── routes.ts             # Пути маршрутов
    │   └── index.ts
    └── storage/                  # Обёртка над localStorage с Zod-валидацией
        ├── localStorage.ts
        └── index.ts


Схема зависимостей
app -> pages -> widgets -> features -> entities -> shared
Импорт только вниз по цепочке. shared не знает о домене. entities не знает о features


Запуск

git clone <repo-url>
cd yandex-music-visualizer-hexlet
npm install
npm run dev


        
