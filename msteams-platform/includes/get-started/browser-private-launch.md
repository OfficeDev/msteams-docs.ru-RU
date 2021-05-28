### <a name="optional-adjust-your-browser-launch-settings"></a>(Необязательный) Настройка параметров запуска браузера

При разработке Teams обычно запускать приложение в другом клиенте разработчика или с альтернативными учетными данными.  И Microsoft Edge, и Google Chrome предоставляют возможности для настройки параметров запуска для браузера.  Например, чтобы обновить проект для поддержки режима InPrivate (Microsoft Edge), откройте `.vscode/launch.json` файл в проекте.  Найми соответствующие параметры запуска и добавьте в каждый из них следующий блок:

``` json
"runtimeArgs": [ "--inprivate" ]
```

Например, параметр запуска для локального запуска выглядит так:

``` json
{
   "name": "Start and Attach to Frontend (Edge)",
   "type": "pwa-msedge",
   "request": "launch",
   "url": "https://teams.microsoft.com/_#/l/app/${localTeamsAppId}?installAppPackage=true",
   "preLaunchTask": "Start Frontend",
   "postDebugTask": "Stop All Services",
   "presentation": {
         "group": "all",
         "hidden": true
   },
   "runtimeArgs": [ "--inprivate" ]
},
```

Кроме того, можно настроить браузер для использования последнего известного профиля. [Создайте новый профиль](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) в Microsoft Edge.  Затем настройть параметры, чтобы использовать последний известный профиль для новых ссылок:

- В Microsoft Edge откройте `edge://settings/profiles/multiProfileSettings` .
- **Отключите автоматическое переключение профиля.**
- Для профиля **по умолчанию для внешних ссылок** выберите **Last used (default).**

Убедитесь, что браузер открыт для правильного профиля перед отладки приложения.
