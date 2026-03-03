---
name: slack-web-api
description: "Slack Web API skill. Use when working with Slack Web for admin.apps.approve, admin.apps.approved.list, admin.apps.requests.list. Covers 174 endpoints."
version: 1.0.0
generator: lapsh
---

# Slack Web API
API version: 1.7.0

## Auth
OAuth2

## Base URL
https://slack.com/api

## Setup
1. Configure auth: OAuth2
2. GET /admin.apps.approved.list -- verify access
3. POST /admin.apps.approve -- create first admin.apps.approve

## Endpoints

174 endpoints across 174 groups. See references/api-spec.lap for full details.

### admin.apps.approve
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.apps.approve | Approve an app for installation on a workspace. |

### admin.apps.approved.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.apps.approved.list | List approved apps for an org or workspace. |

### admin.apps.requests.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.apps.requests.list | List app requests for a team/workspace. |

### admin.apps.restrict
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.apps.restrict | Restrict an app for installation on a workspace. |

### admin.apps.restricted.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.apps.restricted.list | List restricted apps for an org or workspace. |

### admin.conversations.archive
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.archive | Archive a public or private channel. |

### admin.conversations.convertToPrivate
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.convertToPrivate | Convert a public channel to a private channel. |

### admin.conversations.create
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.create | Create a public or private channel-based conversation. |

### admin.conversations.delete
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.delete | Delete a public or private channel. |

### admin.conversations.disconnectShared
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.disconnectShared | Disconnect a connected channel from one or more workspaces. |

### admin.conversations.ekm.listOriginalConnectedChannelInfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.conversations.ekm.listOriginalConnectedChannelInfo | List all disconnected channels—i.e., channels that were once connected to other workspaces and then disconnected—and the corresponding original channel IDs for key revocation with EKM. |

### admin.conversations.getConversationPrefs
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.conversations.getConversationPrefs | Get conversation preferences for a public or private channel. |

### admin.conversations.getTeams
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.conversations.getTeams | Get all the workspaces a given public or private channel is connected to within this Enterprise org. |

### admin.conversations.invite
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.invite | Invite a user to a public or private channel. |

### admin.conversations.rename
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.rename | Rename a public or private channel. |

### admin.conversations.restrictAccess.addGroup
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.restrictAccess.addGroup | Add an allowlist of IDP groups for accessing a channel |

### admin.conversations.restrictAccess.listGroups
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.conversations.restrictAccess.listGroups | List all IDP Groups linked to a channel |

### admin.conversations.restrictAccess.removeGroup
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.restrictAccess.removeGroup | Remove a linked IDP group linked from a private channel |

### admin.conversations.search
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.conversations.search | Search for public or private channels in an Enterprise organization. |

### admin.conversations.setConversationPrefs
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.setConversationPrefs | Set the posting permissions for a public or private channel. |

### admin.conversations.setTeams
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.setTeams | Set the workspaces in an Enterprise grid org that connect to a public or private channel. |

### admin.conversations.unarchive
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.conversations.unarchive | Unarchive a public or private channel. |

### admin.emoji.add
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.emoji.add | Add an emoji. |

### admin.emoji.addAlias
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.emoji.addAlias | Add an emoji alias. |

### admin.emoji.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.emoji.list | List emoji for an Enterprise Grid organization. |

### admin.emoji.remove
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.emoji.remove | Remove an emoji across an Enterprise Grid organization |

### admin.emoji.rename
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.emoji.rename | Rename an emoji. |

### admin.inviteRequests.approve
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.inviteRequests.approve | Approve a workspace invite request. |

### admin.inviteRequests.approved.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.inviteRequests.approved.list | List all approved workspace invite requests. |

### admin.inviteRequests.denied.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.inviteRequests.denied.list | List all denied workspace invite requests. |

### admin.inviteRequests.deny
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.inviteRequests.deny | Deny a workspace invite request. |

### admin.inviteRequests.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.inviteRequests.list | List all pending workspace invite requests. |

### admin.teams.admins.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.teams.admins.list | List all of the admins on a given workspace. |

### admin.teams.create
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.teams.create | Create an Enterprise team. |

