# 📱 Samsung OneUI BL Swap & Root Patcher (Automated)

This project automates the process of **swapping Bootloader (BL) files** between Samsung OneUI 7 and OneUI 8 firmware to ensure compatibility, and automatically patches the **AP file with Magisk 26.3** for rooting. All processing is done securely in the cloud using **GitHub Actions**.

> ⚠️ **DISCLAIMER & WARNING**  
> **Use at your own risk.** This tool is for **educational purposes only**.  
> - Flashing modified firmware can **brick your device**, void your warranty, or cause security vulnerabilities.  
> - The user assumes **full responsibility** for any damage caused to their hardware or software.  
> - This repository **does not host** any firmware files. Users must provide their own direct download links.  
> - Ensure both firmware versions have the **same Bit version** (e.g., Bit 5 to Bit 5). Mismatched bits will hard-brick your device.

---

## 🚀 Features

- ✅ **Automated BL Swap:** Replaces `abl.elf.lz4` in OneUI 8 BL with the OneUI 7 version automatically.
- ✅ **Magisk 26.3 Integration:** Automatically patches the AP file (`boot.img` or `init_boot.img`) with Magisk 26.3.
- ✅ **Cloud Processing:** No need for a powerful local PC; everything runs on GitHub's servers.
- ✅ **Direct Artifact Download:** Get your ready-to-flash `.tar` files directly from the Actions tab.

---

## ⚠️ Critical Limitations: GitHub Actions Storage

**Please Read Before Running:**
GitHub Actions runners have a strict **storage limit of roughly 5GB to 14GB** (depending on the runner image), but the **artifact upload limit is strictly 500MB per file** (or 10GB total per workflow run for free accounts, but individual file limits often apply depending on current policies).

1.  **Firmware Size:** Samsung firmware files are often **4GB - 6GB**.
    - If the combined size of the downloaded ZIPs + extracted files exceeds the runner's disk space, the workflow will **fail**.
    - If the resulting `Patched_AP.tar` is larger than **500MB**, you might face issues uploading it as an artifact (though recent updates allow up to 10GB total, single large files can sometimes be tricky).
2.  **Timeout:** The workflow has a maximum runtime of **6 hours**. Large downloads might cause a timeout.
3.  **Solution for Large Files:** If your firmware is too large, it is recommended to use this workflow **only for the BL Swap** and patch the AP file manually on your phone using the Magisk app.

---

## 🛠️ Prerequisites

1.  A **GitHub Account**.
2.  **Direct Download Links** for:
    - OneUI 7 Firmware (`.zip` format).
    - OneUI 8 Firmware (`.zip` format).
    - *Note: Links must be direct (ending in .zip), not HTML pages. Use "Copy Link Address" from SamFw or similar sites.*
3.  Both firmwares must have the **same Bit version** (check the 5th character in the version string, e.g., `S928BXXU5AXHA` -> **5**).

---

## 📖 How to Use

### Step 1: Setup
1.  Click **"Use this template"** or fork this repository to your account.2.  Go to the **Actions** tab in your repository.
3.  If prompted, click **"I understand my workflows, go ahead and enable them"**.

### Step 2: Run the Workflow
1.  On the left sidebar, select **"Samsung OneUI BL Swap & Root Patcher (Magisk 26.3)"**.
2.  Click the **"Run workflow"** button.
3.  Fill in the required inputs:
    - **OneUI 7 Firmware Direct Download Link**: Paste the direct `.zip` link.
    - **OneUI 8 Firmware Direct Download Link**: Paste the direct `.zip` link.
    - **Magisk Version**: Pre-set to `26.3`.
4.  Click **"Run workflow"**.

### Step 3: Download Results
1.  Wait for the job to turn **Green (Success)**. This may take 10-20 minutes depending on file sizes.
2.  Scroll down to the **"Artifacts"** section.
3.  Download `Samsung-Patched-Firmware-Magisk26.3.zip`.
4.  Extract the zip file. You will find:
    - `Patched_BL.tar`
    - `Patched_AP.tar`

---

## 💻 Flashing Instructions (Odin)

1.  Download **Odin3** on your Windows PC.
2.  Boot your Samsung device into **Download Mode**.
3.  Load the files into Odin:
    - **BL Slot**: Select `Patched_BL.tar`.
    - **AP Slot**: Select `Patched_AP.tar` (If the file is too large for Odin or fails, patch the original AP manually on your phone).
    - **CP Slot**: Select the original `CP_*.tar.md5` from the OneUI 8 firmware.
    - **CSC Slot**: Select `HOME_CSC_*.tar.md5` (to keep data) or `CSC_*.tar.md5` (to wipe data).
4.  Click **Start** and wait for the process to finish.

> **Tip for Large AP Files:** If the automated AP patch fails due to size limits, download the *original* OneUI 8 AP file, transfer it to your phone, install **Magisk 26.3 APK**, and use "Select and Patch a File". Then flash that patched file via Odin.

---

## 🐛 Troubleshooting

| Issue | Solution |
| :--- | :--- |
| **Workflow Failed: Disk Full** | The firmware files are too large for the GitHub runner. Try finding smaller firmware variants or perform the AP patch manually. |
| **403 Forbidden Error** | Your download link expired. Generate a fresh direct link from SamFw and try again. |
| **Device Bootloop** | You likely mismatched the **Bit version**. Ensure OneUI 7 and OneUI 8 have the exact same Bit number. |
| **Magisk Patch Failed** | The `magiskboot` binary might be incompatible with the specific kernel compression. Manual patching on-device is recommended. |

---

## 📄 License
This project is licensed under the **MIT License**. However, the firmware files processed by this tool remain the property of **Samsung Electronics**.

---

## 🙏 Credits

- **Magisk**: [topjohnwu](https://github.com/topjohnwu/Magisk)
- **MagiskBoot Builds**: [HuskyDG](https://github.com/HuskyDG/magiskboot-builds)
- **Firmware Sources**: SamFw, SamMobile, etc.
