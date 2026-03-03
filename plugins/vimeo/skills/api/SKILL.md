---
name: vimeo-api
description: "Vimeo API skill. Use when working with Vimeo for root, categories, channels. Covers 328 endpoints."
version: 1.0.0
generator: lapsh
---

# Vimeo API
API version: 3.4

## Auth
Bearer bearer | OAuth2

## Base URL
https://api.vimeo.com

## Setup
1. Set Authorization header with your Bearer token
2. GET / -- verify access
3. POST /channels -- create first channels

## Endpoints

328 endpoints across 15 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| GET | / | Get an API specification |

### categories
| Method | Path | Description |
|--------|------|-------------|
| GET | /categories | Get all categories |
| GET | /categories/{category} | Get a specific category |
| GET | /categories/{category}/channels | Get all the channels in a category |
| GET | /categories/{category}/groups | Get all the groups in a category |
| GET | /categories/{category}/videos | Get all the videos in a category |
| GET | /categories/{category}/videos/{video_id} | Check for a video in a category |

### channels
| Method | Path | Description |
|--------|------|-------------|
| GET | /channels | Get all channels |
| POST | /channels | Create a channel |
| DELETE | /channels/{channel_id} | Delete a channel |
| GET | /channels/{channel_id} | Get a specific channel |
| PATCH | /channels/{channel_id} | Edit a channel |
| GET | /channels/{channel_id}/categories | Get all the categories in a channel |
| PUT | /channels/{channel_id}/categories | Add a list of categories to a channel |
| DELETE | /channels/{channel_id}/categories/{category} | Remove a category from a channel |
| PUT | /channels/{channel_id}/categories/{category} | Categorize a channel |
| DELETE | /channels/{channel_id}/moderators | Remove a list of channel moderators |
| GET | /channels/{channel_id}/moderators | Get all the moderators in a channel |
| PATCH | /channels/{channel_id}/moderators | Replace the moderators of a channel |
| PUT | /channels/{channel_id}/moderators | Add a list of channel moderators |
| GET | /channels/{channel_id}/moderators/{user_id} | Get a specific channel moderator |
| DELETE | /channels/{channel_id}/moderators/{user_id} | Remove a specific channel moderator |
| PUT | /channels/{channel_id}/moderators/{user_id} | Add a specific channel moderator |
| GET | /channels/{channel_id}/privacy/users | Get all the users who can view a private channel |
| PUT | /channels/{channel_id}/privacy/users | Permit a list of users to view a private channel |
| DELETE | /channels/{channel_id}/privacy/users/{user_id} | Restrict a user from viewing a private channel |
| PUT | /channels/{channel_id}/privacy/users/{user_id} | Permit a specific user to view a private channel |
| GET | /channels/{channel_id}/tags | Get all the tags that have been added to a channel |
| PUT | /channels/{channel_id}/tags | Add a list of tags to a channel |
| DELETE | /channels/{channel_id}/tags/{word} | Remove a tag from a channel |
| GET | /channels/{channel_id}/tags/{word} | Check if a tag has been added to a channel |
| PUT | /channels/{channel_id}/tags/{word} | Add a specific tag to a channel |
| GET | /channels/{channel_id}/users | Get all the followers of a channel |
| DELETE | /channels/{channel_id}/videos | Remove a list of videos from a channel |
| GET | /channels/{channel_id}/videos | Get all the videos in a channel |
| PUT | /channels/{channel_id}/videos | Add a list of videos to a channel |
| DELETE | /channels/{channel_id}/videos/{video_id} | Remove a specific video from a channel |
| GET | /channels/{channel_id}/videos/{video_id} | Get a specific video in a channel |
| PUT | /channels/{channel_id}/videos/{video_id} | Add a specific video to a channel |
| GET | /channels/{channel_id}/videos/{video_id}/comments | Get all the comments on a video |
| POST | /channels/{channel_id}/videos/{video_id}/comments | Add a comment to a video |
| GET | /channels/{channel_id}/videos/{video_id}/credits | Get all the credited users in a video |
| POST | /channels/{channel_id}/videos/{video_id}/credits | Credit a user in a video |
| GET | /channels/{channel_id}/videos/{video_id}/likes | Get all the users who have liked a video |
| GET | /channels/{channel_id}/videos/{video_id}/pictures | Get all the thumbnails of a video |
| POST | /channels/{channel_id}/videos/{video_id}/pictures | Add a video thumbnail |
| GET | /channels/{channel_id}/videos/{video_id}/privacy/users | Get all the users who can view a private video |
| PUT | /channels/{channel_id}/videos/{video_id}/privacy/users | Permit a list of users to view a private video |
| GET | /channels/{channel_id}/videos/{video_id}/texttracks | Get all the text tracks of a video |
| POST | /channels/{channel_id}/videos/{video_id}/texttracks | Add a text track to a video |

