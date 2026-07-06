# MCP Directory Submission Checklist

Use this checklist before syncing this listing to the public Weibo MCP repository, submitting it to MCP directories, or updating a directory entry.

## Public Repository

- Primary repository name: `weibo-mcp`
- Fallback repository name if unavailable: `weibo-socialdatax-mcp`
- Repository URL after creation: `https://github.com/DevinChen2014/weibo-mcp`
- Repository description: `微博 MCP / Weibo MCP by SocialDataX for hot search, post search, post details, comments, comment replies, likers, reposts, user profiles, user posts, and transcript.`
- Suggested repository topics: `mcp`, `mcp-server`, `weibo`, `weibo-mcp`, `weibo-data`, `socialdatax`, `social-insights`, `marketing-research`, `comment-analysis`, `creator-analytics`
- Root README title: `微博 MCP | Weibo MCP`
- Product: `SocialDataX` / `社媒数据助手`
- Website: `https://socialdatax.com`
- Registry name: `com.52choujiang/weibo-insights`
- Future registry name: `com.socialdatax/weibo-insights`
- Hosted MCP endpoint: `https://mcp.socialdatax.com/weibo/mcp`
- Hosted auth: `Authorization: Bearer <SOCIALDATAX_API_KEY>`
- Default client transport: hosted `streamable-http`
- Command/stdio fallback: `npx -y mcp-remote https://mcp.socialdatax.com/weibo/mcp --header "Authorization: Bearer <SOCIALDATAX_API_KEY>"`
- License: MIT for the public documentation and examples only

## Safety Checks

- No real API keys are present.
- No private backend implementation is included.
- No production configuration is included.
- No internal samples are included.
- No account data or credentials are included.
- No generated build output is included.
- Public text uses neutral product wording.
- Public docs do not expose internal business code.

## Required Files

- `README.md`
- `LICENSE`
- `server-card.json`
- `mcp.json`
- `glama.json`
- `examples/streamable_http_config.json`
- `examples/claude_desktop_config.json`
- `examples/cursor_mcp.json`
- `examples/codex_config.toml`
- `assets/logo.png`

## Directory Checks

- Hosted streamable HTTP clients can connect directly to `https://mcp.socialdatax.com/weibo/mcp` with `Authorization: Bearer <SOCIALDATAX_API_KEY>`.
- With a valid key, hosted MCP `initialize` succeeds.
- With a valid key, hosted MCP `tools/list` returns the current 18 public tools.
- `weibo_get_hot_search_list` is present in `tools/list`; if it is missing, deploy the latest service before publishing.
- `weibo_get_post_liker_list_by_post_url` and `weibo_get_post_repost_list_by_post_url` are present in `tools/list`; if either is missing, deploy the latest service before publishing.
- `weibo_submit_video_speech_text_by_post_url`, `weibo_submit_video_speech_text_by_post_id`, and `weibo_get_video_speech_text_job` are present in `tools/list`; if any are missing, deploy the latest service before publishing.
- `examples/codex_config.toml` uses remote HTTP URL and `bearer_token_env_var`, not `mcp-remote`.
- `examples/cursor_mcp.json` uses remote HTTP URL and `headers` with `${env:SOCIALDATAX_API_KEY}`, not `mcp-remote`.
- `mcp.json` is explicitly command/stdio fallback and uses `mcp-remote`.
- Before submitting to directories, verify `https://mcp.socialdatax.com/weibo/.well-known/mcp/server-card.json` returns the Weibo server card, not the root XHS server card.

## Directory Submission Order

1. Official MCP Registry
2. GitHub public repository
3. Glama
4. ModelScope MCP 广场
5. MCP.Directory
6. MCP.so
7. mcpservers.org
8. MCP Market
9. Cline MCP Marketplace
10. awesome-mcp-servers / awesome-remote-mcp-servers

## Search Keywords To Verify After Approval

- `Weibo`
- `Weibo MCP`
- `Weibo data MCP`
- `Weibo hot search MCP`
- `Weibo post research MCP`
- `Weibo comments MCP`
- `微博`
- `微博 MCP`
- `微博 数据 MCP`
- `微博 热搜 MCP`
- `微博 帖子 MCP`
- `微博 评论 MCP`
- `微博 用户 MCP`
- `SocialDataX`
- `社媒数据助手`
