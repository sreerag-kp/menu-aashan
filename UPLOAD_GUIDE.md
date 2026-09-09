# Manual Guide: How to Build & Upload APK to MenuAashan Git Repository

This step-by-step guide explains how to manually build, replace, and upload the `MenuAashan-Owner-POS.apk` file to the [`menu-aashan`](https://github.com/sreerag-kp/menu-aashan.git) GitHub repository without changing the app version (`1.0.0+1`).

---

## Repository & File Locations

| Item | Local Path |
| :--- | :--- |
| **Flutter Project Root** | `c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\owner-app` |
| **Generated Release APK** | `c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\owner-app\build\app\outputs\flutter-apk\app-release.apk` |
| **Release Git Repo** | `c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\menu-aashan-release-repo` |
| **Target APK in Repo** | `c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\menu-aashan-release-repo\MenuAashan-Owner-POS.apk` |
| **GitHub Remote URL** | `https://github.com/sreerag-kp/menu-aashan.git` |

---

## Method 1: Using Terminal / PowerShell (Fastest & Direct)

### Step 1: Open Terminal in the `owner-app` folder
Open PowerShell and navigate to the owner app:
```powershell
cd c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\owner-app
```

### Step 2: Build the Release APK
Run the Flutter release build command:
```powershell
flutter build apk --release
```
> **Note on Versioning**: This automatically uses the version configured in `pubspec.yaml` (`version: 1.0.0+1`). Do not pass `--build-name` or `--build-number` flags to keep the version unchanged.
> Once complete, the APK will be generated at:
> `owner-app\build\app\outputs\flutter-apk\app-release.apk`

---

### Step 3: Copy the Built APK to the Release Repository
Run this command in PowerShell to copy and overwrite the APK in the release repository:
```powershell
Copy-Item -Path "c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\owner-app\build\app\outputs\flutter-apk\app-release.apk" -Destination "c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\menu-aashan-release-repo\MenuAashan-Owner-POS.apk" -Force
```

---

### Step 4: Commit & Push to GitHub
Navigate to the `menu-aashan-release-repo` folder and push:
```powershell
cd c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\menu-aashan-release-repo
git status
git add MenuAashan-Owner-POS.apk
git commit -m "release: update MenuAashan-Owner-POS.apk (v1.0.0+1)"
git push origin main
```

Your updated APK is now live on GitHub!

---

## Method 2: Using File Explorer & VS Code / Git GUI

1. **Build**: Run `flutter build apk --release` in your terminal.
2. **Find the APK**: Open Windows File Explorer (`Win + E`) and paste this into the address bar:
   ```
   c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\owner-app\build\app\outputs\flutter-apk\
   ```
3. **Copy**: Copy `app-release.apk`.
4. **Paste & Rename**: Navigate to:
   ```
   c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\menu-aashan-release-repo\
   ```
   Paste the file and replace the existing `MenuAashan-Owner-POS.apk` (or rename the pasted file to `MenuAashan-Owner-POS.apk`).
5. **Push with Source Control**:
   - In your IDE Source Control tab, you will see `MenuAashan-Owner-POS.apk` marked as modified.
   - Stage the file, enter a commit message like `release: update MenuAashan-Owner-POS.apk`, and click **Commit & Push**.

---

## Method 3: Upload Directly via GitHub Web Browser

If you ever need to upload the APK directly without using local git:

1. Build the APK locally (`flutter build apk --release`).
2. Open your web browser and go to:
   👉 **https://github.com/sreerag-kp/menu-aashan**
3. Click the **`Add file`** button near the top right of the file list, then select **`Upload files`**.
4. Drag and drop `app-release.apk` into the box, or click "choose your files" and select:
   `c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\owner-app\build\app\outputs\flutter-apk\app-release.apk`
5. Ensure the file name in the repo is `MenuAashan-Owner-POS.apk`.
6. At the bottom, write:
   - Commit title: `release: update MenuAashan-Owner-POS.apk`
7. Click the green **Commit changes** button.

---

## Method 4: Publishing as a GitHub Release (Best Practice for APK Downloads)

To provide users with a clean direct download badge on GitHub:

1. Go to: **https://github.com/sreerag-kp/menu-aashan/releases**
2. Click **Draft a new release**.
3. Under **Choose a tag**, enter: `v1.0.0` (or select the existing tag).
4. Release title: `MenuAashan Owner POS v1.0.0`
5. Description:
   ```markdown
   ### Highlights & Fixes
   - Gemini Vision AI menu scanner with 100% OCR precision
   - Smart model auto-switching across Gemini Flash Lite / 3.5 / 3.6
   - Multi-page batch scanning & portion variant detection
   - Cleaned in-app API key dialogs & updated secure proxy
   ```
6. Attach binaries: Drag and drop `owner-app\build\app\outputs\flutter-apk\app-release.apk` into the binary attachment box.
7. Click **Publish release**.

---

## Verification Checklist

- [ ] Version in `owner-app/pubspec.yaml` remains `1.0.0+1`.
- [ ] No API keys are visible in the app UI or stored unencrypted.
- [ ] Direct download link in `menu-aashan-release-repo/README.md` points to the latest APK.
- [ ] SHA-256 checksum can be generated via:
  ```powershell
  Get-FileHash -Path "c:\Users\sreer\.gemini\antigravity-ide\scratch\menu-platform\menu-aashan-release-repo\MenuAashan-Owner-POS.apk" -Algorithm SHA256
  ```