### contentratings
| Method | Path | Description |
|--------|------|-------------|
| GET | /contentratings | Get all content ratings |

### creativecommons
| Method | Path | Description |
|--------|------|-------------|
| GET | /creativecommons | Get all Creative Commons licenses |

### groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /groups | Get all groups |
| POST | /groups | Create a group |
| DELETE | /groups/{group_id} | Delete a group |
| GET | /groups/{group_id} | Get a specific group |
| GET | /groups/{group_id}/users | Get all the members of a group |
| GET | /groups/{group_id}/videos | Get all the videos in a group |
| DELETE | /groups/{group_id}/videos/{video_id} | Remove a video from a group |
| GET | /groups/{group_id}/videos/{video_id} | Get a specific video in a group |
| PUT | /groups/{group_id}/videos/{video_id} | Add a video to a group |

### languages
| Method | Path | Description |
|--------|------|-------------|
| GET | /languages | Get all languages |

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /me | Get a user |
| PATCH | /me | Edit a user |
| GET | /me/albums | Get all the albums that belong to a user |
| POST | /me/albums | Create an album |
| DELETE | /me/albums/{album_id} | Delete an album |
| GET | /me/albums/{album_id} | Get a specific album |
| PATCH | /me/albums/{album_id} | Edit an album |
| GET | /me/albums/{album_id}/videos | Get all the videos in an album |
| PUT | /me/albums/{album_id}/videos | Replace all the videos in an album |
| DELETE | /me/albums/{album_id}/videos/{video_id} | Remove a video from an album |
| GET | /me/albums/{album_id}/videos/{video_id} | Get a specific video in an album |
| PUT | /me/albums/{album_id}/videos/{video_id} | Add a specific video to an album |
| POST | /me/albums/{album_id}/videos/{video_id}/set_album_thumbnail | Set a video as the album thumbnail |
| GET | /me/appearances | Get all the videos in which a user appears |
| GET | /me/categories | Get all the categories that a user follows |
| DELETE | /me/categories/{category} | Unsubscribe a user from a category |
| GET | /me/categories/{category} | Check if a user follows a category |
| PUT | /me/categories/{category} | Subscribe a user to a single category |
| GET | /me/channels | Get all the channels to which a user subscribes |
| DELETE | /me/channels/{channel_id} | Unsubscribe a user from a specific channel |
| GET | /me/channels/{channel_id} | Check if a user follows a channel |
| PUT | /me/channels/{channel_id} | Subscribe a user to a specific channel |
| GET | /me/customlogos | Get all the custom logos that belong to a user |
| POST | /me/customlogos | Add a custom logo |
| GET | /me/customlogos/{logo_id} | Get a specific custom logo |
| GET | /me/feed | Get all the videos in a user's feed |
| GET | /me/followers | Get all the followers of a user |
| GET | /me/following | Get all the users that a user is following |
| POST | /me/following | Follow a list of users |
| DELETE | /me/following/{follow_user_id} | Unfollow a user |
| GET | /me/following/{follow_user_id} | Check if a user is following another user |
| PUT | /me/following/{follow_user_id} | Follow a specific user |
| GET | /me/groups | Get all the groups that a user has joined |
| DELETE | /me/groups/{group_id} | Remove a user from a group |
| PUT | /me/groups/{group_id} | Add a user to a group |
| GET | /me/groups/{group_id} | Check if a user has joined a group |
| GET | /me/likes | Get all the videos that a user has liked |
| DELETE | /me/likes/{video_id} | Cause a user to unlike a video |
| GET | /me/likes/{video_id} | Check if a user has liked a video |
| PUT | /me/likes/{video_id} | Cause a user to like a video |
| GET | /me/ondemand/pages | Get all the On Demand pages of a user |
| POST | /me/ondemand/pages | Create an On Demand page |
| GET | /me/ondemand/purchases | Get all the On Demand purchases and rentals that a user has made |
| GET | /me/ondemand/purchases/{ondemand_id} | Check if a user has made a purchase or rental from an On Demand page |
| GET | /me/pictures | Get all the pictures that belong to a user |
| POST | /me/pictures | Add a user picture |
| DELETE | /me/pictures/{portraitset_id} | Delete a user picture |
| GET | /me/pictures/{portraitset_id} | Get a specific user picture |
| PATCH | /me/pictures/{portraitset_id} | Edit a user picture |
| GET | /me/portfolios | Get all the portfolios that belong to a user |
| GET | /me/portfolios/{portfolio_id} | Get a specific portfolio |
| GET | /me/portfolios/{portfolio_id}/videos | Get all the videos in a portfolio |
| DELETE | /me/portfolios/{portfolio_id}/videos/{video_id} | Remove a video from a portfolio |
| GET | /me/portfolios/{portfolio_id}/videos/{video_id} | Get a specific video in a portfolio |
| PUT | /me/portfolios/{portfolio_id}/videos/{video_id} | Add a video to a portfolio |
| GET | /me/presets | Get all the embed presets that a user has created |
| GET | /me/presets/{preset_id} | Get a specific embed preset |
| PATCH | /me/presets/{preset_id} | Edit an embed preset |
| GET | /me/presets/{preset_id}/videos | Get all the videos that have been added to an embed preset |
| GET | /me/projects | Get all the projects that belong to a user |
| POST | /me/projects | Create a project |
| DELETE | /me/projects/{project_id} | Delete a project |
| GET | /me/projects/{project_id} | Get a specific project |
| PATCH | /me/projects/{project_id} | Edit a project |
| DELETE | /me/projects/{project_id}/videos | Remove a list of videos from a project |
| GET | /me/projects/{project_id}/videos | Get all the videos in a project |
| PUT | /me/projects/{project_id}/videos | Add a list of videos to a project |
| DELETE | /me/projects/{project_id}/videos/{video_id} | Remove a specific video from a project |
| PUT | /me/projects/{project_id}/videos/{video_id} | Add a specific video to a project |
| GET | /me/videos | Get all the videos that a user has uploaded |
| POST | /me/videos | Upload a video |
| GET | /me/videos/{video_id} | Check if a user owns a video |
| DELETE | /me/watched/videos | Delete a user's watch history |
| GET | /me/watched/videos | Get all the videos that a user has watched |
| DELETE | /me/watched/videos/{video_id} | Delete a specific video from a user's watch history |
| GET | /me/watchlater | Get all the videos in a user's Watch Later queue |
| DELETE | /me/watchlater/{video_id} | Remove a video from a user's Watch Later queue |
| GET | /me/watchlater/{video_id} | Check if a user has added a specific video to their Watch Later queue |
| PUT | /me/watchlater/{video_id} | Add a video to a user's Watch Later queue |

