## <a name="update-your-application"></a>Обновление приложения

### <a name="_layoutcshtml"></a>_Layout. cshtml

Чтобы вкладка отображалась в Teams, необходимо включить **клиентский пакет SDK Microsoft Teams** для `microsoftTeams.initialize()` JavaScript и включить вызов после загрузки страницы. Это способ общения вкладки и приложения teams:

- Перейдите к **общей** папке, откройте **_layout. cshtml**и добавьте следующий раздел " `<head>` Теги":

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a>Персоналтаб. cshtml

Откройте **персоналтаб. cshtml** и обновите внедренные `<script>` Теги с `microsoftTeams.initialize()`помощью вызова.

Обязательно сохраните обновленный *персоналтаб. cshtml*.