---
title: Добавление тестовых данных в тестовый клиент Office 365
description: Настройка подписки на программу для разработчиков Office 365 для успешного тестирования приложений Microsoft Teams
keywords: Тестирование Teams в программе для разработчиков приложений
ms.date: 11/01/2019
ms.openlocfilehash: 87e9dc280c192f013098c3e9f604f72238bfafdf
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867097"
---
# <a name="add-test-data-to-your-office-365-test-tenant"></a><span data-ttu-id="5265b-104">Добавление тестовых данных в тестовый клиент Office 365</span><span class="sxs-lookup"><span data-stu-id="5265b-104">Add test data to your Office 365 test tenant</span></span>

<span data-ttu-id="5265b-105">Настройка подписки на программу разработчика O365 (или другого тестового клиента) для упрощения тестирования созданных приложений.</span><span class="sxs-lookup"><span data-stu-id="5265b-105">Set up your O365 developer program subscription (or other test tenant) to make it easy for you to test the apps that you've built.</span></span>  <span data-ttu-id="5265b-106">Это позволит:</span><span class="sxs-lookup"><span data-stu-id="5265b-106">It will help you:</span></span>

- <span data-ttu-id="5265b-107">Создание новых команд и каналов в Организации</span><span class="sxs-lookup"><span data-stu-id="5265b-107">Create new teams and channels in your organization</span></span>

- <span data-ttu-id="5265b-108">Добавьте пользователей, которые созданы с помощью пакета содержимого пользователя, в эти команды.</span><span class="sxs-lookup"><span data-stu-id="5265b-108">Add the users that are created via the User content pack to those teams.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5265b-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="5265b-109">Before you start</span></span>

<span data-ttu-id="5265b-110">Если у вас еще нет тестового клиента, вам потребуется присоединиться к программе для разработчиков Office 365 и зарегистрировать подписку разработчика.</span><span class="sxs-lookup"><span data-stu-id="5265b-110">If you don't already have a test tenant, you will need to join the Office 365 developer program and sign up for a developer subscription.</span></span> <span data-ttu-id="5265b-111">Кроме того, вам потребуется установить необходимые модули PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5265b-111">You'll also need to install the necessary PowerShell modules.</span></span> <span data-ttu-id="5265b-112">Для запуска скриптов необходимо иметь разрешения глобального администратора для любого клиента, который вы используете.</span><span class="sxs-lookup"><span data-stu-id="5265b-112">For whatever tenant you use you'll need to have global administrator permissions to run the scripts.</span></span>

1. [<span data-ttu-id="5265b-113">Присоединяйтесь к программе для разработчиков Office 365</span><span class="sxs-lookup"><span data-stu-id="5265b-113">Join the Office 365 Developer Program</span></span>](/office/developer-program/office-365-developer-program)
2. [<span data-ttu-id="5265b-114">Настройка подписки на Microsoft 365 для разработчиков</span><span class="sxs-lookup"><span data-stu-id="5265b-114">Set up a Microsoft 365 Developer Subscription</span></span>](/office/developer-program/office-365-developer-program-get-started)
3. [<span data-ttu-id="5265b-115">Использование образцов пакетов данных с подпиской на Office 365 для разработчиков для установки пакета содержимого для пользователей</span><span class="sxs-lookup"><span data-stu-id="5265b-115">Use sample data packs with your Office 365 developer subscription to install the Users content pack</span></span>](/office/developer-program/install-sample-packs)
4. [<span data-ttu-id="5265b-116">Установка модуля PowerShell Teams</span><span class="sxs-lookup"><span data-stu-id="5265b-116">Install the Teams PowerShell module</span></span>](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)
5. [<span data-ttu-id="5265b-117">Установка модуля Azure AD PowerShell</span><span class="sxs-lookup"><span data-stu-id="5265b-117">Install the Azure AD PowerShell module</span></span>](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module)

### <a name="optional-step-allow-upload-of-custom-apps"></a><span data-ttu-id="5265b-118">Необязательный шаг: разрешить отправку пользовательских приложений</span><span class="sxs-lookup"><span data-stu-id="5265b-118">Optional step: allow upload of custom apps</span></span>

<span data-ttu-id="5265b-119">По умолчанию только глобальные администраторы или Администраторы службы Teams могут отправлять пользовательские приложения в каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="5265b-119">By default, only global admins or teams service admins can upload custom apps into the tenant app catalog.</span></span>  <span data-ttu-id="5265b-120">Вы также можете разрешить всем пользователям отправлять пользовательские приложения для их использования или для тестирования в Teams.</span><span class="sxs-lookup"><span data-stu-id="5265b-120">You can also enable all users to upload custom apps for their own use or to teams for testing.</span></span>