### oauth
| Method | Path | Description |
|--------|------|-------------|
| POST | /oauth/access_token | Exchange an authorization code for an access token |
| POST | /oauth/authorize/client | Authorize a client with OAuth |
| POST | /oauth/authorize/vimeo_oauth1 | Convert OAuth 1 access tokens to OAuth 2 access tokens |
| GET | /oauth/verify | Verify an OAuth 2 token |

### ondemand
| Method | Path | Description |
|--------|------|-------------|
| GET | /ondemand/genres | Get all On Demand genres |
| GET | /ondemand/genres/{genre_id} | Get a specific On Demand genre |
| GET | /ondemand/genres/{genre_id}/pages | Get all the On Demand pages in a genre |
| GET | /ondemand/genres/{genre_id}/pages/{ondemand_id} | Get a specific On Demand page in a genre |
| DELETE | /ondemand/pages/{ondemand_id} | Delete a draft of an On Demand page |
| GET | /ondemand/pages/{ondemand_id} | Get a specific On Demand page |
| PATCH | /ondemand/pages/{ondemand_id} | Edit an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/backgrounds | Get all the backgrounds of an On Demand page |
| POST | /ondemand/pages/{ondemand_id}/backgrounds | Add a background to an On Demand page |
| DELETE | /ondemand/pages/{ondemand_id}/backgrounds/{background_id} | Remove a background from an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/backgrounds/{background_id} | Get a specific background of an On Demand page |
| PATCH | /ondemand/pages/{ondemand_id}/backgrounds/{background_id} | Edit a background of an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/genres | Get all the genres of an On Demand page |
| DELETE | /ondemand/pages/{ondemand_id}/genres/{genre_id} | Remove a genre from an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/genres/{genre_id} | Check whether an On Demand page belongs to a genre |
| PUT | /ondemand/pages/{ondemand_id}/genres/{genre_id} | Add a genre to an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/likes | Get all the users who have liked a video on an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/pictures | Get all the posters of an On Demand page |
| POST | /ondemand/pages/{ondemand_id}/pictures | Add a poster to an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/pictures/{poster_id} | Get a specific poster of an On Demand page |
| PATCH | /ondemand/pages/{ondemand_id}/pictures/{poster_id} | Edit a poster of an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/promotions | Get all the promotions on an On Demand page |
| POST | /ondemand/pages/{ondemand_id}/promotions | Add a promotion to an On Demand page |
| DELETE | /ondemand/pages/{ondemand_id}/promotions/{promotion_id} | Remove a promotion from an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/promotions/{promotion_id} | Get a specific promotion on an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/promotions/{promotion_id}/codes | Get all the codes of a promotion on an On Demand page |
| DELETE | /ondemand/pages/{ondemand_id}/regions | Remove a list of regions from an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/regions | Get all the regions of an On Demand page |
| PUT | /ondemand/pages/{ondemand_id}/regions | Add a list of regions to an On Demand page |
| DELETE | /ondemand/pages/{ondemand_id}/regions/{country} | Remove a specific region from an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/regions/{country} | Get a specific region of an On Demand page |
| PUT | /ondemand/pages/{ondemand_id}/regions/{country} | Add a specific region to an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/seasons | Get all the seasons on an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/seasons/{season_id} | Get a specific season on an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/seasons/{season_id}/videos | Get all the videos in a season on an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/videos | Get all the videos on an On Demand page |
| DELETE | /ondemand/pages/{ondemand_id}/videos/{video_id} | Remove a video from an On Demand page |
| GET | /ondemand/pages/{ondemand_id}/videos/{video_id} | Get a specific video on an On Demand page |
| PUT | /ondemand/pages/{ondemand_id}/videos/{video_id} | Add a video to an On Demand page |
| GET | /ondemand/regions | Get all the On Demand regions |
| GET | /ondemand/regions/{country} | Get a specific On Demand region |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{word} | Get a specific tag |
| GET | /tags/{word}/videos | Get all the videos with a specific tag |

