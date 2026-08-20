# 微博 MCP | Weibo MCP

This public repository provides public connection docs and MCP metadata for a hosted 微博 MCP / Weibo MCP service by SocialDataX.

If you are looking for a Weibo MCP or 微博 MCP for social media research workflows, this repository includes:

- public MCP metadata and client configuration examples
- the hosted `streamable-http` endpoint for clients that support remote MCP
- an `mcp-remote` fallback example for command/stdio-only MCP clients

The business implementation is privately hosted. This repository exposes only the public connection surface for social media content intelligence workflows.

## Search Aliases

Common search phrases for this MCP service:

- `微博 MCP`
- `微博 数据 MCP`
- `微博 热搜 MCP`
- `微博 帖子 MCP`
- `微博 评论 MCP`
- `微博 用户 MCP`
- `Weibo MCP`
- `Weibo data MCP`
- `Weibo hot search MCP`
- `Weibo post research MCP`
- `Weibo comments MCP`
- `Weibo user MCP`

## Service

- Hosted MCP endpoint: `https://mcp.socialdatax.com/weibo/mcp`
- Hosted transport: `streamable-http`
- Authentication: `Authorization: Bearer <SOCIALDATAX_API_KEY>`
- Product: `SocialDataX` / `社媒数据助手`
- Website: <https://socialdatax.com>
- Registry name: `com.52choujiang/weibo-insights`
- Future registry name: `com.socialdatax/weibo-insights`
- Current public capability version: `0.1.1`

## Platform MCP

Use the hosted `streamable-http` endpoint directly from clients that support authenticated remote MCP. For clients that only support command/stdio MCP servers, use `mcp-remote` as a local compatibility proxy.

## Workflow Scope

This MCP service is designed for social media content intelligence workflows. It does not provide account login, posting, editing, liking, commenting, reposting, or other account actions.

Supported workflows include:

- Query the current API Key account's SocialDataX points balance.
- Read the Weibo / 微博 hot search list.
- Search Weibo posts by keyword or phrase with optional `page_token` continuation; pass only a search term to `keyword`, not a URL or ID.
- Resolve a Weibo post page link, short link, or share text into structured post details.
- Read post details when the caller already has a `post_id`.
- Fetch paginated first-level comments for comment analysis.
- Fetch paginated replies under a first-level comment.
- Fetch paginated liker and repost lists for a post.
- Read user profile data from a user profile link or `user_id`.
- Fetch user post lists from a user profile link or `user_id`.
- Submit a post video speech-to-text transcript task; submit tools 提交完成后最多短等 240 秒, and unfinished jobs should continue polling the same `job_id` until terminal.

## Tools

| Tool | Public purpose |
| --- | --- |
| `socialdatax_get_points_balance` | Query the current API Key account's SocialDataX points balance. |
| `weibo_get_hot_search_list` | Get the current Weibo / 微博 hot search list. |
| `weibo_search_posts` | Search Weibo posts by keyword or phrase. Use this tool when the user needs posts found by a search term; when a post URL or `post_id` is already available, use the corresponding post tool; when a user profile URL or `user_id` is available, use the corresponding user tool. Supports `page_token` continuation. |
| `weibo_get_post_detail_by_post_id` | Fetch structured post details when the caller already has a `post_id`. |
| `weibo_get_post_detail_by_post_url` | Resolve a Weibo post page link, short link, or share text into structured post details. |
| `weibo_get_post_comments_by_post_id` | Fetch paginated first-level comments when the caller already has a `post_id`. |
| `weibo_get_post_comments_by_post_url` | Fetch paginated first-level comments directly from a Weibo post page link, short link, or share text. |
| `weibo_get_post_comment_replies_by_comment_id` | Fetch paginated replies under a first-level comment by `post_id` and `comment_id`. |
| `weibo_get_post_liker_list_by_post_id` | Fetch paginated users who liked a Weibo post by `post_id`. |
| `weibo_get_post_liker_list_by_post_url` | Fetch paginated users who liked a Weibo post from a post page link, short link, or share text. |
| `weibo_get_post_repost_list_by_post_id` | Fetch paginated reposts for a Weibo post by `post_id`. |
| `weibo_get_post_repost_list_by_post_url` | Fetch paginated reposts for a Weibo post from a post page link, short link, or share text. |
| `weibo_get_user_info_by_user_id` | Fetch user profile data when the caller already has a `user_id`. |
| `weibo_get_user_info_by_profile_url` | Resolve a Weibo user profile link into user profile data. |
| `weibo_get_user_posts_by_user_id` | Fetch a paginated list of posts published by a user when the caller already has a `user_id`. |
| `weibo_get_user_posts_by_profile_url` | Fetch a paginated list of posts published by a user from a Weibo user profile link. |
| `weibo_submit_video_speech_text_by_post_url` | Submit a post video speech-to-text transcript task from a post page link, short link, or share text. 提交完成后最多短等 240 秒；未完成时继续查询同一个 `job_id` 直到终态. |
| `weibo_submit_video_speech_text_by_post_id` | Submit a post video speech-to-text transcript task from a `post_id`. 提交完成后最多短等 240 秒；未完成时继续查询同一个 `job_id` 直到终态. |
| `weibo_get_video_speech_text_job` | Continue checking a post video speech-to-text transcript job by `job_id` returned from a submit tool, without creating a new task; each call waits up to 240 seconds. If unfinished, continue querying the same `job_id` until terminal. This v1 surface returns transcript plus content context, not summary. |

