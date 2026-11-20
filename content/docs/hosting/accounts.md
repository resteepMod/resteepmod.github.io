---
title: Accounts and players
weight: 10
---

# Accounts and players

Every player has an account on the server: an email and a password, which Ubisoft Connect signs in with. These are
accounts on that ReSteep server only, never Ubisoft accounts. The password is stored only as a scrypt hash and never
logged; wrong passwords are rate-limited per address.

## Who becomes which player

- **The host** plays as the server's own player without typing anything: the launcher signs in with its own
  credentials.
- **The first account** registered on the server's own PC (or made with `admin account-create`) takes over the
  player already there, for example your imported progress.
- **Every other account**, and one registered from another PC, starts like a new Ubisoft account: level 1, an empty
  inventory and the server's `starting_credits`.

With a server password, a guest's PC must give it (ReSteep asks for it when they first join) before it can make an
account or sign in. Once accounts exist, every call that acts for a player needs that player's session, and a player
changes only their own inventory, rider card, saves and photos. With `registration = "closed"` under `[players]`, only
the host creates accounts.

## Players who join

A player who joins makes their account in ReSteep the first time (or signs in with one they made before). Their
launcher then tells the server, with the password, to let Ubisoft Connect on their PC sign in as that account for the
next ten minutes. Connect signs in as them, whatever account it remembers.

> [!NOTE]
> Players behind one internet address who start Ubisoft Connect within those ten minutes could be taken for each
> other.

## Managing accounts

If someone forgets their password, the host sets a new one:

```
powder-server admin accounts                          # email -> player
powder-server admin account-create <email> <name>     # asks for the password
powder-server admin account-password <email>          # asks for the new password
powder-server admin account-email <email> <new email>
powder-server admin owner-name [NAME]                 # the server owner's player name
powder-server admin account-link <email> <player id>  # the account owns that player instead
```

## Bringing your progress along

To continue with your progress from Ubisoft's servers, import it once from recordings of your own online sessions,
then register: the first account takes it over.

```
powder-server admin import <recordings>             # level, credits, items, stats, rider card, achievements
powder-server admin import <recordings> --replace
```

After the import the server never reads the recordings again. Recordings hold personal data (your account, friends,
other players on leaderboards): keep them private.
