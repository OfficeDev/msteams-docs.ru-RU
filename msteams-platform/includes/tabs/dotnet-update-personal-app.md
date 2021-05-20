## <a name="update-your-application"></a>Обновление приложения

### <a name="_layoutcshtml"></a>_Layout.cshtml

Для отображения вкладки в Teams вы должны **включить Microsoft Teams JavaScript клиента SDK** и включить вызов `microsoftTeams.initialize()` после загрузки страницы. Вот как ваша вкладка и Teams приложение общаются:

- Перейдите в **общую** папку, **откройте _Layout.cshtml** и добавьте следующее в `<head>` раздел тегов:

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a>PersonalTab.cshtml

Откройте **PersonalTab.cshtml и** обновите встроенные `<script>` теги, позвонив `microsoftTeams.initialize()` .

Убедитесь в том, чтобы сохранить **обновленный PersonalTab.cshtml**.