---
title: Добавление тестовых данных в тестовый клиент Microsoft 365
description: Настройка подписки на программу разработчика Office 365 для успешного тестирования приложений Microsoft Teams
ms.topic: how-to
localization_priority: Normal
keywords: тестирование групп программ разработчика приложений
ms.date: 11/01/2019
ms.openlocfilehash: f224ad8b97cd5dd1a4349039824abaf551ef362e
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058469"
---
# <a name="add-test-data-to-your-microsoft-365-test-tenant"></a>Добавление тестовых данных в тестовый клиент Microsoft 365

С подпиской на разработчика Microsoft 365 вы можете использовать приложение Microsoft Teams с группами тестирования, каналами и пользователями.

## <a name="prerequisites"></a>Необходимые условия

1. [Присоединяйтесь к программе разработчиков Microsoft 365,](/office/developer-program/office-365-developer-program)если у вас нет тестового клиента.
2. [Настройка подписки на разработчика Microsoft 365.](/office/developer-program/office-365-developer-program-get-started)
3. [Используйте примеры пакетов данных с подпиской на разработчика Microsoft 365 для установки пакета контента Пользователей.](/office/developer-program/install-sample-packs)
4. [Установите модуль Teams PowerShell.](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)
5. [Установите модуль Azure AD PowerShell.](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true)

> [!NOTE]
> Для любого клиента, который вы используете, необходимо получить разрешения глобального администратора для запуска сценариев.

### <a name="optional-step-to-allow-upload-of-custom-apps"></a>Необязательный шаг, позволяющий загружать настраиваемые приложения

По умолчанию только глобальные администраторы или администраторы служб групп могут загружать настраиваемые приложения в каталог приложений клиента. Вы также можете позволить всем пользователям загружать настраиваемые приложения для собственного использования или в группы для тестирования.

Чтобы включить этот параметр, необходимо обновить глобальную политику установки приложений на портале администрирования Teams.

<img width="430px" src="~/assets/images/microsoft-teams-admin-center-screenshot.png" alt="Screenshot of App Setup Policy"/>

## <a name="optional-step-to-enable-custom-app-sideloading"></a>Необязательный шаг, чтобы включить настраиваемую загрузку приложений

Включение настраиваемой загрузки приложений необязательно. По умолчанию только глобальные администраторы или администраторы служб Teams могут загружать настраиваемые приложения в каталог приложений клиента. Вы также можете разрешить пользователям загружать настраиваемые приложения в Teams. Дополнительные сведения см. в [сведениях об управлении политиками установки приложений в Teams.](/microsoftteams/teams-app-setup-policies)

## <a name="create-teams-and-channels"></a>Создание команд и каналов

1. Сохраните следующий фрагмент в качестве **файла .xml** и обратите внимание на путь файла. Этот XML определяет структуру команды и канала, созданного вместе с ее участниками:

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

2. Сохраните следующий фрагмент в качестве сценария PowerShell (.ps1) и обратите внимание, где он сохранен. В этом скрипте выполняются действия по созданию команды и канала, а также добавлены члены к ним:

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

3. Откройте сеанс Windows PowerShell в режиме Администратор и запустите только что сохраненный сценарий.
4. Если вам будет предложено предоставить учетные данные, введите учетные данные глобального администратора, полученные при первой подписке на разработчика.

    > [!Note]
    > Не закрывайте сеанс PowerShell, так как для выполнения сценария требуется несколько минут. Если вы изменили пользователей подписки на то, что создано в пакете контента по умолчанию, некоторые пользователи могут не быть добавлены в Teams. При выполнении скрипта отображаются успешные или неудачные действия.

5. После завершения выполнения сценария можно войти в клиент Teams с одной из учетных записей пользователей и просмотреть вновь созданные команды.

## <a name="see-also"></a>См. также

- [Отламывка вкладки](~/tabs/how-to/developer-tools.md)
 
- [Отламывка ботов](~/bots/how-to/debug/locally-with-an-ide.md)

- [Тестирование разрешений RSC](~/graph-api/rsc/test-resource-specific-consent.md)

