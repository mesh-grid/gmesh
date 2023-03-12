# Channels - Decentralized Message Portals

Channels are decentralized portals for messages.

## Channel Object

| field name | type     |
| ---------- | -------- |
| id         | integer  |
| name       | string   |
| guild_id   | integer  |
| !parent_id | integer  |

* `guild_id`: **Must** be a valid guild.
* `parent_id`: If present, **must** be a valid channel.

## Message Object

| field name        | type     |
| ----------------- | -------- |
| id                | integer  |
| author_id         | integer  |
| channel_id        | integer  |
| content           | string   |
| timestamp         | integer  |
| !edited_timestamp | integer  |

* `author_id`: **Must** be a valid user.
* `channel_id`: **Must** be a valid channel.
