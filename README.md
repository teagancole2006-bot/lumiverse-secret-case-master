# Secret Case Master (Lumiverse Spindle)

## Install / update
1. In `spindle.json`, replace `YOUR-USERNAME` in both URLs with your own GitHub username.
2. In this folder run: `bun install` then `bun run typecheck` then `bun run build`.
3. Commit source files, spindle.json, package.json, tsconfig.json, bun.lock, and generated `dist/backend.js` to your GitHub repository. Do NOT commit node_modules.
4. Install/update in Lumiverse's Spindle Extensions area. Grant `generation` and `interceptor` permissions.
5. In a NEW detective chat, send: `[CASEMASTER:START] Create a murder mystery with at least two suspects in District 12. Do not spoil the answer.`
6. Subsequent turns should continue the same case. For a new mystery, create a different chat.

## Troubleshooting (without spoilers)
- Look for `Secret Case Master initialized` in the extension logs.
- Look for `Case Master: saved secret case successfully` after starting a case.
- If you see a JSON validation error, the model failed to produce a valid structured answer. Retry in a new chat or use a model with better JSON support.
- On hosts that do not support required interceptors, case-generation failures may fall back to ordinary generation. Check your host version.
- Do not open the case storage JSON or inspect complete assembled prompts if you want to avoid spoilers.

## Limitations
- Case creation calls the model inside a pre-generation interceptor; the first turn can be slow.
- The same original case is retained when the start token is used again within an existing chat.
- A fixed case file helps continuity but cannot guarantee the narrator model will never leak the answer.
- The extension is a starter implementation; clues and accusations are guided by prompting, not separately validated in code.


## 1.0.3 TypeScript SDK compatibility update

- Includes `type: "quiet"` in the generation request, as required by current `GenerationRequestDTO`.
- Narrows the `unknown` generation response before reading its contents.
- Stops accessing unsupported `context.connectionId`; uses the configured generation connection instead.
- Keeps the minimum at **two distinct named suspects**.

Run `bun install`, `bun run typecheck`, then `bun run build` and commit the updated `dist/backend.js`.
