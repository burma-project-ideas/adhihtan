# Adhihtan (အဓိဋ္ဌာန်)

An offline-capable daily Buddhist practice planner and prayer-bead counter, built with .NET 10 Blazor WebAssembly for learners and contributors in [Burma Project Ideas](https://github.com/burma-project-ideas).

[Live app](https://adhihtan.vercel.app/) · [Repository](https://github.com/burma-project-ideas/adhihtan) · [Source credits](THIRD_PARTY_NOTICES.md)

## Contributors and sources

| Contributor / source | Contribution |
| --- | --- |
| [Sann Lynn Htun (@sannlynnhtun-coding)](https://github.com/sannlynnhtun-coding) | Git-history contributor; Blazor application and interface implementation |
| Original Android app `com.a_dhi_htan`, version 1.3.1 | Recovered practice content and schedules; original author and redistribution terms are not identified in the recovered metadata |
| [Board UI](https://www.boardui.com/) | Visual reference for the floating sidebar, dashboard panels, buttons, and grouped settings |
| Rabbit conversion rules (`rabbit-node` 1.0.4) | Unicode/Zawgyi conversion rules used by the generated converter |

The interface is an app-specific Blazor implementation inspired by Board UI. It does not install Board UI's React components or include its paid template source. See the notices for provenance and licensing limitations.

## How it works

1. Open **Setup**, select a practice, level, chant, and counts per round. Custom daily practice accepts 1–108 rounds and 1–108 counts per round.
2. Save the plan. **Counter** shows today's chant, current count, target, and progress. Tap to count; use Undo to reverse a count. Reset asks for confirmation when enabled.
3. **Home** summarizes today's progress, totals, and recent activity. **Categories** lets you search practice names and descriptions and read instructions, benefits, and schedules.
4. In **Settings**, choose Myanmar or English, counter style, feedback, screen wake lock, themes, contrast, and text encoding. Myanmar is the default. Preferences persist on this browser.
5. Export a JSON backup to keep a separate copy of your plan, preferences, counts, and history. Restore accepts version-1 backup envelopes and replaces current state; keep a backup before restoring. The file picker accepts JSON files up to 5 MB.

Inputs are practice selections, counting actions, settings, searches, and optional backup files. Outputs are a saved schedule, daily counts and completion history, shareable progress text, and downloadable JSON backups. Processing and persistence run in the browser with IndexedDB; no application account or server database is required.

## Features and limitations

- Five practice categories, including a custom daily plan, and 13 counter styles.
- Light/dark and high-contrast modes, orange branding, keyboard focus states, native form controls, and reduced-motion support.
- English interface labels, dates, and numbers. Prayer names, source instructions, and some generated messages remain Burmese; this is not a complete translation of religious content.
- Release builds cache application assets for offline use after a successful initial online visit. Development service workers are network-only. Offline installation depends on browser storage and successful asset caching.
- Clearing site data or changing browsers/devices loses local state unless you exported a backup. There is no cross-device synchronization.
- Sound, vibration, sharing, clipboard, and wake lock depend on browser/device support and permissions.
- Restore checks the envelope and normalizes preferences; it is not a comprehensive validator of every nested schedule field. Import only backups you trust.
- Generated content and bundled media have incomplete upstream ownership metadata. This repository does not claim ownership or grant an additional license over them.

## Project structure

| Path | Purpose |
| --- | --- |
| `Adhihtan/Pages/` | Home, setup, counter, category list/detail, settings, and not-found routes |
| `Adhihtan/Components/`, `Layout/` | Shared counter, navigation, toggles, icons, and app shell |
| `Adhihtan/Services/` | State, persistence/JS interop, translation labels, and Burmese date formatting |
| `Adhihtan/Models/` | Persisted preferences, plans, backup envelope, and content models |
| `Adhihtan/wwwroot/` | Styles, images/audio, recovered JSON, browser APIs, and PWA files |
| `scripts/` | Vercel SDK installation and Release publish scripts |
| `tools/` | Content and converter recovery utilities; original decompiled input is not bundled |
| `vercel.json` | Build commands, static output, SPA rewrites, and cache headers |

## Local setup

Install the .NET 10 SDK, then:

```powershell
git clone https://github.com/burma-project-ideas/adhihtan.git
cd adhihtan
dotnet restore
dotnet run --project .\Adhihtan\Adhihtan.csproj
```

Open the URL printed by the development server. The existing checkout may still be named `blazor-adhihtan`; the directory name does not affect the app.

## Build and deployment

```powershell
dotnet build .\Adhihtan.sln
dotnet publish .\Adhihtan\Adhihtan.csproj -c Release -o .\artifacts\publish
```

Serve `artifacts/publish/wwwroot` over HTTPS with fallback to `index.html` for client routes such as `/setup` and `/settings`. Test the published build to verify PWA/offline behavior.

Vercel uses `scripts/vercel-install.sh` to install .NET 10 and `scripts/vercel-build.sh` to publish into `artifacts/vercel/wwwroot`. `vercel.json` configures SPA routing and service-worker cache revalidation. After transferring the GitHub repository, verify the Vercel project's Git integration points to `burma-project-ideas/adhihtan` and that the Vercel GitHub App can access the organization. Existing production hosting alone does not prove future Git-triggered deployments are connected.

The public live URL is https://adhihtan.vercel.app/. Individual immutable deployment URLs may require Vercel authentication.

## Contributing and verification

Read `Adhihtan/AGENTS.md` first. Keep the standalone Blazor framework and offline core flows. Do not introduce server dependencies or copy paid design-system source without the appropriate license.

Build before submitting. Check plan setup, count/undo/reset, language persistence, category search and tabs, backup/restore, and direct route loading. Check narrow/mobile and desktop layouts, keyboard focus, light/dark/high-contrast themes, and reduced motion. A successful build is not a substitute for device and offline testing.

The recovery utilities require Node.js and an original decompiled JavaScript input, for example:

```powershell
node tools/recover-hermes-data.mjs <decompiled.js> <output.json>
```

They are maintenance tools, not part of the normal user workflow. Only run recovery on source you have permission to use.
