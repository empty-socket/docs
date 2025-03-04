# Добавить пользователя

## Добавить пользователя Яндекса{#add-user-account}

Если у сотрудников компании есть аккаунты на Яндексе (например, `{{login-example}}`), они могут использовать эти аккаунты для доступа к сервисам {{yandex-cloud}}, подключенным к вашей организации.

Чтобы добавить аккаунты сотрудников в организацию:

1. [Войдите в аккаунт]({{link-passport}}) администратора организации.

1. Перейдите в сервис [{{org-full-name}}]({{link-org-main}}).

1. На левой панели выберите раздел [Пользователи]({{link-org-users}}) ![icon-users](../_assets/organization/icon-users.png).

1. В правом верхнем углу нажмите кнопку **Добавить пользователя**.

1. Введите почтовые адреса пользователей Яндекса, которых вы хотите пригласить в организацию (например, `{{login-example}}`).

1. Нажмите кнопку **Добавить**. Пользователи будут подключены к организации.

Чтобы получить доступ к сервисам, которые подключены к организации, приглашенным пользователям будет достаточно войти в свой аккаунт на Яндексе.

## Добавить федеративных пользователей {#add-user-sso}

Если при [настройке федерации](add-federation.md#federation-usage) вы не включили опцию **Автоматически создавать пользователей**, федеративных пользователей нужно добавить в организацию вручную.

Для этого вам необходимо знать Name ID пользователей, которые возвращает сервер поставщика удостоверений (IdP) вместе с ответом об успешной аутентификации. Обычно это основной email пользователя. Если вы не знаете, что возвращает сервер в качестве Name ID, обратитесь к администратору, который настраивал аутентификацию в вашей федерации.

Чтобы добавить пользователей федерации в организацию:

{% list tabs %}

- Интерфейс {{ org-name }}

  1. [Войдите в аккаунт]({{link-passport}}) администратора организации.

  1. Перейдите в сервис [{{org-full-name}}]({{link-org-main}}).

  1. На левой панели выберите раздел [Пользователи]({{link-org-users}}) ![icon-users](../_assets/organization/icon-users.png).

  1. В правом верхнем углу нажмите на стрелку возле кнопки **Добавить пользователя**. Выберите **Добавить федеративных пользователей**.

  1. Выберите федерацию, из которой необходимо добавить пользователей.

  1. Перечислите Name ID пользователей, разделяя их переносами строк.

  1. Нажмите кнопку **Добавить**. Пользователи будут подключены к организации.

- CLI

  {% include [cli-install](../_includes/cli-install.md) %}

  {% include [default-catalogue](../_includes/default-catalogue.md) %}

  1. Посмотрите описание команды добавления пользователей:

      ```
      yc organization-manager federation saml add-user-accounts --help
      ```

  1. Добавьте пользователей, перечислив их Name ID через запятую:

      ```
      yc organization-manager federation saml add-user-accounts --name my-federation \
        --name-ids=alice@example.com,bob@example.com,charlie@example.com
      ```

- API

  Чтобы добавить пользователей федерации в облако:

  1.  Сформируйте файл с телом запроса, например `body.json`. В теле запроса укажите массив Name ID пользователей, которых необходимо добавить:

      ```json
      {
        "nameIds": [
          "alice@example.com",
          "bob@example.com",
          "charlie@example.com"
        ]
      }
      ```
  1.  Отправьте запрос, указав в параметрах идентификатор федерации:

      ```bash
      $ curl -X POST \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer <IAM-токен>" \
        -d '@body.json' \
        https://organization-manager.{{ api-host }}/organization-manager/v1/saml/federations/<ID федерации>:addUserAccounts
      ```

{% endlist %}