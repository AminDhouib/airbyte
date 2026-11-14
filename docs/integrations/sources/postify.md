# Postify
Postify is a social media scheduling and publishing app. This connector reads posts (with their per-channel variants and delivery status), connected channels and media library assets from the Postify REST API.

## Prerequisites

- A Postify account. The free plan includes API access (1,000 API requests per month).
- A Postify organization API key. In Postify, open Settings, then API keys, and create a key. A read-only key is enough: the "Read your data" permission, which covers the `posts:read` and `channels:read` scopes. The key starts with `postify_live_` and is shown only once.

## Configuration

| Input | Type | Description | Default Value |
|-------|------|-------------|---------------|
| `api_key` | `string` | API Key. Postify organization API key (starts with postify_live_). |  |

## Streams
| Stream Name | Primary Key | Pagination | Supports Full Sync | Supports Incremental |
|-------------|-------------|------------|---------------------|----------------------|
| posts | id | Cursor | ✅ |  ❌  |
| channels | id | No pagination | ✅ |  ❌  |
| media | id | Cursor | ✅ |  ❌  |

The Postify API has no updated-since filter, so every sync reads all records again.

## Limits

Each page of records is one API request. The Postify plan sets a monthly request allowance and a per-minute limit per key. The connector waits and retries when the per-minute limit is hit. When the monthly allowance is used up, the sync fails with an explanatory message.

## IP allow list

If you use Airbyte Cloud and your organization restricts access to specific IPs, add the [Airbyte Cloud IP addresses](https://docs.airbyte.com/platform/operating-airbyte/ip-allowlist) to your allow list.

## Changelog

<details>
  <summary>Expand to review</summary>

| Version | Date       | Pull Request | Subject        |
|---------|------------|--------------|----------------|
| 0.0.1 | 2026-11-14 | | Initial release by [@AminDhouib](https://github.com/AminDhouib) via Connector Builder |

</details>
