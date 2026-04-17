# 🎙️ Mic Destroyer 3000

> *Turn your microphone into an absolute nightmare — on purpose.*

Mic Destroyer 3000 is a free, open-source Windows audio utility that routes your microphone through a virtual cable and applies real-time audio destruction effects — clipping, noise, distortion, and more — making your mic sound as catastrophically bad as possible. Perfect for trolling, testing audio pipelines, content creation, or just having fun.

---

## ✨ Features

- 🔊 **Real-time audio destruction** — extreme clipping, noise injection, pitch warping, and distortion applied live
- 🔌 **Auto VB-Cable install** — automatically installs a virtual audio cable driver if not already present
- 🎛️ **Auto device detection** — attempts to automatically select the correct input/output audio devices on launch
- 🖥️ **Clean GUI** — simple, easy-to-use interface built with CustomTkinter
- ⚡ **Lightweight** — no background services, no telemetry, no bloat
- 💸 **Completely free** — MIT licensed, open source

---

## 📥 Installation

### Option 1 — Installer (Recommended)
1. Download `MicDestroyer3000_Setup.exe` from the [Releases](../../releases) page
2. Run the installer and follow the on-screen steps
3. If prompted, allow the VB-Cable audio driver to install
4. **Restart your PC** after installation if prompted — required for the virtual audio device to appear

### Option 2 — Build from Source
See [Building from Source](#building-from-source) below.

---

## 🚀 Usage

1. Launch **Mic Destroyer 3000**
2. The app will attempt to auto-select your microphone as input and VB-Cable as output
3. If audio devices are incorrect, manually select them from the dropdowns
4. Press **Start** to begin destroying your mic audio in real time
5. Set your communication app (Discord, Zoom, etc.) to use **VB-Cable Output** as its microphone input

> ⚠️ If no audio devices appear after install, restart your PC and relaunch the app.

---

## 🛠️ How It Works

Mic Destroyer 3000 works by capturing your real microphone input and routing it through a virtual audio pipeline:

```
[Your Mic] → [Python Audio Capture] → [Destruction Effects] → [VB-Cable Virtual Input] → [Any App]
```

### Tech Stack

| Component | Technology |
|---|---|
| Language | Python 3.14 |
| GUI | CustomTkinter |
| Audio Capture & Playback | SoundDevice |
| Audio Processing | NumPy, SciPy |
| Virtual Audio Driver | VB-Audio Virtual Cable (VB-Cable) |
| Packaging | PyInstaller 6 |
| Installer | Inno Setup 6 |

### Audio Effects Pipeline

The app processes audio in real-time chunks through a chain of effects:

- **Hard Clipping** — brutally clips the waveform above a threshold, causing harsh distortion
- **Noise Injection** — adds randomized white noise on top of the signal
- **Gain Staging** — cranks the volume far beyond normal levels before clipping
- **Optional Filters** — low/high pass filtering via SciPy to selectively destroy frequency ranges

All processing is done in NumPy float32 arrays for low-latency performance, then output to the VB-Cable virtual device which any application can use as a microphone source.

### Virtual Cable (VB-Cable)

[VB-Audio Virtual Cable](https://vb-audio.com/Cable/) is a free virtual audio driver that creates a pair of virtual audio devices — a virtual output and a virtual input. Mic Destroyer routes destroyed audio into this virtual cable, so any app that listens to the cable's input receives the mangled signal.

The installer will automatically install VB-Cable silently if it is not detected. A system restart may be required for Windows to register the new audio devices.

---

## 🔨 Building from Source

### Prerequisites

- Python 3.10+
- pip

### Steps

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/Mic-Destroyer.git
cd Mic-Destroyer

# Install dependencies
pip install -r requirements.txt

# Run directly
python mic_destroyer.py

# Or build the executable
pyinstaller mic_destroyer.spec
```

### Building the Installer

1. Install [Inno Setup 6](https://jrsoftware.org/isinfo.php)
2. Place `VBCABLE_Setup.exe` in the `drivers\` folder (download from [vb-audio.com](https://vb-audio.com/Cable/))
3. Compile `installer.iss` with Inno Setup

---

## ⚙️ Requirements

- Windows 7 SP1 or later (64-bit)
- A working microphone
- ~150 MB disk space (includes Python runtime bundled by PyInstaller)
- Administrator rights (required for VB-Cable driver installation)

---

## ❓ Troubleshooting

**Audio devices don't appear after install**
→ Restart your PC. Windows needs a reboot to register new audio drivers.

**App launches but no sound is being routed**
→ Make sure you've selected the correct input (your mic) and output (VB-Cable Input) in the dropdowns, then press Start.

**My communication app isn't picking up the destroyed audio**
→ In your app's audio settings, set the microphone to **CABLE Output (VB-Audio Virtual Cable)**.

**Windows SmartScreen warns about the installer**
→ This is normal for new unsigned apps. Click *More info → Run anyway*. The app contains no malware. You can verify by building from source.

**VB-Cable install fails**
→ Try manually downloading and installing VB-Cable from [vb-audio.com/Cable](https://vb-audio.com/Cable/), then relaunch Mic Destroyer 3000.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

You are free to use, copy, modify, merge, publish, distribute, and sublicense this software for any purpose, including commercially, as long as the original copyright notice is retained.

---

## 🙏 Credits

- [VB-Audio](https://vb-audio.com/) for the VB-Cable virtual audio driver
- [CustomTkinter](https://github.com/TomSchimansky/CustomTkinter) for the modern UI framework
- [PyInstaller](https://pyinstaller.org/) for Python packaging
- [Inno Setup](https://jrsoftware.org/isinfo.php) for the Windows installer

---

*Built for fun. Use responsibly. Or don't — that's kind of the point.*
