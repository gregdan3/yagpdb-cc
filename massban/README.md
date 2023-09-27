# Mass Ban

Discord doesn't offer a way to ban a large number of users at once.

## [massban.go.tmpl](./massban.go.tmpl)

#### Function

Ban a list of users by their IDs in batches of 5 (the maximum number of `execAdmin` that a single custom command may execute). There is no limit on the number of IDs that may be provided, except for the maximum length of a message. The message may be as long as Nitro allows.

#### Parameters

- `$sendto` is the ID of a channel which YAGPDB will send results to. I recommend using an internal channel, as the command is very noisy, but that is up to you.

- `$thiscc` is not a parameter you can choose; you must fill in the ID of the custom command. This is found in the upper left of the custom command's page.
- `$ratelimitdelay` is not a parameter either; it is a constant used to avoid YAGPDB's max number of custom commands executed per minute.

#### Notes

- Do not run more than one instance of this command at once. You'll defeat the purpose of the rate limiting!
- It is **highly** recommended to limit the command to both your admin role and to a specific channel, to not risk it being executed by a non-admin.
