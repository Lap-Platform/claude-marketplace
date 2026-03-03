---
name: public-api
description: "Public API skill. Use when working with Public for accounts, dns, domains. Covers 75 endpoints."
version: 1.0.0
generator: lapsh
---

# Public Api
API version: v2

## Auth
ApiKey (inferred from docs)

## Base URL
/v2

## Setup
1. Set your API key in the appropriate header
2. GET /accounts -- verify access
3. POST /accounts -- create first accounts

## Endpoints

75 endpoints across 13 groups. See references/api-spec.lap for full details.

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts | Overview of accounts |
| POST | /accounts | Create a new account |
| GET | /accounts/{accountId} | Get a specific account |

### dns
| Method | Path | Description |
|--------|------|-------------|
| GET | /dns/{domainName}/records | Get records |
| POST | /dns/{domainName}/records | Create a record |
| GET | /dns/{domainName}/records/{recordId} | Get specific record |
| PUT | /dns/{domainName}/records/{recordId} | Edit a record |
| DELETE | /dns/{domainName}/records/{recordId} | Delete a record |

### domains
| Method | Path | Description |
|--------|------|-------------|
| GET | /domains | Overviews of domains |
| GET | /domains/{domainName} | Details of a domain |
| POST | /domains/registrations | Register a domain |
| POST | /domains/transfers | Transfer a domain |
| PUT | /domains/{domainName}/nameservers | Edit domain name servers |
| PUT | /domains/{domainName}/renew | Edit domain name renew state |

### linuxhostings
| Method | Path | Description |
|--------|------|-------------|
| GET | /linuxhostings | Overview of linux hostings |
| GET | /linuxhostings/{domainName} | Linux hosting detail |
| GET | /linuxhostings/{domainName}/phpsettings/availableversions | Get the available PHP versions. |
| PUT | /linuxhostings/{domainName}/phpsettings/version | Change the Linux hosting PHP version. |
| PUT | /linuxhostings/{domainName}/settings/gzipcompression | Enable/disable GZIP compression |
| POST | /linuxhostings/{domainName}/subsites | Create a subsite |
| DELETE | /linuxhostings/{domainName}/subsites/{siteName} | Delete a subsite |
| POST | /linuxhostings/{domainName}/sites/{siteName}/hostheaders | Create a host header |
| PUT | /linuxhostings/{domainName}/sites/{siteName}/http2/configuration | Configure HTTP/2 |
| PUT | /linuxhostings/{domainName}/ftp/configuration | Configure FTP |
| PUT | /linuxhostings/{domainName}/sslsettings/{hostname}/letsencrypt | Configure let's encrypt |
| PUT | /linuxhostings/{domainName}/sslsettings/{hostname}/autoredirect | Configure auto redirect |
| PUT | /linuxhostings/{domainName}/phpsettings/memorylimit | Configure PHP memory limit |
| PUT | /linuxhostings/{domainName}/phpsettings/apcu | Configure PHP APCu setting |
| GET | /linuxhostings/{domainName}/scheduledtasks | Overview of scheduled tasks |
| POST | /linuxhostings/{domainName}/scheduledtasks | Add a scheduled task |
| GET | /linuxhostings/{domainName}/scheduledtasks/{scheduledTaskId} | Get scheduled task detail |
| PUT | /linuxhostings/{domainName}/scheduledtasks/{scheduledTaskId} | Configure a scheduled task |
| DELETE | /linuxhostings/{domainName}/scheduledtasks/{scheduledTaskId} | Delete a scheduled task |
| GET | /linuxhostings/{domainName}/ssh/keys | Overview of SSH keys |
| POST | /linuxhostings/{domainName}/ssh/keys | Add a SSH key |
| PUT | /linuxhostings/{domainName}/ssh/configuration | Configure SSH |
| DELETE | /linuxhostings/{domainName}/ssh/keys/{fingerprint} | Delete a SSH key |

### mailboxes
| Method | Path | Description |
|--------|------|-------------|
| GET | /mailboxes | Gets your mailboxes. |
| POST | /mailboxes | Create a new mailbox. |
| GET | /mailboxes/{mailboxName} | Get a specific mailbox |
| DELETE | /mailboxes/{mailboxName} | Delete a mailbox |
| PUT | /mailboxes/{mailboxName}/password | Change password for mailbox |
| PUT | /mailboxes/{mailboxName}/autoreply | Configure auto-reply for mailbox |
| PUT | /mailboxes/{mailboxName}/autoforward | Configure auto-forward for mailbox |

