# Channels - Decentralized Message Portals

Channels are decentralized portals for messages.

## Channel Object

| field name | type     |
| ---------- | -------- |
| id         | string   |
| name       | string   |
| guild_id   | integer  |
| !parent_id | integer  |

* `id`: **Must** follow the Gmesh channel format.
* `guild_id`: **Must** be a valid guild.
* `parent_id`: If present, **must** be a valid channel.

## Message Object

| field name        | type     |
| ----------------- | -------- |
| id                | string   |
| author_id         | integer  |
| channel_id        | integer  |
| content           | string   |
| timestamp         | integer  |
| !edited_timestamp | integer  |

* `id`: **Must** follow the Gmesh message format.
* `author_id`: **Must** be a valid user.
* `channel_id`: **Must** be a valid channel.