<span data-ttu-id="5265b-121">Чтобы включить этот параметр, необходимо обновить политику установки глобального приложения в портале администрирования Teams.</span><span class="sxs-lookup"><span data-stu-id="5265b-121">To enable this setting, you'll need to update the global App Setup Policy in your Teams Admin Portal.</span></span>

<img width="430px" src="~/assets/images/microsoft-teams-admin-center-screenshot.png" title="Снимок экрана: политика установки приложений" />

<span data-ttu-id="5265b-123">Дополнительные сведения см. в указанных ниже статьях.    </span><span class="sxs-lookup"><span data-stu-id="5265b-123">For more information see:</span></span>

 - [<span data-ttu-id="5265b-124">Управление политиками установки приложений в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5265b-124">Manage app setup policies in Microsoft Teams</span></span>](/microsoftteams/teams-app-setup-policies)

## <a name="create-teams-and-channels"></a><span data-ttu-id="5265b-125">Создание команд и каналов</span><span class="sxs-lookup"><span data-stu-id="5265b-125">Create teams and channels</span></span>

<span data-ttu-id="5265b-126">Сохраните следующий фрагмент кода в виде XML-файла (XML) и запомните, где вы его сохранили.</span><span class="sxs-lookup"><span data-stu-id="5265b-126">Save the following snippet as an XML (.xml) and note where you've saved it.</span></span>  <span data-ttu-id="5265b-127">В этом XML-коде определяется структура команд и каналов, которые будут созданы, вместе с их участниками.</span><span class="sxs-lookup"><span data-stu-id="5265b-127">This XML defines the structure of the teams and channels that will be created - along with its members.</span></span>

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

<span data-ttu-id="5265b-128">Сохраните следующий фрагмент кода в виде скрипта PowerShell (PS1) и запомните, где вы его сохранили.</span><span class="sxs-lookup"><span data-stu-id="5265b-128">Save the following snippet as a PowerShell script (.ps1) and note where you've saved it.</span></span>  <span data-ttu-id="5265b-129">Этот сценарий выполняет действия по созданию команд и каналов и добавлению участников в них.</span><span class="sxs-lookup"><span data-stu-id="5265b-129">This script executes the steps to create the teams and channels and add members to them.</span></span>

```powershell
Param(
    [Parameter(Mandatory = $true)]
    
    # This specifies the location of your configuration XML.
    
    [string] $teamsFilePath 
)
    
[xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

if ($XmlDocument.Teams.Team.Count -gt 0) {

    try {
        
        # 1. Login with the global administrator account for your O365 Developer Program tenant.  This script will then use these credentials to connect to the powershell modules for Azure Active Directory and Microsoft Teams
        
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

<span data-ttu-id="5265b-130">Откройте сеанс Windows PowerShell в режиме администратора.</span><span class="sxs-lookup"><span data-stu-id="5265b-130">Open a Windows PowerShell session in Administrator mode.</span></span>  <span data-ttu-id="5265b-131">Запустите скрипт, который вы только что сохранили.</span><span class="sxs-lookup"><span data-stu-id="5265b-131">Run the script that you just saved.</span></span>  <span data-ttu-id="5265b-132">Вам будет предложено ввести учетные данные, используя учетные данные глобального администратора, которые вы получили при первой регистрации в вашей подписке разработчика.</span><span class="sxs-lookup"><span data-stu-id="5265b-132">You'll be prompted to provide the credentials - use the Global Administrator credentials you received when you first signed up for your developer subscription.</span></span>

> [!Note]
> <span data-ttu-id="5265b-133">Выполнение сценария займет несколько минут, не закрывайте сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5265b-133">The script will take several minutes to execute - do not close your PowerShell session.</span></span>  <span data-ttu-id="5265b-134">Если вы изменяли пользователей в подписке из того, что создается в пакете содержимого по умолчанию, некоторые пользователи не могут быть добавлены в Teams.</span><span class="sxs-lookup"><span data-stu-id="5265b-134">If you've modified the users in your subscription from what is created in the default content pack, some users may not be added to teams.</span></span>  <span data-ttu-id="5265b-135">При выполнении скрипта будут выводиться действия, которые были успешными или неудачными.</span><span class="sxs-lookup"><span data-stu-id="5265b-135">As the script executes it will output successful or failed actions.</span></span>

<span data-ttu-id="5265b-136">После завершения выполнения скрипта можно выполнить вход в клиент Teams с одной из учетных записей пользователей и просмотреть только что созданные команды.</span><span class="sxs-lookup"><span data-stu-id="5265b-136">Once the script has finished execution, you can login to the Teams client with one of the user accounts and view the newly created teams.</span></span>