### admin.teams.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.teams.list | List all teams on an Enterprise organization |

### admin.teams.owners.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.teams.owners.list | List all of the owners on a given workspace. |

### admin.teams.settings.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.teams.settings.info | Fetch information about settings in a workspace |

### admin.teams.settings.setDefaultChannels
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.teams.settings.setDefaultChannels | Set the default channels of a workspace. |

### admin.teams.settings.setDescription
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.teams.settings.setDescription | Set the description of a given workspace. |

### admin.teams.settings.setDiscoverability
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.teams.settings.setDiscoverability | An API method that allows admins to set the discoverability of a given workspace |

### admin.teams.settings.setIcon
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.teams.settings.setIcon | Sets the icon of a workspace. |

### admin.teams.settings.setName
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.teams.settings.setName | Set the name of a given workspace. |

### admin.usergroups.addChannels
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.usergroups.addChannels | Add one or more default channels to an IDP group. |

### admin.usergroups.addTeams
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.usergroups.addTeams | Associate one or more default workspaces with an organization-wide IDP group. |

### admin.usergroups.listChannels
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.usergroups.listChannels | List the channels linked to an org-level IDP group (user group). |

### admin.usergroups.removeChannels
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.usergroups.removeChannels | Remove one or more default channels from an org-level IDP group (user group). |

### admin.users.assign
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.users.assign | Add an Enterprise user to a workspace. |

### admin.users.invite
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.users.invite | Invite a user to a workspace. |

### admin.users.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin.users.list | List users on a workspace |

### admin.users.remove
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.users.remove | Remove a user from a workspace. |

### admin.users.session.invalidate
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.users.session.invalidate | Invalidate a single session for a user by session_id |

### admin.users.session.reset
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.users.session.reset | Wipes all valid sessions on all devices for a given user |

### admin.users.setAdmin
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.users.setAdmin | Set an existing guest, regular user, or owner to be an admin user. |

### admin.users.setExpiration
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.users.setExpiration | Set an expiration for a guest user |

### admin.users.setOwner
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.users.setOwner | Set an existing guest, regular user, or admin user to be a workspace owner. |

### admin.users.setRegular
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin.users.setRegular | Set an existing guest user, admin user, or owner to be a regular user. |

### api.test
| Method | Path | Description |
|--------|------|-------------|
| GET | /api.test | Checks API calling code. |

### apps.event.authorizations.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps.event.authorizations.list | Get a list of authorizations for the given event context. Each authorization represents an app installation that the event is visible to. |

### apps.permissions.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps.permissions.info | Returns list of permissions this app has on a team. |

### apps.permissions.request
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps.permissions.request | Allows an app to request additional scopes |

### apps.permissions.resources.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps.permissions.resources.list | Returns list of resource grants this app has on a team. |

### apps.permissions.scopes.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps.permissions.scopes.list | Returns list of scopes this app has on a team. |

### apps.permissions.users.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps.permissions.users.list | Returns list of user grants and corresponding scopes this app has on a team. |

### apps.permissions.users.request
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps.permissions.users.request | Enables an app to trigger a permissions modal to grant an app access to a user access scope. |

### apps.uninstall
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps.uninstall | Uninstalls your app from a workspace. |

### auth.revoke
| Method | Path | Description |
|--------|------|-------------|
| GET | /auth.revoke | Revokes a token. |

### auth.test
| Method | Path | Description |
|--------|------|-------------|
| GET | /auth.test | Checks authentication & identity. |

### bots.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /bots.info | Gets information about a bot user. |

### calls.add
| Method | Path | Description |
|--------|------|-------------|
| POST | /calls.add | Registers a new Call. |

### calls.end
| Method | Path | Description |
|--------|------|-------------|
| POST | /calls.end | Ends a Call. |

### calls.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /calls.info | Returns information about a Call. |

### calls.participants.add
| Method | Path | Description |
|--------|------|-------------|
| POST | /calls.participants.add | Registers new participants added to a Call. |

### calls.participants.remove
| Method | Path | Description |
|--------|------|-------------|
| POST | /calls.participants.remove | Registers participants removed from a Call. |

