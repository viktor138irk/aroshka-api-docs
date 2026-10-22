# Справочник методов API Aroshka Cloud

Собрано из `openapi.json` (OpenAPI 3.1.0, версия API 1.0.0).

База: `https://aroshka.cloud/api/v1`. Авторизация: заголовок `Authorization: Bearer <ключ>`.

## Files

### GET `/drive/file-entries/{id}/model`

Retrieve file metadata

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403, 404

### GET `/drive/file-entries`

List all files

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `section` | query | string | да |
| `folder_id` | query | string/null | нет |
| `type` | query | string/null | нет |
| `owner` | query | string/null | нет |
| `created_at` | query | string/null | нет |
| `updated_at` | query | string/null | нет |
| `location` | query | string/null | нет |
| `sharing` | query | string/null | нет |
| `query` | query | string/null | нет |
| `per_page` | query | integer/null | нет |
| `page` | query | integer/null | нет |
| `sort` | query | string/null | нет |

Ответы: 200, 403, 422

### PUT `/drive/file-entries/{id}`

Update file metadata

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `name` | string | нет |
| `description` | string/null | нет |
| `tags` | array/null | нет |

Ответы: 200, 403, 422, 404

### POST `/file-entries/move`

Move files

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `destinationId` | integer/null | нет |
| `entryIds` | массив integer | да |

Ответы: 200, 422, 403

### POST `/file-entries/duplicate`

Duplicate files

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `destinationId` | integer/null | нет |
| `entryIds` | массив integer | да |

Ответы: 200, 422, 403

### POST `/folders`

Create a new folder

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `name` | string | да |
| `parent_id` | integer/null | нет |

Ответы: 200, 422, 403

### GET `/folders/{hash}/path`

Get full path for a folder

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `hash` | path | string | да |
| `shareable_link` | query | string/null | нет |
| `password` | query | string/null | нет |

Ответы: 200, 422, 403

### POST `/file-entries/star`

Star files

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `entryIds` | массив integer | да |

Ответы: 204, 422, 403

### POST `/file-entries/unstar`

Unstar files

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `entryIds` | массив integer | да |

Ответы: 204, 422, 403

### GET `/file-entries/{id}/model`

Retrieve file metadata

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403, 404

### POST `/file-entries`

Upload a file

Тело запроса (multipart/form-data):

| Поле | Тип | Обязательно |
|---|---|---|
| `file` | string | да |
| `parentId` | integer/null | нет |
| `relativePath` | string/null | нет |

Ответы: 200, 403, 422

### POST `/file-entries/bulk-delete`

Bulk delete files

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `paths` | массив string | нет |
| `deleteForever` | boolean | нет |
| `emptyTrash` | boolean | нет |
| `entryIds` | массив integer | нет |

Ответы: 204, 422

### GET `/file-entries/download/{hashes}`

Download files

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `hashes` | path | string | да |

Ответы: 200, 404, 403

### POST `/file-entries/restore`

Restore deleted files

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `entryIds` | массив integer | да |

Ответы: 204, 422, 403

## Links

### GET `/file-entries/{entryId}/shareable-link`

Retrieve a shareable link

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `entryId` | path | integer | да |

Ответы: 200, 403

### POST `/file-entries/{entryId}/shareable-link`

Create a new shareable link

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `entryId` | path | integer | да |

Ответы: 200, 403, 422

### PUT `/file-entries/{entryId}/shareable-link`

Update a shareable link

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `entryId` | path | integer | да |

Ответы: 200, 403, 422

### DELETE `/file-entries/{entryId}/shareable-link`

Delete a shareable link

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `entryId` | path | integer | да |

Ответы: 204, 403

## Sharing

### POST `/file-entries/{id}/share`

Share files

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `emails` | массив string | да |
| `permissions` | object | да |

Ответы: 204, 422, 403, 404

### POST `/file-entries/bulk/unshare`

Unshare files

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `user_id` | integer | да |
| `entry_ids` | массив integer | да |

Ответы: 204, 422, 403

### PUT `/file-entries/{id}/change-permissions`

Change shared file permissions

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `permissions` | object | да |
| `user_id` | integer | да |

Ответы: 204, 422, 403, 404

## File requests

### GET `/file-requests`

List file requests

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `query` | query | string/null | нет |
| `per_page` | query | integer | нет |
| `page` | query | integer | нет |
| `sort` | query | string | нет |
| `workspace_id` | query | string | нет |
| `created_at` | query | string | нет |
| `updated_at` | query | string | нет |
| `deadline` | query | string | нет |
| `closed_at` | query | string | нет |

Ответы: 200, 403, 422

### POST `/file-requests`

Create a new file request

Ответы: 200, 403, 422

### GET `/file-requests/{id}`

Retrieve a file request

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403

### PUT `/file-requests/{id}`

Update a file request

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403, 404, 422

### DELETE `/file-requests/{id}`

Delete a file request

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 204, 403, 404

### POST `/file-requests/{id}/close`

Close a file request

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403, 404

### POST `/file-requests/{id}/reopen`

Reopen a closed file request

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403, 404

### POST `/file-requests/{id}/send-email`

Send file request link via email

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `emails` | массив object | да |

Ответы: 204, 403, 422, 404

## Tags

### GET `/tags`

List all tags

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `query` | query | string/null | нет |
| `per_page` | query | integer | нет |
| `page` | query | integer | нет |
| `sort` | query | string | нет |
| `workspace_id` | query | string | нет |
| `user_id` | query | integer | нет |
| `created_at` | query | string | нет |
| `updated_at` | query | string | нет |

Ответы: 200, 403, 422

### POST `/tags`

Create a tag

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `name` | string | да |

Ответы: 200, 403, 422

### PUT `/tags/{id}`

Update a tag

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `name` | string | нет |

Ответы: 200, 403, 422

### DELETE `/tags/bulk`

Delete tags

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `ids` | query | string | да |

Ответы: 204, 422, 403

## Workspaces

### GET `/workspaces`

List workspaces

Ответы: 200, 401

### POST `/workspaces`

Create a workspace

Ответы: 200, 403, 401, 422

### GET `/workspaces/{id}`

Retrieve a workspace

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403, 401

### PUT `/workspaces/{id}`

Update a workspace

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403, 401, 422

### DELETE `/workspaces/{id}`

Delete a workspace

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403, 401

### GET `/workspace/{id}/members`

List members

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403

### GET `/workspace/{id}/invites`

List invites

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Ответы: 200, 403

### DELETE `/workspace/{id}/member/{userId}`

Remove member

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |
| `userId` | path | integer | да |

Ответы: 200, 403

### POST `/workspace/{id}/invite`

Invite members

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `emails` | массив object | да |

Ответы: 200, 403, 422

### POST `/workspace/{id}/{inviteId}/resend`

Resend invite

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |
| `inviteId` | path | string | да |

Ответы: 200, 403

### POST `/workspace/{id}/member/{memberId}/change-role`

Change member's role

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |
| `memberId` | path | integer | да |

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `roleId` | integer | да |

Ответы: 204, 403, 422

### POST `/workspace/{id}/invite/{inviteId}/change-role`

Change invite's role

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `id` | path | integer | да |
| `inviteId` | path | string | да |

Тело запроса (application/json):

| Поле | Тип | Обязательно |
|---|---|---|
| `roleId` | integer | да |

Ответы: 204, 403, 422

### DELETE `/workspace/invite/{inviteId}`

Delete invite

| Параметр | Где | Тип | Обязателен |
|---|---|---|---|
| `inviteId` | path | string | да |

Ответы: 204, 403