### tokens
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /tokens | Revoke the current access token |

### tutorial
| Method | Path | Description |
|--------|------|-------------|
| GET | /tutorial | Get started with the Vimeo API |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | Search for users |
| GET | /users/{user_id} | Get a user |
| PATCH | /users/{user_id} | Edit a user |
| GET | /users/{user_id}/albums | Get all the albums that belong to a user |
| POST | /users/{user_id}/albums | Create an album |
| DELETE | /users/{user_id}/albums/{album_id} | Delete an album |
| GET | /users/{user_id}/albums/{album_id} | Get a specific album |
| PATCH | /users/{user_id}/albums/{album_id} | Edit an album |
| GET | /users/{user_id}/albums/{album_id}/custom_thumbnails | Get all the custom upload thumbnails of an album |
| POST | /users/{user_id}/albums/{album_id}/custom_thumbnails | Add a custom uploaded thumbnail |
| DELETE | /users/{user_id}/albums/{album_id}/custom_thumbnails/{thumbnail_id} | Remove a custom uploaded album thumbnail |
| GET | /users/{user_id}/albums/{album_id}/custom_thumbnails/{thumbnail_id} | Get a specific custom uploaded album thumbnail |
| PATCH | /users/{user_id}/albums/{album_id}/custom_thumbnails/{thumbnail_id} | Replace a custom uploaded album thumbnail |
| GET | /users/{user_id}/albums/{album_id}/logos | Get all the custom logos of an album |
| POST | /users/{user_id}/albums/{album_id}/logos | Add a custom album logo |
| DELETE | /users/{user_id}/albums/{album_id}/logos/{logo_id} | Remove a custom album logo |
| GET | /users/{user_id}/albums/{album_id}/logos/{logo_id} | Get a specific custom album logo |
| PATCH | /users/{user_id}/albums/{album_id}/logos/{logo_id} | Replace a custom album logo |
| GET | /users/{user_id}/albums/{album_id}/videos | Get all the videos in an album |
| PUT | /users/{user_id}/albums/{album_id}/videos | Replace all the videos in an album |
| DELETE | /users/{user_id}/albums/{album_id}/videos/{video_id} | Remove a video from an album |
| GET | /users/{user_id}/albums/{album_id}/videos/{video_id} | Get a specific video in an album |
| PUT | /users/{user_id}/albums/{album_id}/videos/{video_id} | Add a specific video to an album |
| POST | /users/{user_id}/albums/{album_id}/videos/{video_id}/set_album_thumbnail | Set a video as the album thumbnail |
| GET | /users/{user_id}/appearances | Get all the videos in which a user appears |
| GET | /users/{user_id}/categories | Get all the categories that a user follows |
| DELETE | /users/{user_id}/categories/{category} | Unsubscribe a user from a category |
| GET | /users/{user_id}/categories/{category} | Check if a user follows a category |
| PUT | /users/{user_id}/categories/{category} | Subscribe a user to a single category |
| GET | /users/{user_id}/channels | Get all the channels to which a user subscribes |
| DELETE | /users/{user_id}/channels/{channel_id} | Unsubscribe a user from a specific channel |
| GET | /users/{user_id}/channels/{channel_id} | Check if a user follows a channel |
| PUT | /users/{user_id}/channels/{channel_id} | Subscribe a user to a specific channel |
| GET | /users/{user_id}/customlogos | Get all the custom logos that belong to a user |
| POST | /users/{user_id}/customlogos | Add a custom logo |
| GET | /users/{user_id}/customlogos/{logo_id} | Get a specific custom logo |
| GET | /users/{user_id}/feed | Get all the videos in a user's feed |
| GET | /users/{user_id}/followers | Get all the followers of a user |
| GET | /users/{user_id}/following | Get all the users that a user is following |
| POST | /users/{user_id}/following | Follow a list of users |
| DELETE | /users/{user_id}/following/{follow_user_id} | Unfollow a user |
| GET | /users/{user_id}/following/{follow_user_id} | Check if a user is following another user |
| PUT | /users/{user_id}/following/{follow_user_id} | Follow a specific user |
| GET | /users/{user_id}/groups | Get all the groups that a user has joined |
| DELETE | /users/{user_id}/groups/{group_id} | Remove a user from a group |
| PUT | /users/{user_id}/groups/{group_id} | Add a user to a group |
| GET | /users/{user_id}/groups/{group_id} | Check if a user has joined a group |
| GET | /users/{user_id}/likes | Get all the videos that a user has liked |
| DELETE | /users/{user_id}/likes/{video_id} | Cause a user to unlike a video |
| GET | /users/{user_id}/likes/{video_id} | Check if a user has liked a video |
| PUT | /users/{user_id}/likes/{video_id} | Cause a user to like a video |
| GET | /users/{user_id}/ondemand/pages | Get all the On Demand pages of a user |
| POST | /users/{user_id}/ondemand/pages | Create an On Demand page |
| GET | /users/{user_id}/ondemand/purchases | Check if a user has made a purchase or rental from an On Demand page |
| GET | /users/{user_id}/pictures | Get all the pictures that belong to a user |
| POST | /users/{user_id}/pictures | Add a user picture |
| DELETE | /users/{user_id}/pictures/{portraitset_id} | Delete a user picture |
| GET | /users/{user_id}/pictures/{portraitset_id} | Get a specific user picture |
| PATCH | /users/{user_id}/pictures/{portraitset_id} | Edit a user picture |
| GET | /users/{user_id}/portfolios | Get all the portfolios that belong to a user |
| GET | /users/{user_id}/portfolios/{portfolio_id} | Get a specific portfolio |
| GET | /users/{user_id}/portfolios/{portfolio_id}/videos | Get all the videos in a portfolio |
| DELETE | /users/{user_id}/portfolios/{portfolio_id}/videos/{video_id} | Remove a video from a portfolio |
| GET | /users/{user_id}/portfolios/{portfolio_id}/videos/{video_id} | Get a specific video in a portfolio |
| PUT | /users/{user_id}/portfolios/{portfolio_id}/videos/{video_id} | Add a video to a portfolio |
| GET | /users/{user_id}/presets | Get all the embed presets that a user has created |
| GET | /users/{user_id}/presets/{preset_id} | Get a specific embed preset |
| PATCH | /users/{user_id}/presets/{preset_id} | Edit an embed preset |
| GET | /users/{user_id}/presets/{preset_id}/videos | Get all the videos that have been added to an embed preset |
| GET | /users/{user_id}/projects | Get all the projects that belong to a user |
| POST | /users/{user_id}/projects | Create a project |
| DELETE | /users/{user_id}/projects/{project_id} | Delete a project |
| GET | /users/{user_id}/projects/{project_id} | Get a specific project |
| PATCH | /users/{user_id}/projects/{project_id} | Edit a project |
| DELETE | /users/{user_id}/projects/{project_id}/videos | Remove a list of videos from a project |
| GET | /users/{user_id}/projects/{project_id}/videos | Get all the videos in a project |
| PUT | /users/{user_id}/projects/{project_id}/videos | Add a list of videos to a project |
| DELETE | /users/{user_id}/projects/{project_id}/videos/{video_id} | Remove a specific video from a project |
| PUT | /users/{user_id}/projects/{project_id}/videos/{video_id} | Add a specific video to a project |
| DELETE | /users/{user_id}/uploads/{upload_id} | Complete a user's streaming upload |
| GET | /users/{user_id}/uploads/{upload_id} | Get a user's upload attempt |
| GET | /users/{user_id}/videos | Get all the videos that a user has uploaded |
| POST | /users/{user_id}/videos | Upload a video |
| GET | /users/{user_id}/videos/{video_id} | Check if a user owns a video |
| GET | /users/{user_id}/watchlater | Get all the videos in a user's Watch Later queue |
| DELETE | /users/{user_id}/watchlater/{video_id} | Remove a video from a user's Watch Later queue |
| GET | /users/{user_id}/watchlater/{video_id} | Check if a user has added a specific video to their Watch Later queue |
| PUT | /users/{user_id}/watchlater/{video_id} | Add a video to a user's Watch Later queue |