### mailzones
| Method | Path | Description |
|--------|------|-------------|
| GET | /mailzones/{domainName} | Get the mail zone. |
| POST | /mailzones/{domainName}/catchall | Create a catch-all on the mail zone |
| DELETE | /mailzones/{domainName}/catchall/{emailAddress} | Delete a catch-all on the mail zone |
| PUT | /mailzones/{domainName}/antispam | Configure anti-spam for mail zone |
| POST | /mailzones/{domainName}/aliases | Create a new alias |
| PUT | /mailzones/{domainName}/aliases/{emailAddress} | Configure a alias |
| DELETE | /mailzones/{domainName}/aliases/{emailAddress} | Delete a alias |
| POST | /mailzones/{domainName}/smtpdomains | Create an extra smtp domain |
| PUT | /mailzones/{domainName}/smtpdomains/{hostname} | Configure an extra smtp domain |
| DELETE | /mailzones/{domainName}/smtpdomains/{hostname} | Delete an extra smtp domain |

### mysqldatabases
| Method | Path | Description |
|--------|------|-------------|
| GET | /mysqldatabases | Overview of mysql databases |
| POST | /mysqldatabases | Create a new mysql database |
| GET | /mysqldatabases/{databaseName} | Get a specific database |
| DELETE | /mysqldatabases/{databaseName} | Delete a mysql database |
| GET | /mysqldatabases/{databaseName}/users | Overview of mysql users |
| POST | /mysqldatabases/{databaseName}/users | Create a new mysql user |
| PUT | /mysqldatabases/{databaseName}/users/{userName}/status | Enable/disable mysql user |
| PUT | /mysqldatabases/{databaseName}/users/{userName}/password | Change password for mysql user |
| DELETE | /mysqldatabases/{databaseName}/users/{userName} | Delete a mysql user |

### provisioningjobs
| Method | Path | Description |
|--------|------|-------------|
| GET | /provisioningjobs/{jobId} | Detail of a provisioning job |

### servicepacks
| Method | Path | Description |
|--------|------|-------------|
| GET | /servicepacks | Overview of service packs |

### ssh
| Method | Path | Description |
|--------|------|-------------|
| GET | /ssh | Overview of SSH keys |

### sslcertificaterequests
| Method | Path | Description |
|--------|------|-------------|
| GET | /sslcertificaterequests | Overview of SSL certificate requests |
| POST | /sslcertificaterequests | Add a SSL certificate request |
| GET | /sslcertificaterequests/{id} | Detail of a SSL certificate request |
| PUT | /sslcertificaterequests/{id} | Verify the SSL certificate request domain validations |

### sslcertificates
| Method | Path | Description |
|--------|------|-------------|
| GET | /sslcertificates | Overview of SSL certificates |
| GET | /sslcertificates/{sha1Fingerprint} | Detail of a SSL certificate |
| GET | /sslcertificates/{sha1Fingerprint}/download | Download a SSL certificate |

### windowshostings
| Method | Path | Description |
|--------|------|-------------|
| GET | /windowshostings | Overview of windows hostings |
| GET | /windowshostings/{domainName} | Windows hosting detail |

## Enhanced Skill Content
## Question Mapping

- "What hosting accounts do I have?" -> GET /v2/accounts
- "Show me the DNS records for example.com" -> GET /v2/dns/{domainName}/records
- "Add an A record pointing to 1.2.3.4 for my domain" -> POST /v2/dns/{domainName}/records
- "What PHP version is my Linux hosting running?" -> GET /v2/linuxhostings/{domainName}
- "How much disk space is my hosting using?" -> GET /v2/linuxhostings/{domainName}
- "Register a new domain" -> POST /v2/domains/registrations
- "Transfer my domain from another registrar" -> POST /v2/domains/transfers
- "Create a new mailbox for info@example.com" -> POST /v2/mailboxes
- "Set up auto-reply on my mailbox while I'm on vacation" -> PUT /v2/mailboxes/{mailboxName}/autoreply
- "Create a MySQL database for my WordPress site" -> POST /v2/mysqldatabases
- "Enable Let's Encrypt SSL for my site" -> PUT /v2/linuxhostings/{domainName}/sslsettings/{hostname}/letsencrypt
- "Add a cron job to my hosting" -> POST /v2/linuxhostings/{domainName}/scheduledtasks
- "Is my provisioning job finished yet?" -> GET /v2/provisioningjobs/{jobId}
- "Set up a catch-all email for my domain" -> POST /v2/mailzones/{domainName}/catchall
- "Download my SSL certificate as PFX" -> GET /v2/sslcertificates/{sha1Fingerprint}/download

## Response Tips

