---
title: Добавление тестовых данных в тестовый клиент Microsoft 365
description: Настройка подписки на программу разработчика Office 365 для успешного тестирования приложений Microsoft Teams
ms.topic: how-to
keywords: тестирование групп программ разработчика приложений
ms.date: 11/01/2019
ms.openlocfilehash: 9e23b9054f45ccff6c08b97c72f4d5375fef58ea
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634722"
---
# <a name="add-test-data-to-your-microsoft-365-test-tenant"></a><span data-ttu-id="08de3-104">Добавление тестовых данных в тестовый клиент Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="08de3-104">Add test data to your Microsoft 365 test tenant</span></span>

<span data-ttu-id="08de3-105">С подпиской на разработчика Microsoft 365 вы можете использовать приложение Microsoft Teams с группами тестирования, каналами и пользователями.</span><span class="sxs-lookup"><span data-stu-id="08de3-105">With a Microsoft 365 developer subscription, you can use your Microsoft Teams app with test teams, channels, and users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08de3-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="08de3-106">Prerequisites</span></span>

1. <span data-ttu-id="08de3-107">[Присоединяйтесь к программе разработчиков Microsoft 365,](/office/developer-program/office-365-developer-program)если у вас нет тестового клиента.</span><span class="sxs-lookup"><span data-stu-id="08de3-107">[Join the Microsoft 365 Developer Program](/office/developer-program/office-365-developer-program), if you do not have a test tenant.</span></span>
2. <span data-ttu-id="08de3-108">[Настройка подписки на разработчика Microsoft 365.](/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="08de3-108">[Set up a Microsoft 365 Developer Subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>
3. <span data-ttu-id="08de3-109">[Используйте примеры пакетов данных с подпиской на разработчика Microsoft 365 для установки пакета контента Пользователей.](/office/developer-program/install-sample-packs)</span><span class="sxs-lookup"><span data-stu-id="08de3-109">[Use sample data packs with your Microsoft 365 developer subscription to install the Users content pack](/office/developer-program/install-sample-packs).</span></span>
4. <span data-ttu-id="08de3-110">[Установите модуль Teams PowerShell.](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)</span><span class="sxs-lookup"><span data-stu-id="08de3-110">[Install the Teams PowerShell module](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2).</span></span>
5. <span data-ttu-id="08de3-111">[Установите модуль Azure AD PowerShell.](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="08de3-111">[Install the Azure AD PowerShell module](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true).</span></span>

> [!NOTE]
> <span data-ttu-id="08de3-112">Для любого клиента, который вы используете, необходимо получить разрешения глобального администратора для запуска сценариев.</span><span class="sxs-lookup"><span data-stu-id="08de3-112">For any tenant that you use, you must get the global administrator permissions to run the scripts.</span></span>

## <a name="enable-custom-app-sideloading"></a><span data-ttu-id="08de3-113">Включить настраиваемую загрузку приложений</span><span class="sxs-lookup"><span data-stu-id="08de3-113">Enable custom app sideloading</span></span>

<span data-ttu-id="08de3-114">Включение настраиваемой загрузки приложений необязательно.</span><span class="sxs-lookup"><span data-stu-id="08de3-114">Enabling custom app sideloading is optional.</span></span> <span data-ttu-id="08de3-115">По умолчанию только глобальные администраторы или администраторы служб Teams могут загружать настраиваемые приложения в каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="08de3-115">By default, only global admins or Teams service admins can upload custom apps into the tenant app catalog.</span></span> <span data-ttu-id="08de3-116">Вы также можете разрешить пользователям загружать настраиваемые приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="08de3-116">You can also allow users to upload custom apps to Teams.</span></span> <span data-ttu-id="08de3-117">Дополнительные сведения см. в [сведениях об управлении политиками установки приложений в Teams.](/microsoftteams/teams-app-setup-policies)</span><span class="sxs-lookup"><span data-stu-id="08de3-117">For more information, see [manage app setup policies in Teams](/microsoftteams/teams-app-setup-policies).</span></span>

## <a name="create-teams-and-channels"></a><span data-ttu-id="08de3-118">Создание команд и каналов</span><span class="sxs-lookup"><span data-stu-id="08de3-118">Create teams and channels</span></span>

1. <span data-ttu-id="08de3-119">Сохраните следующий фрагмент в качестве **файла .xml** и обратите внимание на путь файла.</span><span class="sxs-lookup"><span data-stu-id="08de3-119">Save the following snippet as a **.xml** file and note the file path.</span></span> <span data-ttu-id="08de3-120">Этот XML определяет структуру команды и канала, созданного вместе с ее участниками:</span><span class="sxs-lookup"><span data-stu-id="08de3-120">This XML defines the structure of the team and channel that is created along with its members:</span></span>

    ```xml
    <?xml version="1.0"?>
    <Teams>
      <Team Name="Store Portal" ID="storeportal" Description="" Type="Private" Creator="admin">
        <Members>
          <Member UserName="AlexW" IsOwner="false"/>
          <Member UserName="PattiF" IsOwner="false"/>
          <Member UserName="PradeepG" IsOwner="false"/>
          <Member UserName="JoniS" IsOwner="false"/>
          <Member UserName="JohannaL" IsOwner="false"/>
          <Member UserName="NestorW" IsOwner="false"/>
          <Member UserName="IsaiahL" IsOwner="false"/>
          <Member UserName="AdeleV" IsOwner="false"/>
          <Member UserName="LeeG" IsOwner="false"/>
          <Member UserName="MeganB" IsOwner="true"/>
          <Member UserName="LynneR" IsOwner="false"/>
          <Member UserName="GradyA" IsOwner="false"/>
          <Member UserName="LidiaH" IsOwner="false"/>
          <Member UserName="DiegoS" IsOwner="false"/>
          <Member UserName="MiriamG" IsOwner="true"/>
        </Members>
        <Channels>
          <Channel Name="Sales" ID="sales" Description="" Creator="Admin" />
          <Channel Name="Inventory" ID="inventory" Description="" Creator="Admin" />
          <Channel Name="Los Angeles Store 239" ID="losangelesstore239" Description="" Creator="Admin" />
          <Channel Name="Seattle Store 121" ID="seattlestore121" Description="" Creator="Admin" />
          <Channel Name="Online" ID="online" Description="" Creator="Admin" />
          <Channel Name="Store Layout" ID="storelayout" Description="" Creator="Admin" />
          <Channel Name="Promotions" ID="promotions" Description="" Creator="Admin" />
        </Channels>
      </Team>
      <Team Name="Mark 8 Project Team" ID="Mark8ProjectTeam" Description="Welcome to the team that we've assembled to create the Mark 8." Type="Private" Creator="admin">
        <Members>
          <Member UserName="meganb" IsOwner="true" />
          <Member UserName="alexw" IsOwner="false" />
          <Member UserName="lynner" IsOwner="false" />
          <Member UserName="isaiahl" IsOwner="false" />
          <Member UserName="leeg" IsOwner="false" />
          <Member UserName="pradeepg" IsOwner="false" />
          <Member UserName="lidiah" IsOwner="false" />
          <Member UserName="diegos" IsOwner="false" />
          <Member UserName="johannal" IsOwner="false" />
          <Member UserName="miriamg" IsOwner="false" />
          <Member UserName="adelev" IsOwner="false" />
          <Member UserName="jonis" IsOwner="false" />
          <Member UserName="nestorw" IsOwner="false" />
          <Member UserName="gradya" IsOwner="false" />
          <Member UserName="pattif" IsOwner="false" />
        </Members>
        <Channels>
          <Channel Name="Research and Development" ID="researchanddevelopment" Description="Channel for Research and Development!" Creator="meganb" />
          <Channel Name="Design" ID="design" Description="Discuss design projects." Creator="meganb" />
          <Channel Name="Digital Assets Web" ID="digitalassetsweb" Description="Discuss digital assets." Creator="meganb" />
          <Channel Name="Go to Market Plan" ID="gotomarketplan" Description="Our go-to-market plan!" Creator="meganb" />
        </Channels>
      </Team>
      <Team Name="District 9 Road Safety Audit" ID="district9roadsafetyaudit" Description="" Type="Private" Creator="admin">
        <Members>
          <Member UserName="meganb" IsOwner="true" />
          <Member UserName="alexw" IsOwner="false" />
          <Member UserName="lynner" IsOwner="false" />
          <Member UserName="isaiahl" IsOwner="false" />
          <Member UserName="leeg" IsOwner="false" />
          <Member UserName="pradeepg" IsOwner="false" />
          <Member UserName="lidiah" IsOwner="false" />
          <Member UserName="diegos" IsOwner="false" />
          <Member UserName="johannal" IsOwner="false" />
          <Member UserName="miriamg" IsOwner="false" />
          <Member UserName="adelev" IsOwner="false" />
          <Member UserName="jonis" IsOwner="false" />
          <Member UserName="nestorw" IsOwner="false" />
          <Member UserName="gradya" IsOwner="false" />
          <Member UserName="pattif" IsOwner="false" />
        </Members>
        <Channels>
          <Channel Name="Audit Planning" ID="auditplanning" Description="" Creator="Admin" />
          <Channel Name="Delivery" ID="delivery" Description="" Creator="Admin" />
          <Channel Name="Findings" ID="findings" Description="" Creator="Admin" />
          <Channel Name="Recommended Actions" ID="recommendedactions" Description="" Creator="Admin" />
          <Channel Name="Survey" ID="survey" Description="" Creator="Admin" />
        </Channels>
      </Team>
      <Team Name="ACC-1000 Product Team" ID="acc1000productteam" Description="" Type="Private" Creator="admin" >
        <Members>
          <Member UserName="meganb" IsOwner="true" />
          <Member UserName="alexw" IsOwner="false" />
          <Member UserName="lynner" IsOwner="false" />
          <Member UserName="isaiahl" IsOwner="false" />
          <Member UserName="leeg" IsOwner="false" />
          <Member UserName="pradeepg" IsOwner="false" />
          <Member UserName="lidiah" IsOwner="false" />
          <Member UserName="diegos" IsOwner="false" />
          <Member UserName="johannal" IsOwner="false" />
          <Member UserName="miriamg" IsOwner="false" />
          <Member UserName="adelev" IsOwner="false" />
          <Member UserName="jonis" IsOwner="false" />
          <Member UserName="nestorw" IsOwner="false" />
          <Member UserName="gradya" IsOwner="false" />
          <Member UserName="pattif" IsOwner="false" />
        </Members>
        <Channels>
          <Channel Name="Corporate Communication" ID="corporatecommunication" Description="" Creator="Admin" />
          <Channel Name="Lean Process Improvement" ID="corporatecommunication" Description="" Creator="Admin" />
          <Channel Name="Training and Certification" ID="trainingandcertification" Description="" Creator="Admin" />
          <Channel Name="Production" ID="production" Description="" Creator="Admin" />
          <Channel Name="Research and Development" ID="researchanddevelopment" Description="" Creator="Admin" />
          <Channel Name="Supplier Collaboration" ID="suppliercollaboration" Description="" Creator="Admin" />
        </Channels>
      </Team>
    </Teams>
    ```

2. <span data-ttu-id="08de3-121">Сохраните следующий фрагмент в качестве сценария PowerShell (.ps1) и обратите внимание, где он сохранен.</span><span class="sxs-lookup"><span data-stu-id="08de3-121">Save the following snippet as a PowerShell script (.ps1) and note where you have saved it.</span></span> <span data-ttu-id="08de3-122">В этом скрипте выполняются действия по созданию команды и канала, а также добавлены члены к ним:</span><span class="sxs-lookup"><span data-stu-id="08de3-122">This script executes the steps to create the team and channel, and add members to them:</span></span>

    ```powershell
    Param(
        [Parameter(Mandatory = $true)]

        # This specifies the location of your configuration XML.

        [string] $teamsFilePath 
    )

    [xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

    if ($XmlDocument.Teams.Team.Count -gt 0) {

        try {

            # 1. Login with the global administrator account for your O365 Developer Program tenant. This script uses these credentials to connect to the powershell modules for Azure Active Directory and Microsoft Teams

            $creds = Get-Credential

            # Connecting to AAD PowerShell
            Connect-AzureAD -Credential $creds | Out-Null

            # Connect to Microsoft Teams PowerShell
            Connect-MicrosoftTeams -Credential $creds | Out-Null

            Write-Host "Connected to Microsoft 365 and configuring your organization with test teams and channels"

            # 2. Create the teams as specified in the XML.

            foreach ($team in $XmlDocument.Teams.Team ) {
                try {
                    $group = New-Team -DisplayName $team.Name -Description $teams.description -visibility public 
                    Write-Host "Successfully created team: " $group.DisplayName
                }
                catch {
                    Write-Host "Unable to create team: $_"
                }

                # 3. Add users to the newly created teams.
                foreach ($user in $team.Members.Member) {
                    try {
                        $newUserPrincipalName = (Get-AzureADUser -SearchString $user.UserName).UserPrincipalName

                        if($user.IsOwner -eq $true){
                            Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName -Role Owner | Out-Null
                        }else{
                            Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName | Out-Null
                        }

                        Write-Host "Successfully added user : " $user.UserName
                    }
                    catch {
                        Write-Host "Unable to add team user: $_"
                    }

                }

                # 4. Add a set of channels to each newly created team
                foreach ($channel in $team.Channels.Channel) {
                    try {
                        # Adding each team channel
                        New-TeamChannel -GroupId $group.GroupId -DisplayName $channel.Name -Description $channel.Description | Out-Null
                        Write-Host "Successfully created channel: " $channel.Name
                    }
                    catch {
                        Write-Host "Unable to add new Team Channel: $_"
                    }   
                }

                Clear-Variable -Name group
            }

            Clear-Variable -Name creds

            # 5. Disconnect from all PowerShell sessions

            Write-Host "Completed execution and disconnecting from Microsoft 365 PowerShell sessions."
            Disconnect-MicrosoftTeams
            Disconnect-AzureAD
        }
        catch {
            Write-Host "Unable to complete the operation: $_"
        }
    }
    else {
        Write-Host "Content file has invalid data."
    }
    ```

3. <span data-ttu-id="08de3-123">Откройте сеанс Windows PowerShell в режиме Администратор и запустите только что сохраненный сценарий.</span><span class="sxs-lookup"><span data-stu-id="08de3-123">Open a Windows PowerShell session in Administrator mode, and run the script that you just saved.</span></span>
4. <span data-ttu-id="08de3-124">Если вам будет предложено предоставить учетные данные, введите учетные данные глобального администратора, полученные при первой подписке на разработчика.</span><span class="sxs-lookup"><span data-stu-id="08de3-124">When you are prompted to provide the credentials, enter the Global Administrator credentials you received when you first signed up for your developer subscription.</span></span>

    > [!Note]
    > <span data-ttu-id="08de3-125">Не закрывайте сеанс PowerShell, так как для выполнения сценария требуется несколько минут.</span><span class="sxs-lookup"><span data-stu-id="08de3-125">Do not close your PowerShell session as the script takes several minutes to execute.</span></span> <span data-ttu-id="08de3-126">Если вы изменили пользователей подписки на то, что создано в пакете контента по умолчанию, некоторые пользователи могут не быть добавлены в Teams.</span><span class="sxs-lookup"><span data-stu-id="08de3-126">If you have modified the users in your subscription from what is created in the default content pack, some users may not be added to Teams.</span></span> <span data-ttu-id="08de3-127">При выполнении скрипта отображаются успешные или неудачные действия.</span><span class="sxs-lookup"><span data-stu-id="08de3-127">As the script executes it displays successful or failed actions.</span></span>

5. <span data-ttu-id="08de3-128">После завершения выполнения сценария можно войти в клиент Teams с одной из учетных записей пользователей и просмотреть вновь созданные команды.</span><span class="sxs-lookup"><span data-stu-id="08de3-128">After the script has finished execution, you can sign in to the Teams client with one of the user accounts and view the newly created teams.</span></span>

## <a name="see-also"></a><span data-ttu-id="08de3-129">См. также</span><span class="sxs-lookup"><span data-stu-id="08de3-129">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="08de3-130">Отламывка вкладки</span><span class="sxs-lookup"><span data-stu-id="08de3-130">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="08de3-131">Отламывка ботов</span><span class="sxs-lookup"><span data-stu-id="08de3-131">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="08de3-132">Тестирование разрешений RSC</span><span class="sxs-lookup"><span data-stu-id="08de3-132">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