### videos
| Method | Path | Description |
|--------|------|-------------|
| GET | /videos | Search for videos |
| DELETE | /videos/{video_id} | Delete a video |
| GET | /videos/{video_id} | Get a specific video |
| PATCH | /videos/{video_id} | Edit a video |
| GET | /videos/{video_id}/available_albums | Get all the albums to which a user can add or remove a specific video |
| GET | /videos/{video_id}/available_channels | Get all the channels to which a user can add or remove a specific video |
| GET | /videos/{video_id}/categories | Get all the categories to which a video belongs |
| PUT | /videos/{video_id}/categories | Suggest categories for a video |
| GET | /videos/{video_id}/comments | Get all the comments on a video |
| POST | /videos/{video_id}/comments | Add a comment to a video |
| DELETE | /videos/{video_id}/comments/{comment_id} | Delete a video comment |
| GET | /videos/{video_id}/comments/{comment_id} | Get a specific video comment |
| PATCH | /videos/{video_id}/comments/{comment_id} | Edit a video comment |
| GET | /videos/{video_id}/comments/{comment_id}/replies | Get all the replies to a video comment |
| POST | /videos/{video_id}/comments/{comment_id}/replies | Add a reply to a video comment |
| GET | /videos/{video_id}/credits | Get all the credited users in a video |
| POST | /videos/{video_id}/credits | Credit a user in a video |
| DELETE | /videos/{video_id}/credits/{credit_id} | Delete the credit for a user in a video |
| GET | /videos/{video_id}/credits/{credit_id} | Get a specific credited user in a video |
| PATCH | /videos/{video_id}/credits/{credit_id} | Edit the credit for a user in a video |
| GET | /videos/{video_id}/likes | Get all the users who have liked a video |
| GET | /videos/{video_id}/pictures | Get all the thumbnails of a video |
| POST | /videos/{video_id}/pictures | Add a video thumbnail |
| DELETE | /videos/{video_id}/pictures/{picture_id} | Delete a video thumbnail |
| GET | /videos/{video_id}/pictures/{picture_id} | Get a specific video thumbnail |
| PATCH | /videos/{video_id}/pictures/{picture_id} | Edit a video thumbnail |
| DELETE | /videos/{video_id}/presets/{preset_id} | Remove an embed preset from a video |
| GET | /videos/{video_id}/presets/{preset_id} | Check if an embed preset has been added to a video |
| PUT | /videos/{video_id}/presets/{preset_id} | Add an embed preset to a video |
| GET | /videos/{video_id}/privacy/domains | Get all the domains on a video's whitelist |
| DELETE | /videos/{video_id}/privacy/domains/{domain} | Remove a domain from a video's whitelist |
| PUT | /videos/{video_id}/privacy/domains/{domain} | Add a domain to a video's whitelist |
| GET | /videos/{video_id}/privacy/users | Get all the users who can view a private video |
| PUT | /videos/{video_id}/privacy/users | Permit a list of users to view a private video |
| DELETE | /videos/{video_id}/privacy/users/{user_id} | Restrict a user from viewing a private video |
| PUT | /videos/{video_id}/privacy/users/{user_id} | Permit a specific user to view a private video |
| GET | /videos/{video_id}/tags | Get all the tags of a video |
| PUT | /videos/{video_id}/tags | Add a list of tags to a video |
| DELETE | /videos/{video_id}/tags/{word} | Remove a tag from a video |
| GET | /videos/{video_id}/tags/{word} | Check if a tag has been added to a video |
| PUT | /videos/{video_id}/tags/{word} | Add a specific tag to a video |
| GET | /videos/{video_id}/texttracks | Get all the text tracks of a video |
| POST | /videos/{video_id}/texttracks | Add a text track to a video |
| DELETE | /videos/{video_id}/texttracks/{texttrack_id} | Delete a text track |
| GET | /videos/{video_id}/texttracks/{texttrack_id} | Get a specific text track |
| PATCH | /videos/{video_id}/texttracks/{texttrack_id} | Edit a text track |
| POST | /videos/{video_id}/timelinethumbnails | Add a new timeline event thumbnail to a video |
| GET | /videos/{video_id}/timelinethumbnails/{thumbnail_id} | Get a timeline event thumbnail |
| POST | /videos/{video_id}/versions | Add a version to a video |
| GET | /videos/{video_id}/videos | Get all the related videos of a video |

