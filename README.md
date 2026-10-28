# CheapHDR 🌈

Cinema-grade HyperHDR ambient backlighting for practically ANY budget USB WS2812B LED strip.  
**No soldering. No flashing WLED. No headaches.**

---

## 📖 Backstory

I always loved how Ambilight and Govee setups looked, but I could never bring myself to justify the high price tag. A monitor setup is far cheaper, so I picked up a budget USB screen-sync LED kit from TikTok Shop.

Because of how cheap it was, it used a single USB connection paired with bad software called **DX Light**. The app was buggy, had terrible color transitions, and the lights would randomly turn on at full brightness in the middle of the night whenever my computer woke up or ran background updates, so I ended up leaving them unplugged most of the time. Rather than throwing the strip away or cutting the wires to solder an ESP32 or Raspberry Pi Pico, I used **Antigravity** to build a high-speed local bridge. **CheapHDR** translates HyperHDR frame packets directly into native USB commands, giving you smooth, cinema-grade screen sync while keeping the factory cable completely stock.

---

## ⚡ What Makes CheapHDR Universal?

CheapHDR includes dual-mode automatic detection out of the box:

1. **Budget USB-HID Strips (Plug & Play):** Auto-detects Robobloq, DX-Light, SyncLight, Quiklight, and generic Amazon / AliExpress / TikTok Shop kits (`1A86:FE07`) across any USB port.
2. **Standard USB WS2812B Strips (Serial / Adalight):** Auto-detects Arduino, CH340, CP2102, FTDI, and Raspberry Pi Pico kits on COM ports.
3. **No Flashing or Soldering Needed:** Bypasses the hassle of flashing custom firmware or wiring DIY microcontrollers.

---

## ⚡ 60-Second Quick Start

1. **Download this:**
   * Click the green **`<> Code`** button $\rightarrow$ **Download ZIP** (or grab `CheapHDR.zip` from Releases).
   * Extract the folder to your PC.

2. **Configure HyperHDR:**
   * In HyperHDR settings, set your LED Controller to stream to `127.0.0.1:2801`.
   * Set your LED layout to match your monitor.

3. **Click this:**
   * Double-click **`Start-CheapHDR.bat`**.

4. **This process will happen:**
   * CheapHDR automatically detects your USB light strip across any port.
   * It starts the high-speed local bridge on `127.0.0.1:2801`.
   * HyperHDR connects and your lights immediately begin mirroring your screen!

5. **If you want it to run automatically on PC startup:**
   * Double-click **`Add-To-Startup.bat`**.
   * It will now start completely silently in the background whenever Windows boots.

6. **If you ever want to deactivate or turn it off:**
   * **To stop it right now:** Click **`Stop-CheapHDR.bat`**.
   * **To remove from Windows startup:** Click **`Remove-From-Startup.bat`**.
  
   * 
## ⚙️ 2-Minute HyperHDR Setup (One-Time)

Download and open [HyperHDR](https://github.com/awawa-dev/HyperHDR/releases) (in your browser at **`http://localhost:8090`**):

1. **Set Controller:**
   * Go to **LED Hardware** $\rightarrow$ **LED Controller**.
   * **Controller type:** Select **`udpraw`**.
   * **Target IP:** `127.0.0.1`
   * **Port:** `2801`
   * **LED count:** Enter your strip's total LED count (default is `63` for standard 27" monitor strips).
   * *Click **Save settings**.*

2. **Set Monitor LED Layout:**
   * Go to **LED Hardware** $\rightarrow$ **LED Layout**.
   * Enter the number of LEDs on each side of your monitor (e.g., Top: `29`, Left: `17`, Right: `17`, Bottom: `0`).
   * Choose your starting corner and direction (Clockwise / Counter-Clockwise).
   * *Click **Save settings**.*

3. **Turn On Movie Anti-Strobe (The Fix!):**
   * Go to **Image Processing**:
     * **Black Border Detection:** Check **Enable** *(Threshold: `5%`)*.  
       *(This automatically ignores widescreen movie black bars so your lights never flicker).*
     * **Smoothing:** Check **Enable** *(Settling time: `160ms` – `220ms`)*.  
       *(Turns harsh flickers into smooth, luxurious ambient blooms).*
     * **Update frequency:** Set to **`30Hz`** *(optimal 30 FPS, near-zero CPU usage)*.
   * *Click **Save settings**.*

4. **Turn On Output:**
   * On the **Overview** dashboard, turn **System Screen Capture** $\rightarrow$ **ON** 🟢, **LED Device** $\rightarrow$ **ON** 🟢, and turn **USB Capture** $\rightarrow$ **OFF** 🔴.
   * Click the top-right master power button to **ON** 🟢.

**Your lights will now mirror your screen smoothly!**

---

## 📁 What Each File Does

| File | What It Does |
|---|---|
| `Start-CheapHDR.bat` | Opens CheapHDR with a status window showing connection, port, and live FPS. |
| `Start-CheapHDR-Hidden.vbs` | Runs CheapHDR silently in the background with zero visible windows. |
| `Add-To-Startup.bat` | Adds CheapHDR to your Windows Startup folder for automatic boot. |
| `Remove-From-Startup.bat` | Deletes CheapHDR from your Windows Startup folder. |
| `Stop-CheapHDR.bat` | Immediately closes and kills all running CheapHDR background processes. |
| `build.bat` | Recompiles the executable from source using Windows' built-in `.NET` compiler (`csc.exe`). |

---

## 🛠️ Repository Structure

```text
CheapHDR/
├── bin/
│   └── CheapHDR.exe          <-- Standalone binary (0 external dependencies)
├── src/
│   └── Program.cs            <-- Clean C# source code (HID + Adalight support)
├── Start-CheapHDR.bat        <-- 1-Click console launch (shows FPS & status)
├── Start-CheapHDR-Hidden.vbs <-- 1-Click silent launch (runs hidden in background)
├── Add-To-Startup.bat        <-- 1-Click auto-boot on PC startup
├── Remove-From-Startup.bat   <-- 1-Click remove from PC startup
├── Stop-CheapHDR.bat         <-- 1-Click stop to kill all processes
├── build.bat                 <-- 1-Click compiler using Windows' built-in csc.exe
├── README.md
├── LICENSE
└── .gitignore
