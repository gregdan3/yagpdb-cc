# Talk

Sometimes you want to have a conversation with a user, and indicate that it is a mod action, without leading with a warning or mute.

## [talk.go.tmpl](./talk.go.tmpl)

#### Function

Given a user and target reason, create a ticket named after the user and given reason to have an internal discussion with that user.

#### Parameters

- `$logChannel` is the ID of YAGPDB's configured logging channel. You may use any other channel, but the point is to mimic YAGPDB's logging.

#### Notes

- I recommend limiting the command to use by moderators. This is essentially a moderation command, and creates a ticket on another user's behalf.
- This command would ideally send a DM to the target user, but YAGPDB does not have a way to send DMs.
- Right now, there is no corresponding command to indicate the discussion is over