- **Accounts, domains, hostings, databases, mailboxes, SSH, SSL lists**: Paginated via `skip`/`take` query params; response is an array -- check total count headers if available.
- **DNS records**: Filterable by `type`, `record_name`, and `service`; each record has a unique `id` (string) needed for updates and deletes.
- **Provisioning jobs**: Returns 200 with `status` and `completion.estimate` while pending, 201 with `resource_links` when done -- poll until status changes.
- **SSL certificate requests**: May return 303 (redirect to completed cert) or 410 (gone/expired) instead of 200 -- handle these status codes explicitly.
- **Mailbox details**: `auto_reply` and `auto_forward` are nested objects; check the `enabled` boolean before reading sub-fields.
- **Mailzone config**: Contains `aliases`, `catch_all`, `anti_spam`, and `smtp_domains` as separate nested structures -- each managed by its own sub-endpoint.
- **Linux hosting details**: `sites` is an array of subsites; `mysql_database_names` lists linked databases but not full details -- follow up with the mysqldatabases endpoint.
- **All write operations**: 201/202 means accepted/created (often asynchronous); 204 means success with no body -- do not try to parse a response.

## Anomaly Flags

- **Provisioning job stuck**: If `GET /provisioningjobs/{jobId}` returns status other than a completion state and `completion.estimate` is in the past, surface a warning that the job may be stalled.
- **SSL certificate expiring soon**: When `GET /sslcertificates/{sha1Fingerprint}` shows `expires_after` within 30 days, alert the user to renew or request a new certificate.
- **Domain not set to auto-renew**: If `GET /domains/{domainName}` returns `will_renew: false` and expiration is within 60 days, warn about potential domain loss.
- **Disk usage high**: When `GET /linuxhostings/{domainName}` shows `actual_size` or `webspace_usage` above 85% of `max_size` or `max_webspace_size`, flag the capacity risk.
- **Database near capacity**: When `GET /mysqldatabases/{databaseName}` shows `actual_size` approaching `max_size`, alert before writes start failing.
- **SSL request returned 410**: The certificate request has expired or been revoked -- surface this immediately as it requires a new request.
- **FTP or SSH disabled unexpectedly**: If `GET /linuxhostings/{domainName}` returns `ftp_enabled: false` or SSH appears off while the user expects access, flag the misconfiguration.

## Playbook

### Set Up a New Linux Hosting Site with SSL

1. `GET /v2/servicepacks` -- list available service packs, pick one.
2. `POST /v2/accounts` -- create an account with the chosen `servicepack_id` and set an FTP password.
3. `GET /v2/provisioningjobs/{jobId}` -- poll the provisioning job until it completes (201 with `resource_links`).
4. `GET /v2/linuxhostings/{domainName}` -- confirm the hosting is active and note the IP.
5. `POST /v2/dns/{domainName}/records` -- add an A record pointing to the hosting IP.
6. `PUT /v2/linuxhostings/{domainName}/sslsettings/{hostname}/letsencrypt` -- enable Let's Encrypt with `enabled: true`.
7. `PUT /v2/linuxhostings/{domainName}/sslsettings/{hostname}/autoredirect` -- enable HTTP-to-HTTPS redirect.

### Configure Email for a Domain

1. `GET /v2/mailzones/{domainName}` -- check existing mail zone settings and available accounts.
2. `POST /v2/mailboxes` -- create mailboxes (e.g., info@, support@) with passwords.
3. `POST /v2/mailzones/{domainName}/aliases` -- set up aliases (e.g., sales@ -> info@).
4. `POST /v2/mailzones/{domainName}/catchall` -- optionally add a catch-all address.
5. `PUT /v2/mailzones/{domainName}/antispam` -- configure anti-spam to `advanced` or `basic`.

### Register a Domain and Point It to Existing Hosting

1. `POST /v2/domains/registrations` -- register the domain with registrant details and preferred nameservers.
2. `GET /v2/provisioningjobs/{jobId}` -- wait for registration to complete.
3. `GET /v2/linuxhostings/{domainName}` -- get the hosting IP from an existing site.
4. `POST /v2/dns/{domainName}/records` -- add A record pointing to the hosting IP.
5. `POST /v2/linuxhostings/{existingDomain}/sites/{siteName}/hostheaders` -- add the new domain as a host header on the existing site.

### Set Up a MySQL Database with Application User

1. `POST /v2/mysqldatabases` -- create the database linked to an `account_id`, set the admin password.
2. `GET /v2/provisioningjobs/{jobId}` -- wait for the database to be provisioned.
3. `GET /v2/mysqldatabases/{databaseName}` -- confirm creation and note the `hostname`.
4. `POST /v2/mysqldatabases/{databaseName}/users` -- create an application-specific user with a strong password.
5. Use the `hostname`, `database_name`, `user_name`, and `password` in your application config.

### Transfer a Domain and Migrate DNS

1. `GET /v2/dns/{domainName}/records` -- export all DNS records from the current provider (done outside this API).
2. `POST /v2/domains/transfers` -- initiate transfer with the `auth_code` from the current registrar.
3. `GET /v2/provisioningjobs/{jobId}` -- poll until the transfer completes.
4. `POST /v2/dns/{domainName}/records` -- recreate each DNS record (A, CNAME, MX, TXT, etc.) one by one.
5. `PUT /v2/domains/{domainName}/renew` -- set `will_renew: true` to ensure the domain auto-renews under the new account.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
