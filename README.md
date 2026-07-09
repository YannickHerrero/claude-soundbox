# Claude Soundbox 🔊

A small [Claude Code](https://docs.claude.com/en/docs/claude-code) plugin that plays a
different sound depending on what Claude Code is doing. Each state has its own folder of
audio files, and the plugin picks one **at random** every time that state occurs.

## States

| Claude Code state    | Hook event     | Sound folder            |
|----------------------|----------------|-------------------------|
| Task finished        | `Stop`         | `sounds/task-done/`     |
| Waiting for approval | `Notification` | `sounds/approval/`      |
| Waiting for input    | `Notification` | `sounds/waiting-input/` |
| Subagent finished    | `SubagentStop` | `sounds/subagent-done/` |

> The `Notification` event covers both "waiting for approval" and "waiting for input".
> The plugin inspects the notification message to route it to the right folder.

## Install

In Claude Code:

```
/plugin marketplace add YannickHerrero/claude-soundbox
/plugin install claude-soundbox@claude-soundbox
```

## Add your own sounds

The plugin ships with **empty** sound folders — add your own audio files to hear anything.

Drop files into the folder for the state you want:

```
sounds/task-done/       ta-da.mp3, done.wav, ...
sounds/approval/        ping.mp3, ...
sounds/waiting-input/   chime.wav, ...
sounds/subagent-done/   pop.ogg, ...
```

- Supported formats: `.mp3`, `.wav`, `.ogg`, `.flac`, `.m4a`, `.aiff`.
- Put **multiple files** in a folder and one is chosen at random each time.
- A folder with **no** files is simply silent — no error.

## Update

When new sounds are pushed, pull them in Claude Code with:

```
/plugin marketplace update claude-soundbox
```

## Requirements

The plugin plays audio with whatever command-line player it finds, in this order:
`afplay` (macOS), `paplay`/`aplay` (Linux), `ffplay` (ffmpeg), `mpg123`, `play` (SoX),
or `powershell.exe` (Windows/WSL — WAV only).

If none of these is installed, or a sound folder is empty, the plugin does nothing and
never interrupts Claude Code.

## License

MIT — see [LICENSE](LICENSE).
