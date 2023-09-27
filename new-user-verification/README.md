# New User Verification

Discord doesn't offer any level of protection against new accounts between "block 5 minute old accounts" and "require a valid phone number." There's the raid system, but sometimes the bad actors come in a trickle instead of a pour.

Fortunately, YAGPDB lets us respond to joins and lock a potentially offending user in a ticket.

[jan Tepo (@tbodt)](https://github.com/tbodt) provided the `createdAt` code in both `acc-age.go.tmpl` and `creation-date.go.tmpl`. Thanks!

## [acc-age.go.tmpl](./acc-age.go.tmpl) and [creation-date.go.tmpl](./creation-date.go.tmpl)

#### Function

Checks the age of an account on join. The command will create a ticket for that account the moment they join if:

- The account is younger than `$minAccAgeDays` days in `acc-age.go.tmpl`
- The account was created after `$minCreationDate` in `creation-date.go.tmpl`,

#### Parameters

- In `acc-age.go.tmpl`, `$minAgeDays` is the age, in days, of the oldest age of account that will be ticketed.
- In `creation-date.go.tmpl`, `$minCreationDate` is the date, in `YYYY MM DD HH MM SS` format, of the oldest account that will be ticketed.
- `$muteRole` is your configured mute role, the same one already used by YAGPDB.
- `$noViewRole` is an optional role which removes permission to view almost every channel in the server.
  - Recommended. If done right, prevents seeing the member list, blocking DMs. Does not prevent viewing public servers due to Discord's server preview feature.
  - Separate from `$muteRole` so normal muted users can still see what they were muted for.
  - If configured, remove the comment delimiters (`/* */`) from the variable and where the role is added, as well as from the `letin.go.tmpl` command.

#### Notes

Join Message commands do not log errors. If you set an invalid role, or otherwise break the command, the command will not work and you will get no feedback as to why.

## [letin.go.tmpl](./letin.go.tmpl)

#### Function

Remove `muteRole` and optionally `noViewRole` from a given user.

#### Parameters

- `$muteRole` is the same role as before.
- `$noViewRole` is the same role as before.

#### Notes

If the user does not have the role, the command will fail at the point you attempt to remove the role.
