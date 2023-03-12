# Guild - Rooms for Communities

Guilds in Crowdle are treated like if a community. They have members, those members have presences, and more.

## Guild Object

Guilds can be referred to on the platform via a uniquely made invite code, or id
like `1234567890:crowdle.org` or `developers:crowdle.org`.


| field name    | type     |
| ------------- | -------- |
| id            | integer  |
| name          | string   |
| owner_id      | integer  |
| ?flags        | integer  |
| permissions?  | integer  |


* `owner_id`: This **must** be a user present on the platform that the Guild is located in.
* `flags`: If present, must be a bitwise integer following the flags standard.
* `permissions`:
    - If present, must be a bitwise integer following the permissions standard.
    - If over 64 bits, **must** be converted to a string.

## Guild Flags

Bitwise-based integer flags for Guilds.

| flag      | value |
| --------- | ----- |
| verified  | 0     |
| partnered | 1     |
| official  | 2     |
| nightly   | 3     |

* `nightly`: If present, this guild **must** have nightly-enabled features activated.

## Member Object

| field name | type     |
| ---------- | -------- |
| user_id    | integer  |
| guild_id   | integer  |
| !nick      | string   |
| snowfish   | string   |

* `user_id`: **Must** be a user present on `snowfish`.
* `snowfish`: **Must** be a valid IP or domain to the Snowfish protocol.