### calls.update
| Method | Path | Description |
|--------|------|-------------|
| POST | /calls.update | Updates information about a Call. |

### chat.delete
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat.delete | Deletes a message. |

### chat.deleteScheduledMessage
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat.deleteScheduledMessage | Deletes a pending scheduled message from the queue. |

### chat.getPermalink
| Method | Path | Description |
|--------|------|-------------|
| GET | /chat.getPermalink | Retrieve a permalink URL for a specific extant message |

### chat.meMessage
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat.meMessage | Share a me message into a channel. |

### chat.postEphemeral
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat.postEphemeral | Sends an ephemeral message to a user in a channel. |

### chat.postMessage
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat.postMessage | Sends a message to a channel. |

### chat.scheduleMessage
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat.scheduleMessage | Schedules a message to be sent to a channel. |

### chat.scheduledMessages.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /chat.scheduledMessages.list | Returns a list of scheduled messages. |

### chat.unfurl
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat.unfurl | Provide custom unfurl behavior for user-posted URLs |

### chat.update
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat.update | Updates a message. |

### conversations.archive
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.archive | Archives a conversation. |

### conversations.close
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.close | Closes a direct message or multi-person direct message. |

### conversations.create
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.create | Initiates a public or private channel-based conversation |

### conversations.history
| Method | Path | Description |
|--------|------|-------------|
| GET | /conversations.history | Fetches a conversation's history of messages and events. |

### conversations.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /conversations.info | Retrieve information about a conversation. |

### conversations.invite
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.invite | Invites users to a channel. |

### conversations.join
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.join | Joins an existing conversation. |

### conversations.kick
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.kick | Removes a user from a conversation. |

### conversations.leave
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.leave | Leaves a conversation. |

### conversations.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /conversations.list | Lists all channels in a Slack team. |

### conversations.mark
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.mark | Sets the read cursor in a channel. |

### conversations.members
| Method | Path | Description |
|--------|------|-------------|
| GET | /conversations.members | Retrieve members of a conversation. |

### conversations.open
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.open | Opens or resumes a direct message or multi-person direct message. |

### conversations.rename
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.rename | Renames a conversation. |

### conversations.replies
| Method | Path | Description |
|--------|------|-------------|
| GET | /conversations.replies | Retrieve a thread of messages posted to a conversation |

### conversations.setPurpose
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.setPurpose | Sets the purpose for a conversation. |

### conversations.setTopic
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.setTopic | Sets the topic for a conversation. |

### conversations.unarchive
| Method | Path | Description |
|--------|------|-------------|
| POST | /conversations.unarchive | Reverses conversation archival. |

### dialog.open
| Method | Path | Description |
|--------|------|-------------|
| GET | /dialog.open | Open a dialog with a user |

### dnd.endDnd
| Method | Path | Description |
|--------|------|-------------|
| POST | /dnd.endDnd | Ends the current user's Do Not Disturb session immediately. |

### dnd.endSnooze
| Method | Path | Description |
|--------|------|-------------|
| POST | /dnd.endSnooze | Ends the current user's snooze mode immediately. |

### dnd.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /dnd.info | Retrieves a user's current Do Not Disturb status. |

### dnd.setSnooze
| Method | Path | Description |
|--------|------|-------------|
| POST | /dnd.setSnooze | Turns on Do Not Disturb mode for the current user, or changes its duration. |

### dnd.teamInfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /dnd.teamInfo | Retrieves the Do Not Disturb status for up to 50 users on a team. |

### emoji.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /emoji.list | Lists custom emoji for a team. |

### files.comments.delete
| Method | Path | Description |
|--------|------|-------------|
| POST | /files.comments.delete | Deletes an existing comment on a file. |

### files.delete
| Method | Path | Description |
|--------|------|-------------|
| POST | /files.delete | Deletes a file. |

### files.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /files.info | Gets information about a file. |

### files.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /files.list | List for a team, in a channel, or from a user with applied filters. |

### files.remote.add
| Method | Path | Description |
|--------|------|-------------|
| POST | /files.remote.add | Adds a file from a remote service |

### files.remote.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /files.remote.info | Retrieve information about a remote file added to Slack |