## Quick Start

For clients that support authenticated `streamable-http`, use the hosted endpoint directly:

```json
{
  "mcpServers": {
    "socialdatax-weibo": {
      "type": "streamable_http",
      "url": "https://mcp.socialdatax.com/weibo/mcp",
      "headers": {
        "Authorization": "Bearer <SOCIALDATAX_API_KEY>"
      }
    }
  }
}
```

A ready-to-copy example is available in [`examples/streamable_http_config.json`](examples/streamable_http_config.json).

For command/stdio-only MCP clients, use `mcp-remote`:

```json
{
  "mcpServers": {
    "socialdatax-weibo": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://mcp.socialdatax.com/weibo/mcp",
        "--header",
        "Authorization: Bearer <SOCIALDATAX_API_KEY>"
      ]
    }
  }
}
```

Claude Code can use remote HTTP directly:

```bash
claude mcp add --transport http socialdatax-weibo https://mcp.socialdatax.com/weibo/mcp --header 'Authorization: Bearer ${SOCIALDATAX_API_KEY}'
```

Persist `SOCIALDATAX_API_KEY` in the runtime environment or client Secret before restarting Claude Code.

Claude Desktop should use its remote MCP / Connectors UI when available. If a local configuration file in your version only supports command/stdio servers, use the `mcp-remote` fallback.

## Client Examples

Configuration examples are available in [examples](examples/):

- [Command/stdio fallback config](mcp.json)
- [Claude Desktop fallback config](examples/claude_desktop_config.json)
- [Cursor remote HTTP config](examples/cursor_mcp.json)
- [Codex remote HTTP config](examples/codex_config.toml)
- [Direct streamable HTTP config](examples/streamable_http_config.json)

## API Key

Request or manage API access from the product website:

<https://socialdatax.com>

Use the key as a Bearer token in the `Authorization` request header. Do not commit real API Key values to code, docs, issues, or screenshots.

## Directory Metadata

Public metadata files in this repository:

- [server-card.json](server-card.json): directory-oriented metadata for the hosted service. Official MCP Registry publishing uses the private source repo's `registry/weibo/server.json` for the current `com.52choujiang/weibo-insights` entry.
- [mcp.json](mcp.json): generic command/stdio fallback config using `mcp-remote`.
- [glama.json](glama.json): Glama repository ownership metadata.
- [SUBMISSION_CHECKLIST.md](SUBMISSION_CHECKLIST.md): checklist for MCP directory submissions.

## License

The files in this public repository are released under the MIT License. The license covers the public documentation and configuration examples in this repository only. It does not cover the managed service implementation, hosted infrastructure, or any private backend code outside this repository.
