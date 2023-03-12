# Standard - v0.1.0: Nightly

Crowdle is a federated social media platform for text, voice, and posted communications.
It's similar to Discord, Reddit, and Facebook, as in it's design but different in its implementation 
as to be more public and federated.

To achieve this form of fast and speedy yet global federated communications, we form a standard which is 
version-based which systems rely on to provide services.

If a single route of a system breaks this standard, firstly check the version, and then act upon that.
Nightly versions of the standard should normally not be said as "stable," nor be publicly supported until
its stable release and publicization.

## Why Standardize?

Simply to support custom implementations. Want to make your own Crowdle implementation? You can do it!
Just follow the standard.

## Symbols

Sometimes we may use characters in the standard to symbolize different things.

- ! - This may be null
- ? - This may be undefined
- !? - This may be undefined or null
- !! - This is required

## Unique Integer-based IDs

To generate unique yet short IDs, Crowdle uses Twitter's Snowflake ID.
