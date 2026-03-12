# Testing This Project

## What you are testing

- `backend/` runs the wiki retrieval and LLM service.
- `plugin/` is the RuneLite plugin package you load in a development client.

## What you need installed

- IntelliJ IDEA Community Edition
- Java 11
- Git
- Python 3.11 or similar
- A GitHub account

## Step 1. Push this repo to GitHub

1. Create a new GitHub repository.
2. Upload this project to that repository.
3. Keep this repo as your working monorepo if you want both plugin and backend together.

## Step 2. Create a real Plugin Hub plugin repo

1. Generate a new repository from the RuneLite Plugin Hub template.
2. Clone that template repo locally in IntelliJ.
3. Copy the contents of `plugin/` from this repo into the template repo.
4. Rename the package if you want a different final namespace than `com.osrsllm.plugin`.
5. Make sure the plugin main class still matches `plugins=` in `runelite-plugin.properties`.

## Step 3. Run the backend locally

```bash
cd backend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8081
```

Optional:

- Put your OpenAI key into `.env` using `.env.example` as the starting point.
- If you do not set `OPENAI_API_KEY`, the backend will still return retrieved wiki context previews for testing.

## Step 4. Run the RuneLite dev client

1. Open the plugin template repository in IntelliJ.
2. Let Gradle load the project.
3. Open `build.gradle` or `build.gradle.kts` in that plugin repo.
4. Run the `run` Gradle task from IntelliJ.
5. RuneLite development client should open.

## Step 5. Test the plugin in RuneLite

1. Find `OSRS LLM` in the sidebar.
2. Open the plugin config.
3. Set the backend base URL to `http://localhost:8081`.
4. Ask a question like `How do I get a rune pouch?`.
5. Confirm the answer appears and source buttons open wiki pages.

## If it does not show up

- Confirm `runelite-plugin.properties` is present.
- Confirm the `plugins=` value matches the plugin class.
- Confirm the package name refactor was applied everywhere.
- Refresh Gradle dependencies.
- Make sure `runeliteVersion=latest.release` is set.

## For Plugin Hub submission later

- Keep the plugin in its own public repository.
- Keep the backend separate.
- Add a BSD 2-Clause license to the plugin repository.
- Submit the plugin repository and commit hash through the Plugin Hub manifest process.