### files.remote.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /files.remote.list | Retrieve information about a remote file added to Slack |

### files.remote.remove
| Method | Path | Description |
|--------|------|-------------|
| POST | /files.remote.remove | Remove a remote file. |

### files.remote.share
| Method | Path | Description |
|--------|------|-------------|
| GET | /files.remote.share | Share a remote file into a channel. |

### files.remote.update
| Method | Path | Description |
|--------|------|-------------|
| POST | /files.remote.update | Updates an existing remote file. |

### files.revokePublicURL
| Method | Path | Description |
|--------|------|-------------|
| POST | /files.revokePublicURL | Revokes public/external sharing access for a file |

### files.sharedPublicURL
| Method | Path | Description |
|--------|------|-------------|
| POST | /files.sharedPublicURL | Enables a file for public/external sharing. |

### files.upload
| Method | Path | Description |
|--------|------|-------------|
| POST | /files.upload | Uploads or creates a file. |

### migration.exchange
| Method | Path | Description |
|--------|------|-------------|
| GET | /migration.exchange | For Enterprise Grid workspaces, map local user IDs to global user IDs |

### oauth.access
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth.access | Exchanges a temporary OAuth verifier code for an access token. |

### oauth.token
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth.token | Exchanges a temporary OAuth verifier code for a workspace token. |

### oauth.v2.access
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth.v2.access | Exchanges a temporary OAuth verifier code for an access token. |

### pins.add
| Method | Path | Description |
|--------|------|-------------|
| POST | /pins.add | Pins an item to a channel. |

### pins.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /pins.list | Lists items pinned to a channel. |

### pins.remove
| Method | Path | Description |
|--------|------|-------------|
| POST | /pins.remove | Un-pins an item from a channel. |

### reactions.add
| Method | Path | Description |
|--------|------|-------------|
| POST | /reactions.add | Adds a reaction to an item. |

### reactions.get
| Method | Path | Description |
|--------|------|-------------|
| GET | /reactions.get | Gets reactions for an item. |

### reactions.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /reactions.list | Lists reactions made by a user. |

### reactions.remove
| Method | Path | Description |
|--------|------|-------------|
| POST | /reactions.remove | Removes a reaction from an item. |

### reminders.add
| Method | Path | Description |
|--------|------|-------------|
| POST | /reminders.add | Creates a reminder. |

### reminders.complete
| Method | Path | Description |
|--------|------|-------------|
| POST | /reminders.complete | Marks a reminder as complete. |

### reminders.delete
| Method | Path | Description |
|--------|------|-------------|
| POST | /reminders.delete | Deletes a reminder. |

### reminders.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /reminders.info | Gets information about a reminder. |

### reminders.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /reminders.list | Lists all reminders created by or for a given user. |

### rtm.connect
| Method | Path | Description |
|--------|------|-------------|
| GET | /rtm.connect | Starts a Real Time Messaging session. |

### search.messages
| Method | Path | Description |
|--------|------|-------------|
| GET | /search.messages | Searches for messages matching a query. |

### stars.add
| Method | Path | Description |
|--------|------|-------------|
| POST | /stars.add | Adds a star to an item. |

### stars.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /stars.list | Lists stars for a user. |

### stars.remove
| Method | Path | Description |
|--------|------|-------------|
| POST | /stars.remove | Removes a star from an item. |

### team.accessLogs
| Method | Path | Description |
|--------|------|-------------|
| GET | /team.accessLogs | Gets the access logs for the current team. |

### team.billableInfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /team.billableInfo | Gets billable users information for the current team. |

### team.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /team.info | Gets information about the current team. |

### team.integrationLogs
| Method | Path | Description |
|--------|------|-------------|
| GET | /team.integrationLogs | Gets the integration logs for the current team. |

### team.profile.get
| Method | Path | Description |
|--------|------|-------------|
| GET | /team.profile.get | Retrieve a team's profile. |

### usergroups.create
| Method | Path | Description |
|--------|------|-------------|
| POST | /usergroups.create | Create a User Group |

### usergroups.disable
| Method | Path | Description |
|--------|------|-------------|
| POST | /usergroups.disable | Disable an existing User Group |

