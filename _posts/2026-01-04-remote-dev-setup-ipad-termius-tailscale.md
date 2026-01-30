---
title: "Claude Code on Your iPhone: Quick Remote Dev Setup with Termius + Tailscale"
date: 2026-01-04
last_modified_at: 2026-01-30T22:00:00+02:00
author_profile: true
classes: wide
header:
  image: "/assets/images/blog/2026-01-04-claude-remote-setup.png"
  og_image: "/assets/images/blog/2026-01-04-claude-remote-setup.png"
  teaser: "/assets/images/blog/2026-01-04-claude-remote-setup.png"
categories:
  - notes
tags:
  - Linux
  - Development
  - Remote
  - Claude Code
  - AI-assisted
---

*This post was written with assistance from Claude, an AI by Anthropic.*
{: .notice--info}

Want to run Claude Code from your iPhone or iPad? Here's how I set it up - and yes, it actually works great for quick fixes on the go.

<figure style="display: flex; gap: 20px; align-items: flex-start; flex-wrap: wrap;">
    <div style="flex: 1; min-width: 300px;">
        <a href="/assets/images/blog/2026-01-04-termius-ipad.png">
            <img src="/assets/images/blog/2026-01-04-termius-ipad.png" style="width:100%; height:auto;">
        </a>
        <figcaption>Claude Code running on iPad via Termius</figcaption>
    </div>
    <div style="flex: 1; min-width: 300px;">
        <a href="/assets/images/blog/2026-01-04-termius-iphone.jpg">
            <img src="/assets/images/blog/2026-01-04-termius-iphone.jpg" style="width:100%; height:auto;">
        </a>
        <figcaption>Yes, even on iPhone - Termius has a great mobile keyboard</figcaption>
    </div>
</figure>
<br>

### What You Need

- An Ubuntu machine (local, cloud VM, whatever)
- [Termius app][TermiusAppStore] on your iPhone/iPad (free version works)
- A [Tailscale][TailscaleHome] account (also free)

### Step 1: Set Up Your Dev Machine

SSH into your Ubuntu machine and run my setup script:

**Friendly reminder:** Always [read scripts][dotfileRepo] before running them.
{: .notice--info}

**TLDR:** `./setup-machine.sh && sudo tailscale up` → tailscale login → `npm install -g @anthropic-ai/claude-code`
{: .notice}

```bash
git clone https://github.com/anuraj-rp/dotfiles.git ~/dotfiles
cd ~/dotfiles
./setup-machine.sh
```

**Don't want everything?** Run individual scripts instead:

```bash
./install-tailscale.sh  # Required - for remote access
./install-nodejs.sh     # Required - for Claude Code
./install-tmux.sh       # Recommended - keeps sessions alive
```

Skip what you don't need: `install-docker.sh`, `install-vim.sh`, `install-starship.sh`, `install-nerdfonts.sh`

All scripts support cleanup - e.g. `./install-vim.sh --clean` (remove configs) or `--clean-all` (full uninstall).

The full setup installs:
- **tmux** - keeps your sessions alive when you disconnect
- **vim** with plugins (NERDTree, themes, git integration)
- **Docker**
- **Tailscale** - the magic that makes this work from anywhere
- **Starship prompt** - because life's too short for ugly terminals

### Step 2: Connect to Tailscale

```bash
sudo tailscale up
```

Follow the URL it gives you to authenticate. Then grab your Tailscale IP:

```bash
tailscale ip
```

Keep this IP handy - you'll need it for Termius.

### Step 3: Set Up Termius

1. Open Termius → tap "+" → "New Host"
2. Enter your Tailscale IP as hostname
3. Add your username and password (or set up SSH keys)

Connect and you're in!

### Step 4: Using tmux (Essential for Mobile)

Start a named session:

```bash
tmux new -s dev
```

Now here's the beauty - if your connection drops (happens on mobile), just reconnect and run:

```bash
tmux attach -t dev
```

Everything's exactly where you left it.

Quick tmux commands (prefix is `Ctrl+a`):

| What | Keys |
|------|------|
| New window | `Ctrl+a c` |
| Next/prev window | `Ctrl+a n` / `Ctrl+a p` |
| Split screen | `Ctrl+a \|` or `Ctrl+a -` |
| Detach | `Ctrl+a d` |

### Step 5: Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

Now just run `claude` and start coding from your phone!

### Step 6: Add Claude HUD (Optional)

[Claude HUD][ClaudeHUD] adds a statusline showing context usage, active tools, running agents, and todo progress.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Claude HUD demo</p>&mdash; Jarrod Watts (@jarrodwatts) <a href="https://twitter.com/jarrodwatts/status/2007579355762045121?ref_src=twsrc%5Etfw">January 2026</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Install it from within Claude Code:

```
/plugin marketplace add jarrodwatts/claude-hud
/plugin install claude-hud
/claude-hud:setup
```

### Step 7: Add Speech-to-Text (Optional)

Typing on a phone keyboard gets old fast. Speech-to-text makes Claude Code on mobile genuinely productive - dictate your prompts instead of pecking at tiny keys.

**For iPhone/iPad: [Wispr Flow][WisprFlow]**

Wispr Flow is an AI voice keyboard that works inside any app. Install it, enable the keyboard in iOS Settings, then switch to it when you want to dictate in Termius.

- Automatically adds punctuation and removes filler words
- Works in 100+ languages
- Free tier gives 2,000 words/week

To use: tap the globe icon on your keyboard → select Wispr Flow → start talking.

**For Desktop (Mac/Windows/Linux): [Voquill][Voquill]**

If you're also using Claude Code from your desktop, [Voquill][Voquill] is an open-source alternative worth checking out.

- Runs Whisper locally (no cloud required) or via Groq API
- AI cleanup removes filler words automatically
- Personal glossary for technical terms
- AGPLv3 licensed

Both tools turn voice into polished text, which is exactly what you want when dictating code prompts.

### Pro Tips

**tmux plugins** - Press `Ctrl+a Shift+i` after first launch to install session persistence and vim integration.

**Multiple machines?** Run `tailscale status` to see all your devices. Add each to Termius and switch between them easily.

### Why This Works So Well

Tailscale creates a secure mesh network between your devices. Termius gives you a proper terminal with a mobile-friendly keyboard row (Ctrl, Esc, arrows). And tmux means you never lose your work when switching apps or losing signal.

I've used this setup on trains, buses and coffee shops. It's surprisingly usable for quick bug fixes and code reviews. Give it a shot!

[dotfileRepo]: https://github.com/anuraj-rp/dotfiles.git
[TailscaleHome]: https://tailscale.com
[TermiusAppStore]: https://apps.apple.com/app/termius-ssh-client/id549039908
[ClaudeHUD]: https://github.com/jarrodwatts/claude-hud
[WisprFlow]: https://wisprflow.ai
[Voquill]: https://github.com/josiahsrc/voquill
