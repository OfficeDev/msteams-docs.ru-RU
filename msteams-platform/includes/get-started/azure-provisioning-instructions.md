## <a name="deploy-your-app-to-azure"></a>Развертывание приложения в Azure

Развертывание состоит из двух этапов.  Сначала создаются необходимые облачные ресурсы (также известные как подготовка). Затем код приложения копируется в созданные облачные ресурсы. В этом руководстве будет развернуто приложение вкладки.

> <details>
> <summary>В чем разница между Provision и Deploy?</summary>
>
> Шаг **Provision** создает ресурсы в Azure и Microsoft 365 для приложения, но код (HTML, CSS, JavaScript и т.д.) не копируется в ресурсы. Шаг **Развертывание** копирует код приложения на ресурсы, созданные во время шага по предоставлению. Часто развертывается несколько раз без предоставления новых ресурсов. Так как этап предоставления может занять некоторое время, он отделен от шага развертывания.
</details>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

Выберите значок Набор инструментов Teams:::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: на боковой панели Visual Studio Code.

1. Выберите **Положение в облаке**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Снимок экрана, показывающий команды по подготовкам" border="false":::

1. Выберите подписку для использования для ресурсов Azure.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="Снимок экрана, показывающий ресурсы для подготовка" border="false":::

   > [!NOTE]
   > Для размещения приложения всегда используются некоторые ресурсы Azure.

    Диалоговое окно предупреждает, что при запуске ресурсов в Azure могут возникнуть затраты.

1. Выберите **Положение**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="Снимок экрана диалогового временного набора." border="false":::

   Процесс подготовка создает ресурсы в облаке Azure. Это может занять некоторое время. Вы можете отслеживать ход, наблюдая диалоги в правом нижнем углу. Через несколько минут вы увидите следующее уведомление:

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-success.png" alt-text="Снимок экрана, показывающий полный диалоговое окно подготовка." border="false":::

    Если вы хотите, вы можете просмотреть предварительные ресурсы. В этом руководстве нет необходимости просматривать ресурсы.

    Предварительный ресурс отображается в разделе **Окружающая** среда.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="Снимок экрана, показывающий полный диалоговое окно подготовка." border="false":::

1. Выберите **Развертывание в облаке** из панели **развертывания** после завершения подготовка.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="Снимок экрана, показывающий, где щелкнуть, чтобы развернуть в облако." border="false":::

   Как и в области подготовка, развертывание занимает некоторое время. Вы можете отслеживать процесс, наблюдая диалоги в правом нижнем углу. Через несколько минут вы увидите уведомление о завершении.

Теперь вы можете использовать тот же процесс для развертывания приложений для расширения ботов и сообщений в Azure.

# <a name="command-line"></a>[Командная строка](#tab/cli)

В окне терминала:

1. Запустите `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   При запросе выберите подписку Azure для использования ресурсов Azure.

   > [!NOTE]
   > Для размещения приложения всегда используются некоторые ресурсы Azure.

1. Запустите `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

---

## <a name="run-the-deployed-app"></a>Запуск развернутых приложений

После завершения этапов подготовка и развертывание:

1. Откройте панель отключки (**Ctrl+Shift+D** / **⌘⇧-D** или **Просмотр > Run**) из Visual Studio Code.
1. Выберите **Пульт запуска (Edge)** из выпадаемой конфигурации запуска.
1. Выберите кнопку Play, чтобы запустить приложение из Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="Снимок экрана с удаленным отображением запуска приложения." border="false":::

1. Нажмите **Добавить**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="Снимок экрана, показывающий установку приложения." border="false":::

   Ваше приложение загружается на сайт Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-app.png" alt-text="Снимок экрана, показывающий установку приложения." border="false":::

    Поздравляем! Приложение вкладки теперь работает удаленно из Azure!