### usergroups.enable
| Method | Path | Description |
|--------|------|-------------|
| POST | /usergroups.enable | Enable a User Group |

### usergroups.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /usergroups.list | List all User Groups for a team |

### usergroups.update
| Method | Path | Description |
|--------|------|-------------|
| POST | /usergroups.update | Update an existing User Group |

### usergroups.users.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /usergroups.users.list | List all users in a User Group |

### usergroups.users.update
| Method | Path | Description |
|--------|------|-------------|
| POST | /usergroups.users.update | Update the list of users for a User Group |

### users.conversations
| Method | Path | Description |
|--------|------|-------------|
| GET | /users.conversations | List conversations the calling user may access. |

### users.deletePhoto
| Method | Path | Description |
|--------|------|-------------|
| POST | /users.deletePhoto | Delete the user profile photo |

### users.getPresence
| Method | Path | Description |
|--------|------|-------------|
| GET | /users.getPresence | Gets user presence information. |

### users.identity
| Method | Path | Description |
|--------|------|-------------|
| GET | /users.identity | Get a user's identity. |

### users.info
| Method | Path | Description |
|--------|------|-------------|
| GET | /users.info | Gets information about a user. |

### users.list
| Method | Path | Description |
|--------|------|-------------|
| GET | /users.list | Lists all users in a Slack team. |

### users.lookupByEmail
| Method | Path | Description |
|--------|------|-------------|
| GET | /users.lookupByEmail | Find a user with an email address. |

### users.profile.get
| Method | Path | Description |
|--------|------|-------------|
| GET | /users.profile.get | Retrieves a user's profile information. |

### users.profile.set
| Method | Path | Description |
|--------|------|-------------|
| POST | /users.profile.set | Set the profile information for a user. |

### users.setActive
| Method | Path | Description |
|--------|------|-------------|
| POST | /users.setActive | Marked a user as active. Deprecated and non-functional. |

### users.setPhoto
| Method | Path | Description |
|--------|------|-------------|
| POST | /users.setPhoto | Set the user profile photo |

### users.setPresence
| Method | Path | Description |
|--------|------|-------------|
| POST | /users.setPresence | Manually sets user presence. |

### views.open
| Method | Path | Description |
|--------|------|-------------|
| GET | /views.open | Open a view for a user. |

### views.publish
| Method | Path | Description |
|--------|------|-------------|
| GET | /views.publish | Publish a static view for a User. |

### views.push
| Method | Path | Description |
|--------|------|-------------|
| GET | /views.push | Push a view onto the stack of a root view. |

### views.update
| Method | Path | Description |
|--------|------|-------------|
| GET | /views.update | Update an existing view. |

### workflows.stepCompleted
| Method | Path | Description |
|--------|------|-------------|
| GET | /workflows.stepCompleted | Indicate that an app's step in a workflow completed execution. |

### workflows.stepFailed
| Method | Path | Description |
|--------|------|-------------|
| GET | /workflows.stepFailed | Indicate that an app's step in a workflow failed to execute. |

### workflows.updateStep
| Method | Path | Description |
|--------|------|-------------|
| GET | /workflows.updateStep | Update the configuration for a workflow extension step. |

## Enhanced Skill Content


## Question Mapping

- "How do I send a message to a channel?" -> POST /chat.postMessage
- "How do I list all channels in the workspace?" -> GET /conversations.list
- "How do I find a user by their email address?" -> GET /users.lookupByEmail
- "How do I get the message history of a channel?" -> GET /conversations.history
- "How do I upload a file to Slack?" -> POST /files.upload
- "How do I add a reaction to a message?" -> POST /reactions.add
- "How do I search for messages across the workspace?" -> GET /search.messages
- "How do I create a new channel?" -> POST /conversations.create
- "How do I invite a user to a channel?" -> POST /conversations.invite
- "How do I set a user's Do Not Disturb snooze?" -> POST /dnd.setSnooze
- "How do I get thread replies for a message?" -> GET /conversations.replies
- "How do I schedule a message for later?" -> POST /chat.scheduleMessage
- "How do I list all members of a channel?" -> GET /conversations.members
- "How do I verify my bot's authentication token?" -> GET /auth.test
- "How do I add a custom emoji to the workspace?" -> POST /admin.emoji.add

