---
title: Добавление тестовых данных в тестовый клиент Microsoft 365
description: Узнайте, как настроить подписку Office 365 разработчика для успешного тестирования приложений Microsoft Teams с помощью фрагментов кода
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 11/01/2019
ms.openlocfilehash: 6d3524ffc5e2ec5bb8f43fefcc100050060e154e
ms.sourcegitcommit: 22e0803bb1d17ccb5222b7a1aa0f1ccebd785bdc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/20/2022
ms.locfileid: "67835549"
---
# <a name="add-test-data-to-your-environment"></a>Добавление тестовых данные в среду

Вы можете протестировать Microsoft Teams с примерами данных с помощью подписки на Microsoft 365 для разработчиков.

## <a name="prerequisites"></a>Предварительные условия

1. [Присоединитесь к программе для разработчиков Microsoft 365](/office/developer-program/office-365-developer-program), если у вас нет тестового клиента.
2. [Настройка подписки для разработчиков Microsoft 365](/office/developer-program/office-365-developer-program-get-started)
3. [Используйте примеры пакетов данных с подпиской на Microsoft 365 для разработчиков, чтобы установить пакет содержимого "Пользователи"](/office/developer-program/install-sample-packs).
4. [Установите модуль Teams PowerShell](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2).
5. [Установите модуль Azure AD PowerShell](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true).

> [!NOTE]
> Для запуска сценариев необходимо иметь разрешения глобального администратора в клиенте.

## <a name="allow-users-to-upload-apps"></a>Разрешить пользователям загружать приложения

По умолчанию только глобальные администраторы или администраторы службы Teams могут отправлять (загружать неопубликованные надстройки) приложения в клиенте. Вы также можете разрешить пользователям отправлять пользовательские приложения для собственного использования или в Teams для тестирования. Дополнительные сведения см. в разделе [Управление политиками и параметрами пользовательских приложений в Teams](/microsoftteams/teams-custom-app-policies-and-settings).

## <a name="create-teams-and-channels-for-testing"></a>Создание команд и каналов для тестирования

1. Сохраните следующий фрагмент в виде файла **.xml** и запишите путь к файлу. Этот XML-код определяет структуру команды и канала, которые создаются вместе с ее участниками:

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

2. Сохраните следующий фрагмент кода в виде скрипта PowerShell (.ps1) и запишите, где он был сохранен. Этот сценарий выполняет действия по созданию команды и канала и добавлению в них участников:

    ```powershell
    Param(
        [Parameter(Mandatory = $true)]

        # This specifies the location of your configuration XML.

        [string] $teamsFilePath 
    )

    [xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

    if ($XmlDocument.Teams.Team.Count -gt 0) {

        try {

            # 1. Login with the global administrator account for your Office 365 Developer Program tenant. This script uses these credentials to connect to the PowerShell modules for Azure Active Directory and Microsoft Teams

            $creds = Get-Credential

            # Connecting to Azure AD PowerShell
            Connect-AzureAD -Credential $creds | Out-Null

            # Connect to Microsoft Teams PowerShell
            Connect-MicrosoftTeams -Credential $creds | Out-Null

            Write-Host "Connected to Microsoft 365 and configuring your organization with test teams and channels"

            # 2. Create the teams as specified in the XML.

            foreach ($team in $XmlDocument.Teams.Team ) {
                try {
                    $group = New-Team -DisplayName $team.Name -Description $team.description -visibility public 
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

3. Откройте сеанс Windows PowerShell в режиме администратора и запустите сохраненный скрипт.
4. При появлении запроса на ввод учетных данных введите учетные данные глобального администратора, полученные при первой регистрации в подписке разработчика.

    > [!Note]
    > Не закрывайте сеанс PowerShell, так как выполнение сценария занимает несколько минут. Если вы изменили пользователей в вашей подписке, созданных в пакете содержимого по умолчанию, некоторые пользователи могут не быть добавлены в Teams. По мере выполнения сценария отображаются успешные или неудачные действия.

5. После завершения выполнения сценария можно войти в клиент Teams с помощью одной из учетных записей пользователей и просмотреть только что созданные команды.

## <a name="see-also"></a>Дополнительные ресурсы

* [Отладка вкладки](~/tabs/how-to/developer-tools.md)
* [Отладка ботов](~/bots/how-to/debug/locally-with-an-ide.md)
* [Тестирование разрешений RSC](~/graph-api/rsc/test-resource-specific-consent.md)
