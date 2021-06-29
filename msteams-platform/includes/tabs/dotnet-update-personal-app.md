## <a name="update-your-application"></a>Обновление приложения

### <a name="_layoutcshtml"></a>_Layout.cshtml

Чтобы вкладка отображалась в Teams, необходимо включить Microsoft Teams **клиента JavaScript** и включить вызов после загрузки `microsoftTeams.initialize()` страницы. Это то, как ваша вкладка и Teams приложение:

Перейдите в **общую** папку, **откройте _Layout.cshtml** и добавьте в раздел `<head>` теги следующее:

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

### <a name="personaltabcshtml"></a>PersonalTab.cshtml

Откройте **PersonalTab.cshtml** и обновите встроенные `<script>` теги, `microsoftTeams.initialize()` позвонив.

Сохраните обновленный **файл PersonalTab.cshtml.**