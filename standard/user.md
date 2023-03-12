# User - You!

Users make the backbone of Crowdle. They power, and do all the actions on the platform.
Bots are simply just users with a special flag.

## User Object

| field name    | type     |
| ------------- | -------- |
| id            | integer  |
| username      | string   |
| discriminator | string   |
| email         | string   |
| flags         | integer  |

* `discriminator`: **Must** be a 4 length integer wrapped with a string.
* `email`: Should only be shown within the home Snowfish.
* `flags`: **Must** follow the user flag standard.

## User Flags

| field name    | type     |
| ------------- | -------- |
| owner         | 0        |
| bot           | 1        |
| system        | 2        |