## Enhanced Skill Content
## Question Mapping

- "How do I search for videos on Vimeo?" -> GET /videos
- "What categories are available?" -> GET /categories
- "How do I get my profile information?" -> GET /me
- "How do I upload a video?" -> POST /me/videos
- "How do I add a video to an album?" -> PUT /me/albums/{album_id}/videos/{video_id}
- "How do I like a video?" -> PUT /me/likes/{video_id}
- "How do I create a new channel?" -> POST /channels
- "How do I add a video to my watch later list?" -> PUT /me/watchlater/{video_id}
- "How do I get comments on a video?" -> GET /videos/{video_id}/comments
- "How do I create an On Demand page for selling my film?" -> POST /me/ondemand/pages
- "How do I manage who can see my private video?" -> PUT /videos/{video_id}/privacy/users
- "How do I find users on Vimeo?" -> GET /users
- "How do I set a custom thumbnail on my album?" -> POST /me/albums/{album_id}/videos/{video_id}/set_album_thumbnail
- "How do I restrict my video to specific domains?" -> PUT /videos/{video_id}/privacy/domains/{domain}
- "How do I verify my OAuth token is valid?" -> GET /oauth/verify

## Response Tips

- **Paginated lists** (videos, channels, users, albums, categories): All accept `page` and `per_page` params; responses include `total`, `page`, and `per_page` in a paging object -- always check `total` to know if more pages exist.
- **Video objects**: Deeply nested under `metadata.connections` (related counts/URIs) and `metadata.interactions` (buy/rent/like/watchlater states) -- drill into `interactions` for actionable state like `like.added` or `watchlater.added`.
- **On Demand pages**: Contain nested `buy`, `rent`, and `subscription` pricing maps keyed by currency code (USD, EUR, etc.) -- treat missing keys as "not available in that currency."
- **204 responses**: Indicate success with no body (likes, follows, watch later, channel membership, video removal) -- do not attempt to parse a response body.
- **Error responses**: Return a JSON object with `error` (human message), `link` (docs URL), and `developer_message` (debug detail) -- surface `developer_message` for troubleshooting.

