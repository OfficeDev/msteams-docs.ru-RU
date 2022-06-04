## <a name="deploy-your-app-to-azure"></a>Развертывание приложения в Azure

Развертывание состоит из двух этапов.  Во-первых, создаются необходимые облачные ресурсы (также называемые подготовкой). Затем код приложения копируется в созданные облачные ресурсы. В этом руководстве вы развернете приложение табуляции.
<br> 
<br>
<details>
<summary>В чем разница между подготовкой и развертыванием?</summary>
<br>
На <b>этапе</b> подготовки создаются ресурсы в Azure и Microsoft 365 для вашего приложения, но код (HTML, CSS, JavaScript и т. д.) не копируется в ресурсы. На <b>шаге</b> "Развертывание" код приложения копируется в ресурсы, созданные на этапе подготовки. Обычно развертывание выполняется несколько раз без подготовки новых ресурсов. Так как этап подготовки может занять некоторое время, он отделен от шага развертывания.
</details>
<br>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode);

Выберите значок Набор инструментов Teams:::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: на боковой панели Visual Studio Code.

1. Выберите **"Подготовка в облаке"**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Снимок экрана: команды подготовки" border="false":::

1. Выберите подписку, используемую для ресурсов Azure.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="Снимок экрана: ресурсы для подготовки" border="false":::

   > [!NOTE]
   > Для размещения приложения всегда используются некоторые ресурсы Azure.

    В диалоговом окне выводится предупреждение о том, что при запуске ресурсов в Azure могут возникнуть затраты.

1. Выберите **"Подготовка"**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="Снимок экрана: диалоговое окно подготовки." border="true":::

   Процесс подготовки создает ресурсы в облаке Azure. Это может занять некоторое время. Ход выполнения можно отслеживать, просмотрев диалоги в правом нижнем углу. Через несколько минут вы увидите следующее уведомление:

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-successmsg.png" alt-text="Снимок экрана: диалоговое окно завершения подготовки." border="false":::

    При необходимости можно просмотреть подготовленные ресурсы. В этом руководстве вам не нужно просматривать ресурсы.

    Подготовленный ресурс отображается в разделе **"Среда** ".

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="Снимок экрана: диалоговое окно завершения подготовки." border="false":::

1. Выберите **"Развернуть в облаке** " на панели **развертывания** после завершения подготовки.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="Снимок экрана, показывающий, где можно выполнить развертывание в облаке." border="false":::

   Как и в случае с подготовкой, развертывание занимает некоторое время. Вы можете отслеживать процесс, просмотрев диалоги в правом нижнем углу. Через несколько минут вы увидите уведомление о завершении.

Теперь вы можете использовать тот же процесс для развертывания приложений Бота и расширения сообщений в Azure.

# <a name="command-line"></a>[Командная строка](#tab/cli)

В окне терминала:

1. Запустите `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   При появлении запроса выберите подписку Azure для использования ресурсов Azure.

   > [!NOTE]
   > Для размещения приложения всегда используются некоторые ресурсы Azure.

1. Запустите `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

---

## <a name="run-the-deployed-app"></a>Запуск развернутых приложений

После завершения подготовки и развертывания сделайте следующее:

1. Откройте панель отладки (**CTRL+SHIFT+D** / **⌘⇧-D** или view **> Run**) в Visual Studio Code.
1. В **раскрывающемся списке конфигурации запуска выберите launch Remote (Edge** ).
1. Выберите команду **"Начать отладку" (F5),** чтобы запустить приложение из Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="Снимок экрана: удаленное приложение запуска." border="false":::

1. Выберите **"Добавить** " при появлении запроса на загрузку неопубликованного приложения в Teams.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="Снимок экрана: устанавливаемого приложения." border="false":::

    Поздравляем! Первое приложение табуляции запущено в вашей среде Azure!

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-apptab.png" alt-text="Снимок экрана: сообщение о попытке использовать приложение сейчас или позже" border="true":::
 