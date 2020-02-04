## <a name="update-your-application"></a><span data-ttu-id="978e3-101">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="978e3-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="978e3-102">_Layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="978e3-102">_Layout.cshtml</span></span>

<span data-ttu-id="978e3-103">Чтобы вкладка отображалась в Teams, необходимо включить **клиентский пакет SDK Microsoft Teams** для `microsoftTeams.initialize()` JavaScript и включить вызов после загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="978e3-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="978e3-104">Это способ общения вкладки и приложения teams:</span><span class="sxs-lookup"><span data-stu-id="978e3-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="978e3-105">Перейдите к **общей** папке, откройте **_layout. cshtml**и добавьте следующий раздел " `<head>` Теги":</span><span class="sxs-lookup"><span data-stu-id="978e3-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a><span data-ttu-id="978e3-106">Персоналтаб. cshtml</span><span class="sxs-lookup"><span data-stu-id="978e3-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="978e3-107">Откройте **персоналтаб. cshtml** и обновите внедренные `<script>` Теги с `microsoftTeams.initialize()`помощью вызова.</span><span class="sxs-lookup"><span data-stu-id="978e3-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="978e3-108">Обязательно сохраните обновленный *персоналтаб. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="978e3-108">Make sure to save your updated *PersonalTab.cshtml*.</span></span>