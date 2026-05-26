# Ironveil Depths — AI Game Master

A browser-based text RPG where an LLM acts as a persistent Game Master running a dark fantasy dungeon adventure. You type actions, the AI narrates what happens, and your health, inventory, gold, and location update live in the sidebar.

No server, no install. Just open the HTML file in a browser.

---

## How it works

You type an action. That gets sent to the OpenRouter API along with your full conversation history and a structured system prompt. The model responds with narrative text and a JSON block encoding the current game state. The page parses the JSON and updates the UI in real time.

```
Your action → OpenRouter API (full history + system prompt)
                        ↓
        narrative text + GAMESTATE:{...} JSON
                        ↓
        page parses them apart
                        ↓
        chat updates + sidebar animates new state
```

The prompt engineering is the core technical piece — getting the model to stay in character as a GM while reliably outputting valid structured JSON at the end of every single response took iteration to get right.

---

## Stack

- **Frontend:** HTML + CSS + Vanilla JavaScript (single file, no frameworks)
- **LLM:** NVIDIA Nemotron 3 Super 120B via OpenRouter API (free tier)
- **No backend** — API calls go directly from the browser

---

## Running it

You need a free OpenRouter API key — sign up at https://openrouter.ai, no credit card needed.

1. Download `ironveil.html`
2. Open it in any browser
3. Paste your OpenRouter key in the setup screen
4. Start playing

---

## What I learned

- How to write a system prompt that makes an LLM output consistent, parseable JSON on every response while staying in character
- Managing multi-turn conversation state (sending full history on every API call so the GM remembers everything)
- Parsing structured output embedded inside free-form LLM responses
- The difference between a chatbot and a game AI agent is mostly just prompt design

---

## What's next

- Save/load game state to localStorage
- Image generation for room descriptions using an AIGC API
- Dice-roll probability system for combat outcomes
- Voice narration via a TTS API
