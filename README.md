# Daily Notes — v0.2.6

A personal Mac work journal. Apple Silicon, macOS 13 or newer. Local AI setup requires macOS 14 or newer.

## Update
Use **Check for Updates…** inside your installed Daily Notes app. The signed update replaces the same app and preserves saved activity, manual notes and settings. No new extraction or duplicate application is needed.

For a first installation or repair, extract this package and double-click **Install or Update Daily Notes.command**. The internal application filename remains Daily Flow.app for updater compatibility; its displayed name is Daily Notes. Keep only the installed application in Applications for normal use.

## Local AI work notes
1. Open **Local AI work notes…** in the sidebar.
2. Click **Set up local AI**. Terminal downloads the official Ollama app if needed, starts a local-only service and downloads qwen3:1.7b (about 1.4 GB). No account, subscription or paid API is required. Wait for Setup complete.
3. Click **Check local AI**, then enable **Create work notes automatically**.
4. Enable **Use active-window text for better notes**, and grant Accessibility access in macOS settings. Window titles are an alternative with less task detail.
5. Start tracking and work in another app. Short work-note suggestions appear about every two minutes when useful context is available. **Generate** requests a summary for the selected day immediately.

Work notes describe observed subjects rather than claiming completed work. Review and edit them. They are separate from app-time totals and your manual notes. Editing preserves your wording. Trash buttons ask Yes or No; deleted work notes are not automatically restored from the same observations. Export includes work notes and manual notes, falling back to app-time totals when no work notes exist.

Automatic AI and text capture are off by default. With both disabled, existing app-time tracking continues normally. Local AI failure does not stop activity tracking. Older activity containing only app names cannot reliably produce task descriptions; capture new work context first.

## What is captured
Active app sampling runs every five seconds. Consecutive samples form approximate time blocks. With text capture enabled, short Accessibility text excerpts from the active window are saved at most once every 30 seconds. Text areas require a visible character range; password controls and form text fields are skipped. Some apps expose little or no accessible text. No screenshots, audio or keystrokes are recorded. Sensitive document or chat content can still appear in excerpts. Private browser windows are not automatically detected.

Work context goes only to the local Ollama address 127.0.0.1:11434. The client refuses redirects and remote models. Setup-created services bind to loopback with Ollama cloud disabled and start when you log in. An already running Ollama service is reused; Daily Notes still requires a local GGUF model. Internet is used to download software/models and to check/install app updates.

Activity, excerpts and notes are unencrypted JSON under `~/Library/Application Support/DailyFlow/`, accessible to your macOS account. Turn text capture off to stop future capture. Delete the relevant activity items or day to remove saved excerpts. Delete work notes separately if you also want derived summaries removed; Delete this day removes both. Manual notes are never overwritten by AI.

## Tracking and exclusions
Start tracking once; the running/paused preference persists across updates and restarts. Closing the window keeps the menu-bar tracker running. Quitting stops it until reopened. No time while closed is backfilled. Idle after two minutes; sleep and session changes reset sampling boundaries. Brief switches can be missed, and up to two minutes before idle detection can count.

YouTube exclusion supports Safari, Chrome, Edge, Brave, Vivaldi, Opera and Arc with Automation access. URLs are checked in memory, never saved. If browser access fails, that browser is paused. Unsupported browsers are not filtered. Comma-separated app exclusions apply to both time tracking and new text capture.

## Export and build
Export Markdown notes or an all-day Outlook-compatible .ics file. Import the calendar file yourself; no Microsoft account sync is connected.

Build the source with `zsh build.command` using Apple Command Line Tools. Tests are in Source/Tests. Sparkle 2.10.0 checks signed update archives and feeds. This personal app uses ad-hoc signing, without Apple notarization. The test suite exercises tracking, old-data compatibility, persistence and a simulated local AI server. Real-model quality and app-specific text capture require verification on your Mac after setup.
