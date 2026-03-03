---
name: clubhouse-api
description: "Clubhouse API skill. Use when working with Clubhouse for start_phone_number_auth, call_phone_number_auth, resend_phone_number_auth. Covers 41 endpoints."
version: 1.0.0
generator: lapsh
---

# Clubhouse API
API version: 1

## Auth
No authentication required.

## Base URL
https://www.clubhouseapi.com/api/

## Setup
1. No auth setup needed
2. GET /get_all_topics -- verify access
3. POST /start_phone_number_auth -- create first start_phone_number_auth

## Endpoints

41 endpoints across 41 groups. See references/api-spec.lap for full details.

### start_phone_number_auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /start_phone_number_auth | Starts phone number auth. |

### call_phone_number_auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /call_phone_number_auth | Call phone number auth. |

### resend_phone_number_auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /resend_phone_number_auth | Resend phone number auth. |

### complete_phone_number_auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /complete_phone_number_auth | Call phone number auth. |

### check_waitlist_status
| Method | Path | Description |
|--------|------|-------------|
| POST | /check_waitlist_status | checks waitlist status. |

### me
| Method | Path | Description |
|--------|------|-------------|
| POST | /me | gets user |

### get_release_notes
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_release_notes | gets release notes. |

### get_all_topics
| Method | Path | Description |
|--------|------|-------------|
| GET | /get_all_topics | gets all topics. |

### get_topic
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_topic | looks up topic by ID. |

### get_clubs_for_topic
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_clubs_for_topic | looks up clubs by topic. |

### get_profile
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_profile | looks up user profile by ID. |

### get_users_for_topic
| Method | Path | Description |
|--------|------|-------------|
| GET | /get_users_for_topic | looks up users by topic. |

### get_channels
| Method | Path | Description |
|--------|------|-------------|
| GET | /get_channels | get all channels |

### join_channel
| Method | Path | Description |
|--------|------|-------------|
| POST | /join_channel | join a channel. |

### leave_channel
| Method | Path | Description |
|--------|------|-------------|
| POST | /leave_channel | leave a channel. |

### update_username
| Method | Path | Description |
|--------|------|-------------|
| POST | /update_username | edits username. |

### follow
| Method | Path | Description |
|--------|------|-------------|
| POST | /follow | follows a user |

### refresh_token
| Method | Path | Description |
|--------|------|-------------|
| POST | /refresh_token | gets an access_token from a refresh_token. |

### get_suggested_invites
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_suggested_invites | find users to invite based on phone number. |

### get_suggested_club_invites
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_suggested_club_invites | find users to invite to clubs based on phone number |

### get_club
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_club | gets club by id |

### check_for_update
| Method | Path | Description |
|--------|------|-------------|
| GET | /check_for_update | Clubhouse uses this to check for updates when app is not installed from App Store (eg TestFlight) |

### invite_to_app
| Method | Path | Description |
|--------|------|-------------|
| POST | /invite_to_app | invite a user to the app, using one of your invites |

### invite_from_waitlist
| Method | Path | Description |
|--------|------|-------------|
| POST | /invite_from_waitlist | wave to another user on the waitlist to give them access |

### get_following
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_following | get a list of the users and clubs that this user is following. Returned users have bios truncated to ~80 characters. |

### get_suggested_follows_friends_only
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_suggested_follows_friends_only | find people to follow by uploading contacts during signup |

### get_suggested_follows_all
| Method | Path | Description |
|--------|------|-------------|
| GET | /get_suggested_follows_all | gets suggested follows during signup |

### update_notifications
| Method | Path | Description |
|--------|------|-------------|
| POST | /update_notifications | updates notification during signup. |

### get_online_friends
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_online_friends | gets online friends on the app homepage. |

### get_events
| Method | Path | Description |
|--------|------|-------------|
| GET | /get_events | the Upcoming for You page |

### get_settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /get_settings | get notification settings |

### get_welcome_channel
| Method | Path | Description |
|--------|------|-------------|
| GET | /get_welcome_channel | called during signup |

### record_action_trails
| Method | Path | Description |
|--------|------|-------------|
| POST | /record_action_trails | analytics |

### get_notifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /get_notifications | get notifications (the bell icon) |

### get_actionable_notifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /get_actionable_notifications | get actionable notifications (the bell again) |

### get_create_channel_targets
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_create_channel_targets | is fetched when you tap Create Room |

### create_channel
| Method | Path | Description |
|--------|------|-------------|
| POST | /create_channel | creates a channel |

### get_suggested_speakers
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_suggested_speakers | gets suggested users when you start a private room |

### search_users
| Method | Path | Description |
|--------|------|-------------|
| POST | /search_users | search for users |

