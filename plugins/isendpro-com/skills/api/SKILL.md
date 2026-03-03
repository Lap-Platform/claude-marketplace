---
name: api-isendpro
description: "API iSendPro API skill. Use when working with API iSendPro for campagne, comptage, credit. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# API iSendPro
API version: 1.1.1

## Auth
No authentication required.

## Base URL
https://apirest.isendpro.com/cgi-bin

## Setup
1. No auth setup needed
3. POST /campagne -- create first campagne

## Endpoints

14 endpoints across 12 groups. See references/api-spec.lap for full details.

### campagne
| Method | Path | Description |
|--------|------|-------------|
| POST | /campagne | Retourne les SMS envoyés sur une période donnée |

### comptage
| Method | Path | Description |
|--------|------|-------------|
| POST | /comptage | Compter le nombre de caractère |

### credit
| Method | Path | Description |
|--------|------|-------------|
| POST | /credit | Interrogation credit |

### hlr
| Method | Path | Description |
|--------|------|-------------|
| POST | /hlr | Vérifier la validité d'un numéro |

### repertoire
| Method | Path | Description |
|--------|------|-------------|
| POST | /repertoire | Gestion repertoire (creation) |
| PUT | /repertoire | Gestion repertoire (modification) |

### getlistenoire
| Method | Path | Description |
|--------|------|-------------|
| POST | /getlistenoire | Retourne le liste noire |

### setlistenoire
| Method | Path | Description |
|--------|------|-------------|
| POST | /setlistenoire | Ajoute un numero en liste noire |

### dellistenoire
| Method | Path | Description |
|--------|------|-------------|
| POST | /dellistenoire | Ajoute un numero en liste noire |

### shortlink
| Method | Path | Description |
|--------|------|-------------|
| POST | /shortlink | add a shortlink |

### subaccount
| Method | Path | Description |
|--------|------|-------------|
| POST | /subaccount | Ajoute un sous compte |
| PUT | /subaccount | Edit a subaccount |

### sms
| Method | Path | Description |
|--------|------|-------------|
| POST | /sms | Envoyer un sms |

### smsmulti
| Method | Path | Description |
|--------|------|-------------|
| POST | /smsmulti | Envoyer des SMS |

## Enhanced Skill Content
## Question Mapping

- "How do I send an SMS to a single number?" -> POST /sms
- "How do I send SMS messages to multiple recipients at once?" -> POST /smsmulti
- "How many SMS credits do I have left?" -> POST /credit
- "How do I check if a phone number is valid and active?" -> POST /hlr
- "How do I create a new contact list?" -> POST /repertoire
- "How do I update an existing contact list?" -> PUT /repertoire
- "Which phone numbers are on my blacklist?" -> POST /getlistenoire
- "How do I block a number from receiving messages?" -> POST /setlistenoire
- "How do I remove a number from the blacklist?" -> POST /dellistenoire
- "How do I create a tracked short link for my SMS campaign?" -> POST /shortlink
- "How do I check the status of a sent campaign?" -> POST /campagne
- "How many recipients match my campaign filters?" -> POST /comptage
- "How do I create a sub-account for a team member?" -> POST /subaccount
- "How do I modify permissions on a sub-account?" -> PUT /subaccount
- "How do I send a bulk campaign and then verify delivery counts?" -> POST /smsmulti, then POST /campagne

## Response Tips

- **SMS (sms, smsmulti):** Check the per-recipient status code inside the response map; a 200 at the HTTP level does not guarantee every message was accepted.
- **Credit:** The returned balance is a numeric string; parse it to a number before comparing thresholds.
- **HLR:** Lookup results may include carrier and reachability fields; absent fields mean the number could not be resolved.
- **Repertoire:** Create returns the new list ID; store it for subsequent PUT updates or campaign targeting.
- **Blacklist (get/set/del listenoire):** Get returns an array of entries; set and del return confirmation of the affected number count.
- **Campagne & Comptage:** Campaign stats and recipient counts are point-in-time snapshots; re-query for updated delivery states.
- **Subaccount:** Create returns credentials for the new sub-account; these are shown only once.
- **All endpoints:** A 400 response includes an error code and message in the body; always parse both fields for diagnostics.

## Anomaly Flags

- **Low credit balance:** After any `/credit` check, surface a warning if the balance would cover fewer than 100 messages at the current send rate.
- **High blacklist removal volume:** Flag if a `/dellistenoire` call removes more than 50 entries at once, as this may indicate accidental bulk removal.
- **HLR unreachable numbers:** If more than 30% of numbers in a batch HLR lookup return unreachable, warn about list quality before sending a campaign.
- **Repeated 400 errors:** If consecutive calls to the same endpoint return 400, surface the error code pattern -- common causes are expired credentials or malformed phone number formats.
- **Comptage vs. actual send mismatch:** If `/comptage` returns a recipient count significantly different from what `/smsmulti` processes, flag the discrepancy.
- **Sub-account credential exposure:** After `/subaccount` POST, remind the user to store the returned credentials securely since they are not retrievable later.

## Playbook

### 1. Send a bulk SMS campaign with delivery tracking

1. Call `POST /credit` to verify sufficient balance for your recipient count.
2. Call `POST /comptage` with your targeting filters to get the exact recipient count.
3. Call `POST /smsmulti` with your message body and recipient list.
4. Note the campaign ID from the response.
5. Call `POST /campagne` with the campaign ID to monitor delivery status.
6. Repeat step 5 periodically until all messages show a terminal state.

### 2. Clean a contact list before sending

1. Call `POST /repertoire` to create or identify your target contact list.
2. Call `POST /hlr` with the numbers from the list to validate reachability.
3. Collect numbers that returned unreachable or invalid.
4. Call `POST /setlistenoire` to add invalid numbers to the blacklist.
5. Call `PUT /repertoire` to remove invalid numbers from the contact list.

### 3. Manage sub-accounts for team access

1. Call `POST /subaccount` with the new user's details to create the account.
2. Store the returned credentials securely.
3. Call `POST /credit` from the sub-account to confirm its initial balance.
4. To adjust permissions or details later, call `PUT /subaccount` with the updated fields.

### 4. Blacklist management workflow

1. Call `POST /getlistenoire` to retrieve the current blacklist.
2. Review entries for numbers that should be unblocked.
3. Call `POST /dellistenoire` for each number to remove.
4. To add opt-out requests, call `POST /setlistenoire` with the new numbers.
5. Verify the final state by calling `POST /getlistenoire` again.

### 5. Create a tracked SMS with short link

1. Call `POST /shortlink` with your target URL to generate a tracked short link.
2. Note the returned short URL.
3. Compose your SMS body embedding the short link.
4. Call `POST /sms` (single) or `POST /smsmulti` (bulk) with the composed message.
5. Use the short link analytics to track click-through rates alongside `POST /campagne` for delivery stats.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
