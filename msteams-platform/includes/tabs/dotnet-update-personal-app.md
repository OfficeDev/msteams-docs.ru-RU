## <a name="update-your-application"></a><span data-ttu-id="06ce0-101">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="06ce0-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="06ce0-102">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="06ce0-102">_Layout.cshtml</span></span>

<span data-ttu-id="06ce0-103">Чтобы вкладка отображалась в Teams, необходимо включить Microsoft Teams **клиента JavaScript** и включить вызов после загрузки `microsoftTeams.initialize()` страницы.</span><span class="sxs-lookup"><span data-stu-id="06ce0-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="06ce0-104">Это то, как ваша вкладка и Teams приложение:</span><span class="sxs-lookup"><span data-stu-id="06ce0-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="06ce0-105">Перейдите в **общую** папку, **откройте _Layout.cshtml** и добавьте в раздел `<head>` теги следующее:</span><span class="sxs-lookup"><span data-stu-id="06ce0-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a><span data-ttu-id="06ce0-106">PersonalTab.cshtml</span><span class="sxs-lookup"><span data-stu-id="06ce0-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="06ce0-107">Откройте **PersonalTab.cshtml** и обновите встроенные `<script>` теги, `microsoftTeams.initialize()` позвонив.</span><span class="sxs-lookup"><span data-stu-id="06ce0-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="06ce0-108">Обязательно сохраните обновленный **PersonalTab.cshtml.**</span><span class="sxs-lookup"><span data-stu-id="06ce0-108">Make sure to save your updated **PersonalTab.cshtml**.</span></span>