### get_suggested_follows_similar
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_suggested_follows_similar | find similar users. (The Sparkles button on Clubhouse's profile page) |

### search_clubs
| Method | Path | Description |
|--------|------|-------------|
| POST | /search_clubs | search clubs. |

## Enhanced Skill Content
## Question Mapping

- "How do I log in to Clubhouse?" -> POST /start_phone_number_auth
- "How do I verify my phone number?" -> POST /complete_phone_number_auth
- "I didn't get the auth code, can I get a phone call instead?" -> POST /call_phone_number_auth
- "Can I resend the verification code?" -> POST /resend_phone_number_auth
- "Am I still on the waitlist?" -> POST /check_waitlist_status
- "What's my profile info?" -> POST /me
- "How do I look up another user's profile?" -> POST /get_profile
- "What rooms are live right now?" -> GET /get_channels
- "How do I join a live room?" -> POST /join_channel
- "How do I leave a room I'm in?" -> POST /leave_channel
- "How do I find users by name?" -> POST /search_users
- "How do I find clubs by name?" -> POST /search_clubs
- "How do I follow someone?" -> POST /follow
- "Who am I following?" -> POST /get_following
- "How do I create a new room?" -> POST /create_channel
- "What topics are available to browse?" -> GET /get_all_topics
- "What events are coming up?" -> GET /get_events
- "How do I invite someone to Clubhouse?" -> POST /invite_to_app
- "Which friends are online right now?" -> POST /get_online_friends
- "How do I check my notifications?" -> GET /get_notifications

## Response Tips

- **Auth endpoints** (start/call/resend/complete_phone_number_auth): Expect token and user object on success; chain these sequentially - start first, then complete with the verification code.
- **Profile/user endpoints** (me, get_profile, search_users): User objects are nested; look for `user_profile` containing bio, photo_url, follower counts, and club memberships.
- **Channel endpoints** (get_channels, join_channel, leave_channel, create_channel): Channel objects include `users` arrays with speaker/listener roles; `join_channel` returns the full channel state including current participants.
- **Paginated endpoints** (get_notifications, get_events, get_users_for_topic, get_suggested_follows_all): Pass `page` and `page_size` params; responses include a `count` or `next` cursor - keep fetching until next is null.
- **Topic/club discovery** (get_all_topics, get_topic, get_clubs_for_topic): Topics are hierarchical; clubs nest member counts and descriptions inside each result object.
- **Error responses**: 400 errors typically mean invalid input (bad channel ID, username taken, invalid invite); 401 means expired/missing auth token; 403 on `/me` means the account is banned or suspended.

## Anomaly Flags

- **401 on any endpoint**: Auth token has expired - surface this immediately and suggest calling `POST /refresh_token` before retrying.
- **403 on /me**: Account may be suspended or banned - alert the user rather than silently retrying.
- **400 on /join_channel**: Room may have ended, be full, or the user may be blocked from it - surface the error detail.
- **400 on /update_username**: Username is likely taken or contains invalid characters - show the specific rejection reason.
- **400 on /invite_to_app or /invite_from_waitlist**: Invite quota may be exhausted or the phone number is already registered - flag which constraint was hit.
- **Waitlist status not progressing**: If `check_waitlist_status` keeps returning the same position across multiple checks, surface this to the user.
- **Empty channel list**: If `get_channels` returns zero results during normal hours, it may indicate a network issue or geo-restriction rather than genuinely no live rooms.
- **Token refresh failure (401 on /refresh_token)**: Full re-authentication is required - do not loop on refresh, escalate to the phone auth flow.

## Playbook

### 1. Authenticate and Set Up a Session

1. Call `POST /start_phone_number_auth` with the user's phone number to trigger an SMS code.
2. If the SMS doesn't arrive, call `POST /resend_phone_number_auth` or `POST /call_phone_number_auth` for a voice call.
3. Call `POST /complete_phone_number_auth` with the verification code to receive an auth token.
4. Call `POST /me` to confirm the session is active and retrieve the authenticated user's profile.
5. Store the auth token; when it expires, call `POST /refresh_token` before re-authenticating from scratch.

### 2. Browse and Join a Live Room

1. Call `GET /get_channels` to list all currently active rooms.
2. Optionally call `GET /get_all_topics` and `POST /get_clubs_for_topic` to filter rooms by interest area.
3. Call `POST /join_channel` with the target channel ID to enter the room.
4. Call `POST /get_suggested_speakers` to see who might be invited to speak.
5. When finished, call `POST /leave_channel` to exit cleanly.

### 3. Discover and Follow Users

1. Call `POST /search_users` with a query string to find users by name or handle.
2. Call `POST /get_profile` with the user ID to view their full profile, bio, and club memberships.
3. Call `POST /follow` with the user ID to follow them.
4. Call `POST /get_following` to confirm the follow was recorded and review your full following list.
5. Call `GET /get_suggested_follows_all` (paginated) or `POST /get_suggested_follows_friends_only` for more recommendations.

### 4. Create and Host a Room

1. Call `POST /get_create_channel_targets` to retrieve valid topic and club targets for room creation.
2. Call `POST /create_channel` with the desired topic, title, and optional club association.
3. Call `POST /get_suggested_speakers` to identify users to invite as speakers.
4. Share the channel with contacts using the channel URL from the creation response.
5. When the session is over, call `POST /leave_channel` (the room closes when all speakers leave).

### 5. Manage Invites and Onboarding

1. Call `POST /check_waitlist_status` to see if the user has been approved from the waitlist.
2. Call `POST /get_suggested_invites` to see which contacts are eligible for an invite.
3. Call `POST /invite_to_app` with a phone number to send an invite (watch for 400 if quota is exhausted).
4. For waitlisted users you can approve, call `POST /invite_from_waitlist` with their user ID.
5. Call `POST /get_suggested_club_invites` to recommend clubs to newly onboarded users.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
