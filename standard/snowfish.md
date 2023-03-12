# Snowfish - System of Federation

Murcurial relies upon a system of global federation called Snowfish.

The [Specimen] standard already explains how Snowfish systems communicate versioning,
and many miscellaneous things. But, this now is further more for communication directly.

In terms of Snowfish server naming, [we follow the Matrix spec here](https://spec.matrix.org/v1.6/appendices/#server-name).

However, unlike the Matrix spec, we have case-insensitivity for server naming.

Snowfish endpoints, unlike user ones, should have **reliable** integers instead of the normal unreliable.

## Authorizing Snowfish Servers

### `/_snowfish/v0/server`

Gives an external Snowfish server insight into this Snowfish server.

| field name | type     |
| ---------- | -------- |
| location   | string   |

* `location`: **Must** be a valid server name, and **must** be used for Snowfish requests.

### `/_snowfish/v0/pub`

Gives the servers current public ed25519 key.

| field name | type     |
| ---------- | -------- |
| expire_sec | integer  |
| signature  | string   |
| key        | string   |

* `signature`: **Must** be a base64-encoded signature signed with `key`.
* `key`: **Must** be a base64-encoded ed25519 public key.
* `expire_sec`: **Must** be a UTC-based UNIX timestamp set in the future.

`expire_sec` must be used by other Snowfish servers to know when to re-request for public keys.

The `key` identifies whether you are the server sending a valid event, requesting to join a guild, or other such.

### `/_snowfish/v0/target`

**RATE-LIMIT**: 3/10 minutes. Should be cached by servers.

Used by servers to get keys. It should be expected that the server being requested
requests to the external server's pub endpoint after this.

| field name | type     |
| ---------- | -------- |
| server     | string   |
| signature  | string   |

* `server`: Valid server name.
* `signature`: Valid signature, should be verifiable with `key`. Should be encoded with base64.

#### Returns

| field name    | type     |
| ------------- | -------- |
| expires_sec   | integer  |
| token         | string   |

* `expires_sec`: When this token will expire in a UTC-based UNIX timestamp. At minimum, must be at least 4 minutes in the future.
* `token`: This can be of minimum 1 length, and maximum 124.

## External Guilds

Users, being who they are, are allowed to join external guilds.
However, they **are not** able to create guilds on external Snowfishes.

For a user to join external guilds, they **must** provide an invite created on the external Snowfish.

On `_snowfish` endpoints, the ids of Guilds are stringified into the following:

```txt
:id = (:integer_guild_id : :server_name)
```

Something like `1234567890:murcurial.com`.

### `/_snowfish/v0/guilds/push`

Pushes an event to a Guild.

| field name    | type     |
| ------------- | -------- |
| _origin       | string   |
| _ts           | integer  |
| _ev           | string   |
| signature     | string   |
| origin_user   | user     |
| guild_id      | integer  |
| data          | object   |

* `_origin`: **Must** be the originating server.
* `_ts`: The event timestamp.
* `_ev`: The event type being sent. Must follow the Snowfish event type proclamation.
* `signature`: Signature following the originating server's key.
* `origin_user`: The user invoking this event.
* `guild_id`: Where this event is being sent.
* `data`: The valid event data, in contrast with `_ev`.

#### Example

```json
{
    "_origin": "http://murcurial.com",
    "_ts": 1234567890,
    "_ev": "gc.message_create",
    "signature": "...",
    "origin_user": {
        "id": 1234567890,
        "username": "VincentRPS",
        "discriminator": "0000",
        "flags": 0
    },
    "guild_id": 1234567890,
    "data": {
        "id": 1234567890,
        "author_id": 1234567890,
        "channel_id": 1234567890,
        "content": "Good Morning!",
        "timestamp": 1678599385,
        "edited_timestamp": null
    }
}
```

#### Errors

If an error occurs, such as permissions or other such, the server must return a detailed
exemplementation structured like so:

```json
{
    "t": "failure",
    "errors": [
        {
            "e": "origin_user",
            "_errors": [
                "Forbidden Permissions",
                "Not a member of this guild"
            ]
        },
        {
            "e": "signature",
            "_errors": [
                "Invalid Signature"
            ]
        },
        {
            "e": "authorization",
            "_errors": [
                "Unregistered Snowfish server"
            ]
        }
    ]
}
```
