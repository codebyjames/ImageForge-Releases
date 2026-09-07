# ImageForge

**A local AI image generator for Windows.** Everything runs on your own
machine — no account, no subscription, no cloud, nothing sent anywhere unless
you ask for it.

### [⬇ Download ImageForge for Windows](../../releases/latest)

*Installer (47 MB) or portable zip (57 MB) · Windows 10/11, 64-bit · free and
[MIT licensed](LICENSE)*

### See it running

https://github.com/user-attachments/assets/193cc798-3c92-4ed5-9b41-a348e9923d6b

*21 seconds, no narration: a prompt typed live, the render on a local GPU,
the gallery, and the API an agent calls. Every picture in it was made by
ImageForge on an RTX 3060.*

![The Generate screen](docs/generate-web.png)

---

**[Read the guide](docs/GUIDE.md)** — what every screen does, which model to use for what, training your own subject, and connecting an agent.

## What it does

|   |   |
|---|---|
| **Write a prompt, get a picture** | Thirteen models built in, from a 3-second draft model to full-quality SDXL and FLUX. It picks sensible settings; every control explains itself in plain words rather than jargon. |
| **Edit what you made** | Img2img, inpainting, and structural control — draw a box, give it a pose, keep a composition. |
| **Train it on your own subject** | Point it at a folder of photos and it trains a LoRA adapter, captioning the images for you. |
| **Runs offline** | Once the engine and a model are downloaded, unplug the network and it keeps working. |
| **Also an API and an MCP server** | The same engine behind an HTTP API and a Model Context Protocol server, so Claude or another agent can generate images through it. |

## Installing

1. **[Download the installer](../../releases/latest)** — `ImageForge-*-setup.exe`
2. Run it. No administrator needed; it installs for your user only.
3. Open ImageForge. The **System** screen offers the image engine.

**Nothing to sign up for, and nothing to configure.** No account, no API key,
no administrator prompt, no firewall rule — the app's own API listens on
`127.0.0.1` only, which Windows does not ask about. A HuggingFace token and a
RunPod key are *optional*, and only if you want gated models or cloud
rendering; the System screen's **Run the checks** button tells you what is
present and what each missing thing would cost you.

> ### About that engine download
>
> The app is 47 MB. The image engine is **about 5 GB more**, and it is not
> bundled — the right build depends on your graphics card, which an installer
> cannot know in advance.
>
> On this machine it took **5 minutes**. If you have an NVIDIA card it
> installs the accelerated build and says so; if you don't, it installs the
> processor build and warns you that renders will be much slower. It does not
> refuse either way.

Prefer not to install anything? The **zip** is the same application — unzip it
anywhere and run `ImageForge.exe`.

---

## ⚠ Windows will warn you about this app

**It is not code-signed, and you will see this:**

> **Windows protected your PC**
> Microsoft Defender SmartScreen prevented an unrecognised app from starting.

Click **More info**, then **Run anyway**.

**Why, honestly:** a code signing certificate costs money every month, and —
this is the part that surprised me — *it would not remove the warning either*.
Microsoft's own documentation says SmartScreen reputation *"builds up
automatically. The prompt stops appearing once the file hash has sufficient
download history."* A signed app from a publisher nobody has heard of shows the
same dialog until enough people have downloaded it. Paying would buy a slower
version of the same warning.

So: it's unsigned, that's a deliberate choice, and here is how to check the
download is really what I published rather than taking my word for it.

### Verify your download

Every release includes `latest.json` with the SHA-256 of the archive:

```powershell
Get-FileHash .\ImageForge-0.1.7-win64.zip -Algorithm SHA256
```

Compare it with the `sha256` field in
[`latest.json`](../../releases/latest/download/latest.json). If they match, the
file is byte-for-byte what was built.

---

## Connecting an agent

ImageForge is also an **MCP server**, so Claude, Cursor or any MCP client can
generate images through it. The **Agents** screen prints the configuration to
paste in — it names the engine's own interpreter and a working directory, so
it works as-is once the engine is installed.

Seven tools are exposed: `generate_image`, `edit_image`, `inpaint_image`,
`assist_prompt`, `list_models`, `rate_output` and `generation_insights`. Each
model in `list_models` carries its licence, so an agent asked for something
commercial can see that SDXL-Turbo is not licensed for it.

There is an HTTP API on `127.0.0.1:8765` as well, with the same engine behind
it. Both are local only.

## What you may do with the pictures

![The System screen](docs/system-web.png)

**The app is MIT — the models are not.** ImageForge ships no model weights; it
downloads them from their publishers to your machine, and *their* licences
govern what you may do with what you generate. They differ, and not in the way
you would guess:

| Model | Commercial use |
|---|---|
| **SD-Turbo** (the default) | Yes — **below US$1,000,000 of annual revenue** |
| **SDXL-Turbo** | **No.** Research and personal use only |
| SDXL family, RealVisXL | Yes, with use restrictions |
| FLUX.1 schnell, FLUX.2 klein | Yes, unrestricted (Apache-2.0) |

The **System** screen lists every one of these with a link to the licence text,
and says which of them your current model falls under. It also tells you when
a feature pulls extra weights on terms of their own — inpainting and depth
control both do.

See [`TERMS.txt`](TERMS.txt) for acceptable use, and
[`THIRD-PARTY-NOTICES.txt`](../../releases/latest) — shipped with the app — for
the 50 open-source packages inside it.

## Privacy

Nothing leaves your machine unless you ask:

- No telemetry, no analytics, no crash reporting, nothing sent at startup
- Downloading the engine or a model contacts HuggingFace, because that is where
  the files are
- The update check contacts GitHub **only when you press it**
- Your prompts and images stay on your disk

Renders go to `%LOCALAPPDATA%\ImageForge\outputs`. Uninstalling leaves them, and
leaves the engine, so reinstalling doesn't mean downloading 5 GB again.

## Requirements

|   |   |
|---|---|
| **OS** | Windows 10 or 11, 64-bit |
| **Graphics** | An NVIDIA card with 8 GB or more is strongly recommended. Works without one, much more slowly — the app installs a processor build and says so. |
| **Disk** | ~5 GB for the engine, plus 2–7 GB per model |
| **Memory** | 16 GB recommended |

## Questions and problems

[Open an issue](../../issues) — bug reports and questions both welcome.

---

*This repository holds **downloads only**. It contains no source code.*
