## <a name="update-your-application"></a><span data-ttu-id="71e30-101">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="71e30-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="71e30-102">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="71e30-102">_Layout.cshtml</span></span>

<span data-ttu-id="71e30-103">Для отображения вкладки в Teams вы должны **включить Microsoft Teams JavaScript клиента SDK** и включить вызов `microsoftTeams.initialize()` после загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="71e30-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="71e30-104">Вот как ваша вкладка и Teams приложение общаются:</span><span class="sxs-lookup"><span data-stu-id="71e30-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="71e30-105">Перейдите в **общую** папку, **откройте _Layout.cshtml** и добавьте следующее в `<head>` раздел тегов:</span><span class="sxs-lookup"><span data-stu-id="71e30-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a><span data-ttu-id="71e30-106">PersonalTab.cshtml</span><span class="sxs-lookup"><span data-stu-id="71e30-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="71e30-107">Откройте **PersonalTab.cshtml и** обновите встроенные `<script>` теги, позвонив `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="71e30-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="71e30-108">Убедитесь в том, чтобы сохранить **обновленный PersonalTab.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="71e30-108">Make sure to save your updated **PersonalTab.cshtml**.</span></span>