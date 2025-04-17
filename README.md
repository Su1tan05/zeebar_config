## Локальное подключение зависимостей (React, Zebar и др.)

Вместо загрузки зависимостей из удалённых CDN (например, https://esm.sh), можно собрать весь код и зависимости локально, чтобы обеспечить офлайн-доступ, стабильность и контроль версий.

### Шаги:

1. **Инициализировать npm-проект:**

   ```bash
   npm init -y
   ```

2. **Установить необходимые зависимости:**

   ```bash
   npm install react react-dom zebar
   ```

3. **Создать точку входа (например, `src/index.jsx`) и перенести туда весь React-код:**

   ```jsx
   import React, { useState, useEffect } from 'react';
   import { createRoot } from 'react-dom/client';
   import * as zebar from 'zebar';

   function App() {
     // ... твой React-код
   }

   createRoot(document.getElementById('root')).render(<App />);
   ```

4. **Установить сборщик (Esbuild) и добавить скрипт сборки в `package.json`:**

   Установка:
   ```bash
   npm install --save-dev esbuild
   ```

   Добавить в `package.json`:

   ```json
   "scripts": {
     "build": "esbuild src/index.jsx --bundle --outfile=resources/bundle.js --platform=browser --format=esm"
   }
   ```

5. **Собрать проект:**

   ```bash
   npm run build
   ```

   В результате будет создан локальный бандл `resources/bundle.js`, включающий все зависимости.

6. **Изменить HTML-файл:**

   Удалить внешние CDN-ссылки, например:
   ```html
   <script src="https://esm.sh/react@18?dev"></script>
   ```

   Заменить на:

   ```html
   <script type="module" src="./resources/bundle.js"></script>
   ```
