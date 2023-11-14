# New User Verification

Discord doesn't offer much protection against new accounts between "block 5 minute old accounts" and "require a valid phone number."
The raid system can help with bursts of abuse, but not with abusers that come over time.

YAGPDB lets us respond to joins and lock too-new users in a ticket.

[jan Tepo (@tbodt)](https://github.com/tbodt) provided the `createdAt` code in both `account-age.go.tmpl` and `creation-date.go.tmpl`. Thanks!

## [account-age.go.tmpl](./account-age.go.tmpl) and [creation-date.go.tmpl](./creation-date.go.tmpl)

#### Function

Checks the age of an account on join.
The command will create a ticket for that account the moment they join or finish onboarding (if configured), if:

- The account is younger than `$minAccAgeDays` days in `account-age.go.tmpl`
- The account was created after `$minCreationDate` in `creation-date.go.tmpl`.

#### Parameters

- In `account-age.go.tmpl`, `$minAgeDays` is the age, in days, of the oldest age of account that will be ticketed.
- In `creation-date.go.tmpl`, `$minCreationDate` is the date, in `YYYY MM DD HH MM SS` format, of the oldest account that will be ticketed.
- `$muteRole` is your configured mute role, the same one used by YAGPDB.

#### Notes

Join Message commands do not log errors.
If you set an invalid role or otherwise break the command, the command will not work and you will not get an error.

## [letin.go.tmpl](./letin.go.tmpl)

#### Function

Remove `muteRole` from a given user.

#### Parameters

- `$muteRole` is the same role as before.

#### Notes

If the user does not have the role, the command will fail at the point you attempt to remove the role.
This will throw an error since this is a normal custom command.
