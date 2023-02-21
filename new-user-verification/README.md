# New User Verification

Discord doesn't offer any level of protection against new accounts between "block 5 minute old accounts" and "require a valid phone number." I guess there's the raid system, but sometimes the bad actors come in a trickle instead of a pour.

Fortunately, YAGPDB lets us respond to joins and lock a potentially offending user in a ticket.

## [verify.go.tmpl](./verify.go.tmpl)

[jan Tepo (@tbodt)](https://github.com/tbodt) provided the `createdAt` code. Thanks!

#### Function

Checks the age of an account on join. If a user joins the server while their account is younger than `$minAgeDays`, a ticket will open up for that user, and request verification in some form.

#### Parameters

- `$minAgeDays` is the age, in days, of the oldest ticketable account.
- `$muteRole` is your configured mute role, the same one already used by YAGPDB.
  - This is a safety net if you use but misconfigure `$noViewRole`.
- `$noViewRole` is a role which removes permission to view almost every channel in the server.
  - Recommended. If done right, prevents seeing the member list, blocking DMs.
  - Separate from `$muteRole` so normal muted users can still see what they were muted for.

#### Notes

Note that Join Message commands do not log errors. If you set an invalid role, or otherwise break the command, the command will not work and you will get no feedback as to why.

## [unmute.go.tmpl](./unmute.go.tmpl)

#### Function

Remove the `noViewRole` from a given user when they are unmuted.

The user should already be muted if you configured the command as intended, so add this to the end of your unmute DM to combine the two.

#### Parameters

- `$noViewRole` is the same role as before.

#### Notes

If the user does not have the role, it will fail silently at the point you attempt to remove the role.
