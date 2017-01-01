---
title: "DSiWare Downgrade (App Injection)"
permalink: /dsiware-downgrade-(App-injection).html
---

If you are between versions 11.0.0 and 11.2.0, you can follow this guide to downgrade your NATIVE_FIRM using DSiWare.
{: .notice}

This takes advantage of an oversight which allows DSiWare titles to read and write anywhere in NAND.
{: .notice--info}

This is a currently working implementation of the "FIRM partitions known-plaintext" exploit detailed [here](https://www.3dbrew.org/wiki/3DS_System_Flaws).
{: .notice--info}

This exploit works by temporarily replacing the `movable.sed` encryption seed on your console with all `00`s, allowing you to import DSiWare that has been pre-injected with DSiWare hax and exported by another console that has the same encryption seed.
{: .notice--info}

The process of injecting the seed will temporarily format your console, but it will be back to normal once re-injected with your old encryption seed.
{: .notice--info}

#### What you need

* Prepare to purchase *(but do not buy until instructed to in the steps!)* or already own *(legitimately for your NNID)* one of the following pre-exploited DSiWare games on your 3DS
  + **Sudoku** (USA)
  + EUR Coming Soon
  + JPN Coming Soon
* An entrypoint from [Homebrew Launcher (SoundHax)](homebrew-launcher-(soundhax)) or [Homebrew Launcher (No Browser)](homebrew-launcher-(no-browser))
* [`import_seed.bin`]()
* The latest release of [sedManager](https://github.com/Plailect/sedManager/releases/latest)
* The latest release of [fasthax](https://github.com/nedwill/fasthax/releases/latest)
* The latest release of [3DSident](https://github.com/joel16/3DSident/releases/latest)
* The latest release of [dgTool](https://github.com/Plailect/dgTool/releases/latest)
* The pre-injected exploit DSiWare corresponding to the game you will purchase
  + **Sudoku** (USA): [`4B344445.bin`]()
  + EUR Coming Soon
  + JPN Coming Soon
* The NFIRM `.zip` corresponding to your device and version:
  + [New 3DS 11.0.0](magnet:?xt=urn:btih:2d13a5ea1570f911bd5c6423e0c30e51d548837a&dn=11.0.0%5Fto%5F10.4.0%5Fn3ds.zip&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=http%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fzer0day.ch%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969%2Fannounce&tr=http%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2710%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=http%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker1.wasabii.com.tw%3A6969%2Fannounce&tr=http%3A%2F%2Ftracker.baravik.org%3A6970%2Fannounce&tr=http%3A%2F%2Ftracker.tfile.me%2Fannounce&tr=udp%3A%2F%2Ftorrent.gresille.org%3A80%2Fannounce&tr=http%3A%2F%2Ftorrent.gresille.org%2Fannounce&tr=udp%3A%2F%2Ftracker.yoshi210.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.tiny-vps.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.filetracker.pl%3A8089%2Fannounce)
  + [Old 3DS 11.0.0](magnet:?xt=urn:btih:72393bbd99bc285db84a9cabf39d9b3200058d6a&dn=11.0.0%5Fto%5F10.4.0%5Fo3ds.zip&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=http%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fzer0day.ch%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969%2Fannounce&tr=http%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2710%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=http%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker1.wasabii.com.tw%3A6969%2Fannounce&tr=http%3A%2F%2Ftracker.baravik.org%3A6970%2Fannounce&tr=http%3A%2F%2Ftracker.tfile.me%2Fannounce&tr=udp%3A%2F%2Ftorrent.gresille.org%3A80%2Fannounce&tr=http%3A%2F%2Ftorrent.gresille.org%2Fannounce&tr=udp%3A%2F%2Ftracker.yoshi210.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.tiny-vps.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.filetracker.pl%3A8089%2Fannounce)     
  ~    
  + [New 3DS 11.1.0](magnet:?xt=urn:btih:d7d60c27c18f53bd8508a194656a465f6448bedf&dn=11.1.0%5Fto%5F10.4.0%5Fn3ds.zip&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=http%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fzer0day.ch%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969%2Fannounce&tr=http%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2710%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=http%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker1.wasabii.com.tw%3A6969%2Fannounce&tr=http%3A%2F%2Ftracker.baravik.org%3A6970%2Fannounce&tr=http%3A%2F%2Ftracker.tfile.me%2Fannounce&tr=udp%3A%2F%2Ftorrent.gresille.org%3A80%2Fannounce&tr=http%3A%2F%2Ftorrent.gresille.org%2Fannounce&tr=udp%3A%2F%2Ftracker.yoshi210.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.tiny-vps.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.filetracker.pl%3A8089%2Fannounce)     
  + [Old 3DS 11.1.0](magnet:?xt=urn:btih:0caf9a948a2d8bf23606d641f6628e2baeb983bb&dn=11.1.0%5Fto%5F10.4.0%5Fo3ds.zip&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=http%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fzer0day.ch%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969%2Fannounce&tr=http%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2710%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=http%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker1.wasabii.com.tw%3A6969%2Fannounce&tr=http%3A%2F%2Ftracker.baravik.org%3A6970%2Fannounce&tr=http%3A%2F%2Ftracker.tfile.me%2Fannounce&tr=udp%3A%2F%2Ftorrent.gresille.org%3A80%2Fannounce&tr=http%3A%2F%2Ftorrent.gresille.org%2Fannounce&tr=udp%3A%2F%2Ftracker.yoshi210.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.tiny-vps.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.filetracker.pl%3A8089%2Fannounce)     

#### Instructions

##### Section I - Prep Work

4. Copy and merge the `3ds` folder from the sedManager `.zip` to the root of your SD card
5. Copy and merge the `3ds` folder from the 3DSident `.zip` to your SD card
5. Copy `fasthax.3dsx` to the `/3ds/` folder on your SD card
6. Copy the dgTool `boot.nds` to the root of your SD card
1. Create a folder named `dgTool` on the root of your SD card if it does not already exist
3. Copy the contents of the NFIRM `.zip` to the `dgTool` folder on the root of your SD card
4. Reinsert your SD card into your 3DS

##### Section II - Export Seed

1. Get into the Homebrew Launcher using your entrypoint
2. Launch fasthax
3. Once it's done, press (Start) to exit
4. Launch sedManager
5. Press (Y) to export (backup) your current encryption seed
6. Press (B) to exit
7. Put your SD card in your computer without turning off your 3DS
8. Copy `export_seed.bin` from the root of your SD card to to a safe location on your computer
  + **You will need this file to restore your console after formatting it!**
  + Make backups in multiple locations
  + This backup can save you from data loss if anything goes wrong in the future
9. Copy the `import_seed.bin` you downloaded to the root of your SD card

##### Section III - Import Seed

This will temporarily format your console, but it will be back to normal once re-injected with your old encryption seed.
{: .notice--info}

1. Reinsert your SD card into your 3DS
4. Launch sedManager
5. Press (X) to import the custom encryption seed
6. Press (B) to exit
7. Press (Start) to open the homebrew launcher exit menu
9. Press (A) to exit
10. Complete the 3DS initial setup

##### Section IV - Export DSiWare

1. Purchase (or re-download using your NNID if you already own) one of the following pre-exploited DSiWare games installed on your 3DS
  + **Sudoku** (USA)
  + EUR Coming Soon
  + JPN Coming Soon
2. Go to System Settings, then "Data Management", then "DSiWare"
3. Copy the DSiWare game you purchased to the SD Card
4. Exit System Settings
5. Put your SD card in your computer
6. Navigate to the following folder on your SD card: `/Nintendo 3DS/ff084737d59d71f775c89e9728d26cd5/064100f8301059b630303030001b534d/Nintendo DSiWare/`
9. Copy the pre-injected exploit DSiWare `.bin` for your purchased game to the `Nintendo DSiWare` folder; overwrite the existing `.bin`
10. Reinsert your SD card into your 3DS

##### Section V - Import DSiWare

2. Go to System Settings, then "Data Management", then "DSiWare"
3. Copy the DSiWare game you purchased from the SD Card back to the System Memory
  + Overwrite the existing software when prompted
4. Exit System Settings

##### Section VI - Backing up NFIRM

3. Launch your DSiWare game
4. Launch dgTool by starting your DSiWare game
5. Select "Dump f0f1" to backup your NFIRM
  + This will take a while
6. Make note of the NFIRM backup's location
7. Exit dgTool
  + You may have to force power off by holding the power button
8. Put your SD card in your computer, then copy `F0F1_N3DS.bin` or `F0F1_O3DS.bin` (depending on your device) to a safe location
  + Make backups in multiple locations
  + This backup will save you from a brick if anything goes wrong in the future

##### Section VII - Flashing NFIRM

**Never downgrade with dgTool on a device that already has arm9loaderhax installed or you will BRICK!**
{: .notice--danger}

1. Launch your DSiWare game
4. Launch dgTool by starting your DSiWare game
3. Select "Downgrade FIRM to 10.4" and confirm to flash the 10.4.0 NFIRM bin
4. Exit dgTool
  + You may have to force power off by holding the power button
5. Reboot

##### Section VIII - Exploit Verification

2. Reinsert your SD card into your 3DS
3. Launch the homebrew launcher on using your entrypoint
4. Launch 3DSident
5. Verify that the following:
  + **Kernel version**: 2.50-11
  + **FIRM version**: 2.50-11
  + If either of these do not display the versions above, make sure you used the correct NFIRM zip and try flashing NFIRM again
5. Press any button to exit back to the Homebrew Launcher

##### Section IX - Restoring the System

1. Put your SD card in your computer without turning off your 3DS
2. Delete `import_seed.bin` from the root of your SD card
3. Rename `export_seed.bin` on the root of your SD card to `import_seed.bin`
4. Reinsert your SD card into your 3DS
5. Launch sedManager
5. Press (X) to import your original encryption seed
6. Press (B) to exit
7. Press (Start) to open the homebrew launcher exit menu
9. Press (A) to exit

Your version number will *not* have changed in the settings.
{: .notice--info}

Continue to [9.2.0 Downgrade](9.2.0-downgrade)
{: .notice--primary}
