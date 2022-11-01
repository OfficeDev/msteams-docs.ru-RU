## <a name="deploy-your-app-to-azure"></a>Развертывание приложения в Azure

Развертывание состоит из двух этапов. Во-первых, создаются необходимые облачные ресурсы (также известные как подготовка). Затем код приложения копируется в созданные облачные ресурсы. В этом руководстве вы развернете приложение вкладки.
<br>
<br>
<details>
<summary>В чем разница между подготовкой и развертыванием?</summary>
<br>
Шаг <b>подготовки</b> создает ресурсы в Azure и Microsoft 365 для приложения, но код (HTML, CSS, JavaScript и т. д.) не копируется в ресурсы. Шаг <b>Развертывание</b> копирует код приложения в ресурсы, созданные на этапе подготовки. Обычно развертывание выполняется несколько раз без подготовки новых ресурсов. Так как процесс подготовки может занять некоторое время, он отделен от шага развертывания.
</details>
<br>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

Выберите значок Набор инструментов Teams:::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: на боковой панели Visual Studio Code.

1. Выберите **Подготовить в облаке**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Снимок экрана: команды подготовки":::

1. Выберите любого пользователя из существующей подписки.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/select-subscription.png" alt-text="Снимок экрана: выбор существующей подписки":::

1. Выберите группу ресурсов, используемую для ресурсов Azure.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="Снимок экрана: ресурсы для подготовки":::

   > [!NOTE]
   > Приложение размещается с помощью ресурсов Azure.
   >
   >Дополнительные сведения см. в разделе [Создание группы ресурсов.](/azure/azure-resource-manager/management/manage-resource-groups-portal)

    В диалоговом окне появится предупреждение о том, что при выполнении ресурсов в Azure могут возникнуть затраты.

1. Выберите **Подготовка**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="Снимок экрана: подготовка диалогового окна.":::

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-confirm1.png" alt-text="Снимок экрана: выбор подписки.":::

   Процесс подготовки создает ресурсы в облаке Azure. Это может занять некоторое время. Ход выполнения можно отслеживать, наблюдая за диалогами в правом нижнем углу. Через несколько минут вы увидите следующее уведомление:

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-successmsgext.png" alt-text="Снимок экрана: ресурс, успешно подготовленный в облаке.":::

    При необходимости можно просмотреть подготовленные ресурсы. В этом руководстве вам не нужно просматривать ресурсы.

    Подготовленный ресурс отображается в разделе **Среда** .

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="Снимок экрана: подготовленный ресурс.":::

1. После завершения **подготовки выберите Развернуть в облаке** на панели **Развертывание** .

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="Снимок экрана: развертывание в облаке.":::

   Как и при подготовке, развертывание занимает некоторое время. Вы можете отслеживать процесс, наблюдая за диалогами в правом нижнем углу. Через несколько минут вы увидите уведомление о завершении.

Теперь вы можете использовать тот же процесс для развертывания приложений Bot и расширения сообщений в Azure.

# <a name="command-line"></a>[Командная строка](#tab/cli)

В окне терминала:

1. Запустите `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   При появлении запроса выберите подписку Azure для использования ресурсов Azure.

1. Запустите `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> Приложение размещается с помощью ресурсов Azure.

## <a name="run-the-deployed-app"></a>Запуск развернутого приложения

После завершения действий по подготовке и развертыванию:

1. Откройте панель отладки (**CTRL+SHIFT+D️** / **⇧-D** или **Просмотр > запуска**) из Visual Studio Code.
1. В раскрывающемся списке конфигурации запуска выберите **Запустить удаленное управление (edge).**
1. Нажмите кнопку **Начать отладку (F5),** чтобы запустить приложение из Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="Снимок экрана: удаленный запуск приложения.":::

1. Выберите **Добавить** при появлении запроса на загрузку неопубликованного приложения в Teams.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="Снимок экрана: устанавливаемое приложение.":::

    Поздравляем, ваше первое приложение вкладки работает в вашей среде Azure!

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-apptab.png" alt-text="Снимок экрана: сообщение о том, как попробовать приложение сейчас или позже.":::
