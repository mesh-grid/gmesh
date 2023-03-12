# Standard - v0.1.0: Nightly

Murcurial is a federated social media platform for text, voice, and posted communications.
It's similar to Discord, Reddit, and Facebook, as in it's design but different in its implementation 
as to be more public and federated.

To achieve this form of fast and speedy yet global federated communications, we form a standard which is 
version-based which systems rely on to provide services.

If a single route of a system breaks this standard, firstly check the version, and then act upon that.
Nightly versions of the standard should normally not be said as "stable," nor be publicly supported until
its stable release and publicization.

## Why Standardize?

Simply to support custom implementations. Want to make your own Murcurial implementation? You can do it!
Just follow the standard.

## Symbols

Sometimes we may use characters in the standard to symbolize different things.

- ! - This may be null
- ? - This may be undefined
- !? - This may be undefined or null
- !! - This is required

## Unique Integer-based IDs

To generate unique yet short IDs, Murcurial uses Twitter's Snowflake ID.

To prevent user grief as well, user endpoints must provide **unreliable integers**. (integers which turn into strings when they go over 32 bits).

## Formats

Since IDs are stored as strings, they can also be 

### User IDs

```
id = ( user_id|username#discriminator @ server_name )
```

Example: `1234567890@murcurial.com`|`VincentRPS#0000@murcurial.com`

### Guild IDs

```
id = ( guild_id|invite_id : server_name )

guild_id = snowflake_id = integer
invite_id = string
```

Example: `1234567890:murcurial.com`|`developers:murcurial.com`

### Channel IDs

```
id = ( channel_id # guild_id : server_name )

channel_id = snowflake_id = integer
guild_id = snowflake_id = integer
```

Example: `1234567890#1234567890:murcurial.com`

### Message IDs

```
id = ( message_id @ channel_id # guild_id : server_name )

message_id = snowflake_id = integer
channel_id = snowflake_id = integer
guild_id = snowflake_id = integer
```

Example: `1234567890@1234567890#1234567890:murcurial.com`