## Anomaly Flags

- **429 status on POST /me/following**: Rate limit hit when bulk-following users -- back off and retry with smaller batches.
- **304 Not Modified**: Returned by video/channel listing endpoints when content has not changed -- surface this so callers know to use cached data rather than re-processing.
- **500 on upload/thumbnail operations**: Server errors on `POST /me/videos`, `DELETE /users/{user_id}/uploads/{upload_id}`, and `set_album_thumbnail` indicate transient failures -- flag for retry rather than treating as permanent.
- **503 on search/user listing**: Vimeo search infrastructure may be temporarily unavailable -- alert the user and suggest retrying after a short delay.
- **403 on write operations**: Likely a plan/permission limitation (e.g., custom logos, On Demand pages, group creation require Vimeo Pro/Business) -- surface the plan requirement rather than just "forbidden."
- **Deprecated OAuth1 flow**: `POST /oauth/authorize/vimeo_oauth1` exists but OAuth1 is legacy -- flag if an agent attempts to use it and recommend OAuth2 instead.
- **On Demand pricing without `accepted_currencies`**: If a user creates an On Demand page with pricing but omits `accepted_currencies`, unexpected currency behavior may occur -- proactively warn.

## Playbook

### 1. Upload a Video and Organize It

1. `POST /me/videos` -- initiate the upload; note the `upload.upload_link` and `upload.approach` (tus or pull) from the response.
2. Upload the file binary to the `upload_link` using the indicated approach (outside the API).
3. `PATCH /videos/{video_id}` -- set the title, description, and privacy settings.
4. `PUT /videos/{video_id}/tags` -- add relevant tags for discoverability.
5. `PUT /me/albums/{album_id}/videos/{video_id}` -- add the video to an album.
6. `PUT /me/projects/{project_id}/videos/{video_id}` -- add the video to a project folder.

