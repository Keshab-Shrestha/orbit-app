# Orbit

Orbit is a Mac assistant with a team of agents. It runs on your Mac, talks to the AI providers you already use, and keeps your data on your machine.

This repository holds the **downloads and install steps**. Get the app from the [latest release](../../releases/latest).

> Version 0.1.0 is an early release. It is signed with a local identity and not notarized by Apple, so macOS asks you to confirm the first open. The steps are below.

## What it does

- **Chats and agents.** Talk to Claude, Codex, OpenCode, Grok and other providers in one app. Give each agent its own role, memory and limits.
- **Work.** A board of tasks, plans that split big goals, and an inbox of drafts that need you.
- **Automations.** Workflows that run on a trigger or a timer, and schedules that your agents create.
- **Memory and library.** Facts and notes that agents remember, skills, plugins, small apps that an agent builds, and a skill hub that you point at one GitHub repository.
- **Computer control.** An agent can look at the screen and use the mouse and keyboard, with approval cards and a halt key.
- **Voice.** Dictate with a hold key, and have answers read aloud.
- **Telegram.** Chat with your agent from your phone through a bot that you own.
- **Providers.** Add any Claude-compatible API with a key, or use a local OmniRoute gateway as a backup.
- **Usage.** See what every connected provider used.
- **Menu bar.** An Orbit icon with a panel for what needs you, what runs, and a quick message.

## Requirements

- A Mac with Apple silicon (M1 or newer). Intel Macs are not supported.
- macOS 13 or newer. I built and tried the app on macOS 27 only. I have not tried older versions.
- At least one AI provider: a provider command-line tool that you have signed in to (for example `claude`, `opencode` or `grok`), the Codex that comes with the ChatGPT app, or an API key. Orbit does not include any model and does not give you access to one.

## Install

1. Download `Orbit-0.1.0-arm64.zip` from the [latest release](../../releases/latest).
2. Check the download (optional but recommended). In Terminal, in the folder with the file:

   ```sh
   shasum -a 256 -c Orbit-0.1.0-arm64.zip.sha256
   ```

   It must print `Orbit-0.1.0-arm64.zip: OK`.
3. Double-click the zip. Drag **Orbit.app** into your **Applications** folder.
4. Open Orbit. macOS blocks the first open, because the app is not notarized. Use one of these:
   - **System Settings.** Open System Settings > Privacy & Security, scroll to the message about Orbit, and click **Open Anyway**. Confirm with your password.
   - **Terminal.** Remove the download mark, then open the app:

     ```sh
     xattr -dr com.apple.quarantine /Applications/Orbit.app
     open /Applications/Orbit.app
     ```

You need to do this once for each downloaded version.

## First run

1. Open **Settings > Providers** and connect a provider. For Claude, OpenCode or Grok, click **Sign in** and follow the terminal in the window. For an API key, use **API key providers**.
2. Start a chat. Pick a model in the composer.
3. Optional: pin Orbit to the Dock (right-click its Dock icon > Options > Keep in Dock), and use the Orbit icon in the menu bar for quick access.

## Permissions

Orbit asks for a macOS permission only when you use the feature that needs it. You can say no and still use the rest.

| Permission | Used for |
| --- | --- |
| Microphone | Voice dictation |
| Input Monitoring | The hold key for dictation |
| Accessibility | Computer control and typing into other apps |
| Screen Recording | Computer control that reads the screen |

## Downloads on first use

The app itself contains no speech model. When you first use voice, Orbit asks before it downloads a model. It checks every file against a fixed SHA-256 value. The models and their licences are listed in [THIRD_PARTY.md](THIRD_PARTY.md). The speech-to-text model is about 740 MB.

## Privacy

- Orbit makes no outbound call by default. A feature that needs the network asks first or starts only when you turn it on.
- Keys and tokens are write-only. They are kept in Orbit's own secret store and never shown again.
- Your data lives in `~/Library/Application Support/dev.orbit.app`.

## Uninstall

1. Quit Orbit. Move `Orbit.app` to the Trash.
2. Delete the data folder `~/Library/Application Support/dev.orbit.app`.
3. If you turned on **Open Orbit when I log in**, turn it off first, or delete `~/Library/LaunchAgents/dev.orbit.app.login.plist`.

## Known limits

- Apple silicon only. Not notarized yet.
- Telegram reaches Orbit only while Orbit is open and your Mac is awake.
- This is version 0.1.0. Expect rough edges. Please [report them](../../issues/new).

## Licence

MIT. See [LICENSE](LICENSE), [NOTICE](NOTICE) and [THIRD_PARTY.md](THIRD_PARTY.md).
