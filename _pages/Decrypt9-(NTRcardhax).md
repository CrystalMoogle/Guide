---
title: "Decrypt9 (ntrcardhax)"
permalink: /decrypt9-(ntrcardhax).html
---

This is needed for KOR New 3DS because all other arm9 exploits (required to launch Decrypt9WIP) are for <=9.2.0, and KOR New 3DS shipped with 9.6.0.
{: .notice}

#### What you need

* An Acekard 2i flashcart *(must have bootrom v1.4.1; other versions can update/downgrade with [this](https://wiki.gbatemp.net/wiki/Updating_the_AK2i_Bootloader))*
* Two 3DS systems
  + **The source 3DS**: a 3DS capable of booting Decrypt9WIP (such as an arm9loaderhax 3DS)
  + **The target 3DS**: the 3DS on stock firmware *(10.3.0 or below)*
* The latest *build* of [Decrypt9WIP](images/Decrypt9WIP-20161231-013928.zip)
* The latest release of [fasthax](https://github.com/nedwill/fasthax/releases/latest)
* The latest release of [ntrcardhax](https://github.com/d3m3vilurr/ntrcardhax/releases/latest)

#### Instructions

##### Section I - Prep work

1. Create a folder named `files9` on the root of **the target 3DS**'s SD card if it does not already exist
2. Copy `Decrypt9WIP.bin` from the Decrypt9WIP `.zip` to the root of **the target 3DS**'s SD card and rename `Decrypt9WIP.bin` to `load.bin`
3. Copy and merge the `3ds` folder from the fasthax `.zip` to the root of **the target 3DS**'s SD card
4. Copy *the contents of* the ntrcardhax `.zip` to the `/3ds/` folder on **the target 3DS**'s SD card
4. Ensure **the source 3DS** is using the latest *build* (not release) of Decrypt9WIP (linked above)
  + Older versions will not have the AK2i options
  + If **the source 3DS** is an arm9loaderhax Luma3DS, you can do this by copying `Decrypt9WIP.bin` from the Decrypt9WIP `.zip` to the `/luma/payloads/` folder on **the source 3DS**'s SD card and rename `Decrypt9WIP.bin` to `x_Decrypt9WIP.bin`
5. Reinsert each SD card back into their corresponding 3DS

##### Section II - Flashing AK2i

For as long as your AK2i has been flashed with ntrcardhax, it will be unable to act as a standard flashcart.
{: .notice--info}

This process will dump a copy of your original AK2i bootrom to a file named `ak2i_flash.bin` on the root of **the source 3DS**'s SD card to allow it to be restored later.
{: .notice--info}

1. Put your Acekard 2i into **the source 3DS**
2. Launch Decrypt9WIP on **the source 3DS**
3. Go to "NDS Flashcart Options"
4. Select "Auto NTRCARDHAX to AK2i"
5. Wait for it to finish flashing your AK2i
6. Press (Start) to reboot

##### Section III - ntrcardhax

The AK2i can be safely removed from **the target 3DS** *after* Decrypt9WIP loads.
{: .notice--info}

1. Get into the Homebrew Launcher on **the target 3DS**
3. Launch fasthax
3. Once it's done, press (Start) to exit
4. Launch ntrcardhax_arm11
5. Put your flashed Acekard 2i into **the target 3DS**
6. Decrypt9WIP should load

##### Section IV - Restoring AK2i

This section is optional. It is only needed if you want to restore your AK2i to be a regular flashcart once more.
{: .notice--info}

1. Put your Acekard 2i into **the source 3DS**
2. Launch Decrypt9WIP on **the source 3DS**
3. Go to "NDS Flashcart Options"
4. Select "Restore AK2i bootrom"
5. Wait for it to finish restoring your AK2i
6. Press (Start) to reboot

Continue to [2.1.0 ctrtransfer](2.1.0-ctrtransfer).
{: .notice--primary}
