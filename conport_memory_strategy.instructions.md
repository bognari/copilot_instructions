---
applyTo: "**"
---
# --- ConPort Memory Strategy ---
conport_memory_strategy:
  initialization:
    actions:
      - "FULLY READ (all 264 lines) ConPort tool description file": ./docs/ConPort_tool.yaml
      - "FULLY READ (all 99 lines) ConPort Caching description file": ./docs/ConPort_caching.yaml
      - "Invoke `get_product_context`... Store result."
      - "Invoke `get_active_context`... Store result."
      - "Invoke `get_decisions` (limit 5 for a better overview)... Store result."
      - "Invoke `get_progress` (limit 5)... Store result."
      - "Invoke `get_system_patterns` (limit 5)... Store result."
      - "Invoke `get_custom_data` (category: \"critical_settings\")... Store result."
      - "Invoke `get_custom_data` (category: \"ProjectGlossary\")... Store result."
      - "Invoke `get_recent_activity_summary` (default params, e.g., last 24h, limit 3 per type) for a quick catch-up. Store result."

  general:
    proactive_logging_cue: "Remember to proactively identify opportunities to log or update ConPort based on the conversation (e.g., if user outlines a new plan, consider logging decisions or progress). Confirm with the user before logging."
    proactive_error_handling: "When encountering errors (e.g., tool failures, unexpected output), proactively log the error details using `log_custom_data` (category: 'ErrorLogs', key: 'timestamp_error_summary') and consider updating active context with open issues if it's a persistent problem. Prioritize using ConPort's item history or recent activity summary to diagnose issues if they relate to past context changes."
    semantic_search_emphasis: "For complex or nuanced queries, especially when direct keyword search (e.g., `search_decisions_fts`, `search_custom_data_value_fts`) might be insufficient, prioritize using semantic search to leverage conceptual understanding and retrieve more relevant context. Explain to the user why semantic search is being used."