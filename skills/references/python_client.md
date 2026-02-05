# TrendsAGI Python Client Notes

This file summarizes key SDK behaviors and method-to-endpoint mappings from the official Python client. Use this to mirror SDK behavior when calling endpoints directly.

## Base URL and Auth
- Default base URL: `https://api.trendsagi.com`
- Auth header: `X-API-Key: <key>`
- Default headers: `Accept: application/json` and `Content-Type: application/json`

## Retries and Rate Limits
- Optional retry on HTTP 429 only.
- Retry uses exponential backoff with jitter and honors `Retry-After` when present.
- Rate limit headers include `X-RateLimit-*` and `Retry-After`.

## Trends and Insights
| SDK Method | HTTP | Endpoint | Notes |
| --- | --- | --- | --- |
| `get_trends` | GET | `/api/trends` | Supports filters like `limit`, `period`, `sort_by`, `sort_dir`, `start_date`, `end_date`, `min_snapshots`, `exclude_sentiment`, `interests`. |
| `get_trend` | GET | `/api/trends/{id}` | Fetch a single trend. |
| `get_trend_analytics` | GET | `/api/trends/{id}/analytics` | Period examples: `1h`, `24h`, `7d`, `30d`. |
| `analyze_trend` | POST | `/api/trends/{id}/analyze` | `force_refresh` in JSON body. |
| `get_trend_autocomplete` | GET | `/api/trends/autocomplete` | Query param `q`. |
| `get_trend_categories` | GET | `/api/trends/categories` | Active categories. |
| `search_insights` | GET | `/api/insights/search` | Query param `q`, `limit`. |

## Reports and Recommendations
| SDK Method | HTTP | Endpoint | Notes |
| --- | --- | --- | --- |
| `generate_custom_report` | POST | `/api/reports/custom` | JSON report spec. |
| `get_recommendations` | GET | `/api/intelligence/recommendations` | Filters: `limit`, `offset`, `type`, `sourceTrendQ`, `priority`, `status`, `matchUserInterests`. |
| `perform_recommendation_action` | POST | `/api/intelligence/recommendations/{id}/action` | JSON body with `action` and `feedback`. |

## Crisis and Financial Intelligence
| SDK Method | HTTP | Endpoint | Notes |
| --- | --- | --- | --- |
| `get_crisis_events` | GET | `/api/intelligence/crisis-events` | Filters supported. |
| `get_crisis_event` | GET | `/api/intelligence/crisis-events/{id}` | Fetch by ID. |
| `perform_crisis_event_action` | POST | `/api/intelligence/crisis-events/{id}/action` | JSON body with `action`. |
| `get_financial_data` | GET | `/api/intelligence/financial-data` | Supports `timezone` and filters. |

## User, Export, and Dashboard
| SDK Method | HTTP | Endpoint | Notes |
| --- | --- | --- | --- |
| `get_user_interests` | GET | `/api/user/interests` | List interests. |
| `create_user_interest` | POST | `/api/user/interests` | JSON body. |
| `delete_user_interest` | DELETE | `/api/user/interests/{id}` | Remove interest. |
| `get_export_settings` | GET | `/api/user/export/settings` | Export configs. |
| `create_export_setting` | POST | `/api/user/export/settings` | JSON body. |
| `delete_export_setting` | DELETE | `/api/user/export/settings/{id}` | Remove config. |
| `run_export_now` | POST | `/api/user/export/configurations/{id}/run-now` | Trigger export. |
| `get_export_history` | GET | `/api/user/export/history` | Export history. |
| `get_dashboard_overview` | GET | `/dashboard/overview` | Aggregated stats. |
| `get_recent_notifications` | GET | `/api/user/notifications/recent` | Recent notifications. |
| `mark_notifications_read` | POST | `/api/user/notifications/mark-read` | JSON body with ids. |
| `get_session_info` | GET | `/api/user/session-info` | Session info. |
| `get_user_profile` | GET | `/api/user/profile` | Current user. |
| `get_user_api_keys` | GET | `/api/user/api-keys` | List keys. |
| `create_user_api_key` | POST | `/api/user/api-keys` | JSON body. |
| `delete_user_api_key` | DELETE | `/api/user/api-keys/{id}` | Revoke key. |
| `get_api_usage` | GET | `/api/user/api-usage` | Usage stats. |

## Context Projects and Items
| SDK Method | HTTP | Endpoint | Notes |
| --- | --- | --- | --- |
| `list_context_projects` | GET | `/api/intelligence/context/projects` | List projects. |
| `create_context_project` | POST | `/api/intelligence/context/projects` | JSON body. |
| `get_context_project` | GET | `/api/intelligence/context/projects/{id}` | Fetch project. |
| `delete_context_project` | DELETE | `/api/intelligence/context/projects/{id}` | Delete project. |
| `list_context_items` | GET | `/api/intelligence/context/items` | List items. |
| `create_context_item` | POST | `/api/intelligence/context/items` | JSON body. |
| `get_context_item` | GET | `/api/intelligence/context/items/{id}` | Fetch item. |
| `delete_context_item` | DELETE | `/api/intelligence/context/items/{id}` | Delete item. |
| `get_context_usage` | GET | `/api/intelligence/context/usage` | Usage stats. |

## Agents
| SDK Method | HTTP | Endpoint | Notes |
| --- | --- | --- | --- |
| `list_agents` | GET | `/api/agents` | List agents. |
| `create_agent` | POST | `/api/agents` | JSON body. |
| `get_agent` | GET | `/api/agents/{id}` | Fetch agent. |
| `update_agent` | PUT | `/api/agents/{id}` | Update agent. |
| `delete_agent` | DELETE | `/api/agents/{id}` | Remove agent. |
| `list_agent_conversations` | GET | `/api/agents/{id}/conversations` | List conversations. |
| `get_agent_conversation` | GET | `/api/agents/conversations/{id}` | Fetch conversation. |
| `delete_agent_conversation` | DELETE | `/api/agents/conversations/{id}` | Delete conversation. |
| `chat_with_agent` | POST | `/api/agents/{id}/chat` | Send message. |
| `get_agent_task_status` | GET | `/api/agents/tasks/{id}` | Check analysis task. |

## Miscellaneous
| SDK Method | HTTP | Endpoint | Notes |
| --- | --- | --- | --- |
| `get_blog_posts` | GET | `/api/blog/posts` | List posts. |
| `get_blog_post` | GET | `/api/blog/posts/{slug}` | Get post. |
| `get_plans` | GET | `/api/plans` | Billing plans. |
| `get_status` | GET | `/status` | Service status. |
| `get_status_history` | GET | `/status/history` | Status history. |
| `get_org_members` | GET | `/api/org/members` | Org members. |
| `get_org_invites` | GET | `/api/org/invites` | Org invites. |
| `create_billing_portal_session` | POST | `/api/billing/create-portal-session` | Stripe portal. |
| `get_integration_webhooks` | GET | `/api/integrations/webhooks` | List webhooks. |
| `get_slack_integration_status` | GET | `/api/integrations/slack/status` | Slack status. |
| `track_event` | POST | `/api/events/track` | Event tracking. |

## Streaming
- The SDK uses WebSocket endpoints derived by replacing `http` with `ws` in the base URL.
- Example streams: finance and trends streams (see SDK README for usage patterns).