## Response Tips

- **Conversations/Users/Files lists**: All return cursor-based pagination; check `response_metadata.next_cursor` and pass it as `cursor` on the next call. An empty string means no more pages.
- **Chat methods**: `chat.postMessage` and `chat.update` return `ts` (timestamp) which is the message ID; save it for edits, deletions, and threading.
- **All endpoints**: Every response includes a top-level `ok` boolean. When `ok: false`, read the `error` string field for the machine-readable error code (e.g., `channel_not_found`, `not_authed`).
- **Files**: `files.info` nests comments and reactions inside the `file` object; use `count`/`page` params to paginate comments.
- **Search**: `search.messages` wraps results in `messages.matches[]` with `total` and `paging` for offset-based pagination (not cursor).
- **Admin endpoints**: Require Enterprise Grid org-level tokens with admin scopes; standard bot tokens will return `missing_scope`.

## Anomaly Flags

- **`ok: false` with `error: ratelimited`**: Surface immediately with the `Retry-After` header value. Slack enforces per-method tier limits (Tier 1 = 1/min, Tier 4 = 100+/min).
- **`error: token_revoked` or `error: not_authed`**: The OAuth token has been invalidated. Alert the user to reauthorize.
- **`error: missing_scope`**: The token lacks a required OAuth scope. Surface the needed scope so the user can update their app permissions.
- **`error: account_inactive`**: The target user has been deactivated. Flag this when bulk-operating on user lists.
- **`response_metadata.warnings`**: Slack sometimes returns deprecation warnings in this array. Surface any entries proactively.
- **`error: channel_not_found` on a known channel**: May indicate the bot was removed from the channel or the channel was converted to private. Suggest checking membership.
- **Pagination with no progress**: If `next_cursor` returns the same value across calls, flag a potential infinite loop.
- **`error: restricted_action`**: Workspace settings prevent the action. Surface to the user that an admin policy is blocking the request.

## Playbook

### 1. Post a threaded reply with a file attachment

1. Upload the file: `POST /files.upload` with `channels` set to the target channel and `thread_ts` set to the parent message timestamp.
2. Confirm upload succeeded by checking `ok: true` and extracting `file.id` from the response.
3. Optionally post a text reply in the same thread: `POST /chat.postMessage` with `channel`, `thread_ts`, and `text`.

### 2. Onboard a new user to specific channels

1. Invite the user to the workspace: `POST /admin.users.invite` with `email`, `team_id`, and `channel_ids` for default channels.
2. After the user accepts, look them up: `GET /users.lookupByEmail` with their email to get their `user.id`.
3. Invite them to additional channels: `POST /conversations.invite` with `channel` and `users` for each extra channel.
4. Optionally send a welcome DM: `POST /conversations.open` with `users` set to the new user's ID, then `POST /chat.postMessage` to the returned `channel.id`.

### 3. Archive a channel and notify members

1. Get channel members: `GET /conversations.members` with `channel`, paginating through all `next_cursor` values.
2. Fetch user details for notification: `GET /users.info` for each member (or batch with `users.list`).
3. Post a notice in the channel: `POST /chat.postMessage` with a message explaining the archive.
4. Archive the channel: `POST /conversations.archive` with the `channel` ID.

### 4. Search messages and export matching files

1. Search for messages: `GET /search.messages` with `query`, iterating through pages using `page` parameter.
2. For each matching message, check if it contains file attachments in the `files[]` array.
3. Get file details: `GET /files.info` with each `file` ID to retrieve download URLs.
4. Generate public download links if needed: `POST /files.sharedPublicURL` with the `file` ID.

### 5. Create and populate a user group

1. Create the group: `POST /usergroups.create` with `name`, `handle`, and optional `description`.
2. Extract the `usergroup.id` from the response.
3. Add members: `POST /usergroups.users.update` with the `usergroup` ID and a comma-separated `users` list.
4. Optionally assign default channels: `POST /admin.usergroups.addChannels` with `usergroup_id` and `channel_ids`.
5. Verify membership: `GET /usergroups.users.list` with the `usergroup` ID.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