### 2. Create and Populate a Channel

1. `POST /channels` -- create the channel with name, description, and privacy settings.
2. `PUT /channels/{channel_id}/videos/{video_id}` -- add videos one at a time, or use `PUT /channels/{channel_id}/videos` with `video_uri` for batch.
3. `PUT /channels/{channel_id}/moderators/{user_id}` -- assign moderators.
4. `PUT /channels/{channel_id}/categories/{category}` -- associate with relevant categories.
5. `GET /channels/{channel_id}/videos` -- verify the channel content is correct.

### 3. Set Up an On Demand Film for Sale

1. `POST /me/ondemand/pages` -- create the page with `type: "film"`, `content_rating`, `name`, `description`, and pricing under `buy`/`rent`.
2. `PUT /ondemand/pages/{ondemand_id}/videos/{video_id}` -- attach the film video (set `type` to `main`).
3. `PUT /ondemand/pages/{ondemand_id}/videos/{trailer_id}` -- attach a trailer (set `type` to `trailer`).
4. `PUT /ondemand/pages/{ondemand_id}/genres/{genre_id}` -- assign genres.
5. `PUT /ondemand/pages/{ondemand_id}/regions/{country}` -- configure regional availability.
6. `POST /ondemand/pages/{ondemand_id}/promotions` -- create discount promo codes.
7. `PATCH /ondemand/pages/{ondemand_id}` -- publish when ready.

### 4. Manage Video Privacy and Embedding

1. `PATCH /videos/{video_id}` -- set `privacy.view` to `disable`, `unlisted`, `password`, or `users`.
2. `PUT /videos/{video_id}/privacy/users/{user_id}` -- grant access to specific users (when `privacy.view` is `users`).
3. `PUT /videos/{video_id}/privacy/domains/{domain}` -- whitelist embedding domains.
4. `GET /videos/{video_id}/privacy/domains` -- verify the domain whitelist.
5. `GET /videos/{video_id}/privacy/users` -- verify the user access list.

### 5. Curate and Manage an Album (Showcase)

1. `POST /me/albums` -- create the album with name, description, layout, and theme.
2. `PUT /me/albums/{album_id}/videos` -- batch-add videos by passing comma-separated `videos` URIs.
3. `POST /me/albums/{album_id}/videos/{video_id}/set_album_thumbnail` -- set the album thumbnail from a specific video frame using `time_code`.
4. `GET /me/albums/{album_id}/videos?sort=manual` -- verify video order.
5. `PATCH /me/albums/{album_id}` -- update privacy, password, or branding settings.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
