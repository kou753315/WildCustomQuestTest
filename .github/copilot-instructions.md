# WildCustomQuest AI Coding Guidelines

## Project Architecture
WildCustomQuest is a web-based tool for generating custom quests in Monster Hunter Wild (MHW:Iceborne). It consists of:
- **Web Interface**: `quest_generator.html` - Single-page app that loads JSON data and generates quest files
- **Data Files**: JSON databases (`enemies.json`, `items.json`, `reward_list_*.json`) with multilingual support
- **Quest Output**: Generates `.raw.json` (quest structure) and `.ext.json` (rewards) files for Custom Quest Loader mod
- **Data Extraction**: Lua scripts (`itemdump.lua`) for extracting game data using REFramework

## Critical Workflows
- **Quest Generation**: Open `quest_generator.html` in browser → select monsters from `enemies.json` → configure rewards from `items.json` → download ZIP with quest files
- **Data Dumping**: Run `lua itemdump.lua <language_id>` (requires REFramework mod active in game)
- **Mod Integration**: Place generated `.raw.json` and `.ext.json` in Custom Quest Loader's quest folder

## Project Conventions
- **JSON Structure**: Maintain `fixedId`, `id`, `label` fields; preserve multilingual `name` objects with all supported locales
- **Naming**: Use CamelCase for properties; keep `id`/`fixedId` references intact across files
- **Encoding**: UTF-8 with CRLF line endings for JSON files
- **Quest Files**: `.raw.json` contains complex nested quest data; `.ext.json` has reward arrays with `itemId`, `minCount`/`maxCount`, `probability`

## Key Files
- `quest_generator.html`: Main interface - loads data via `fetch()`, builds quest objects, exports JSON
- `enemies.json`: Monster database - example: `{"fixedId": 26, "id": 0, "label": "EM0001_00_0", "name": {"en-us": "Rathian", ...}}`
- `quest_examples/`: Reference quest structures - study `10086.raw.json` for quest data format, `10086.ext.json` for rewards

## Dependencies
- Requires Custom Quest Loader mod by kassent for in-game use
- Lua scripts need REFramework for game data access
- No build system - static web app with local JSON files