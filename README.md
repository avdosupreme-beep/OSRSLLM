# OSRSLLM

OSRSLLM is a starter monorepo for a RuneLite sidebar plugin backed by a wiki-grounded LLM service.

## Architecture at a glance

- `plugin/` is the RuneLite Plugin Hub-facing package.
- `backend/` is the service that searches the OSRS Wiki and calls the LLM.
- The plugin should go in its own public Plugin Hub repository when you are ready to submit it.
- The backend should stay separate and never be shipped in the plugin jar.

## End-to-end flow

1. A player asks a question in the RuneLite sidebar panel.
2. The plugin posts the question to the backend.
3. The backend searches the OSRS Wiki via MediaWiki API.
4. The backend fetches page extracts for the top results.
5. The backend sends grounded context to the LLM.
6. The backend returns the answer plus source links.
7. The sidebar renders the response in a chat-style UI.

## Important split

If you want to publish this to Plugin Hub, the contents of [plugin/README.md](/C:/Users/Avdo/Desktop/OSRSLLM/plugin/README.md) are the part you turn into a plugin repository.

Your backend stays private or separately deployed and the plugin config points to that backend URL.

## Key files

- [plugin/src/main/java/com/osrsllm/plugin/OsrsLlmPlugin.java](/C:/Users/Avdo/Desktop/OSRSLLM/plugin/src/main/java/com/osrsllm/plugin/OsrsLlmPlugin.java)
- [plugin/src/main/java/com/osrsllm/plugin/OsrsLlmConfig.java](/C:/Users/Avdo/Desktop/OSRSLLM/plugin/src/main/java/com/osrsllm/plugin/OsrsLlmConfig.java)
- [plugin/src/main/java/com/osrsllm/plugin/ui/OsrsLlmPanel.java](/C:/Users/Avdo/Desktop/OSRSLLM/plugin/src/main/java/com/osrsllm/plugin/ui/OsrsLlmPanel.java)
- [backend/app/services/wiki_service.py](/C:/Users/Avdo/Desktop/OSRSLLM/backend/app/services/wiki_service.py)
- [backend/app/services/llm_service.py](/C:/Users/Avdo/Desktop/OSRSLLM/backend/app/services/llm_service.py)

## Backend quick start

```bash
cd backend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8081
```

## Plugin quick start

1. Use the Plugin Hub template to create a dedicated plugin repository.
2. Copy the contents of `plugin/` into that repository.
3. Run the RuneLite development client from that template setup.
4. Open the plugin config and set the backend URL.

## Notes

- `plugin/gradle.properties` is set to `latest.release` for RuneLite dependency resolution.
- The plugin avoids extra third-party runtime dependencies to keep Plugin Hub review simpler.
- The current UI is a polished sidebar chat panel, not an in-game overlay, because that fits LLM Q and A much better.
