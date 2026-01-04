# Presets

- Banner size has to be 256x128px and PNG format.
- Icon size has to be 48x48px and PNG format.
- Sound length has to be **LESS** than 3 seconds, e.g. 2,9 seconds. WAV format.
- Game must be in your chosen version's format (PBP or CHD).
- UNIQUE ID must be four characters. Only letters and numbers.

# Tutorial
This tutorial was possible thanks to [CrystalTikal](https://gbatemp.net/members/crystaltikal.702551/).

1. Download this repository by clicking the button below. Then extract it.

[<kbd> <br> Download <br> </kbd>](https://github.com/AverageJohtonian/Windows-PlayStation-3DS-forwarder/archive/refs/heads/main.zip)

2. Copy game's banner, icon and sound to the Resources folder.
3. Copy `retroarch.cfg` to Romfs folder, then open the copy with your favorite Notepad.
4. Replace all instances named `ROMNAME` with the long name of your game. It should look like this: `sdmc:/retroarch/forwarders/Resident Evil: Director's Cut`. Then save and close it.
5. Move your ROM to the Romfs folder, its name must be `game.chd`.
6. Go back to the Resources folder, click the directory bar, write "CMD" and hit Enter.

<img src="https://user-images.githubusercontent.com/2971735/81331899-90671d80-90a2-11ea-91bc-9bd33efea069.png">

## Important

**Edit everything between brackets**. Path should look like this:

`C:\Users\[Your user]\Downloads\Windows-PlayStation-3DS-forwarder-main\resources`

Delete the brackets, but don't quotation marks.

## CMD lines

### Template
``` shell
bannertool.exe makesmdh -s "[Short name]" -l "[Long name]" -p "[Publisher]" -i "[Path to icon]" -o icon.icn

bannertool.exe makebanner -i "[Path to banner]" -a "[Path to sound]" -o "banner.bnr"

3dstool.exe -cvtf romfs romfs.bin --romfs-dir "[Path to romfs]"

makerom.exe -f cia -o "[Output file, must end in .cia]" -rsf  "[Path to template.rsf]" -exefslogo -elf "[Path to retroarch_3ds.elf]" -romfs romfs.bin -icon icon.icn -banner banner.bnr -DAPP_UNIQUE_ID=[UNIQUE HEX ID] -DAPP_SYSTEM_MODE=64MB -DAPP_SYSTEM_MODE_EXT=124MB -DAPP_ENCRYPTED=false

```

### Usage example
``` sh
bannertool.exe makesmdh -s "Resident Evil" -l "Resident Evil: Director's Cut" -p "CAPCOM" -i "C:\Users\Myuser\Downloads\Windows-PlayStation-3DS-forwarder-main\resources\icon.png" -o icon.icn

bannertool.exe makebanner -i "C:\Users\Myuser\Downloads\Windows-PlayStation-3DS-forwarder-main\resources\banner.png" -a "C:\Users\Myuser\Downloads\Windows-PlayStation-3DS-forwarder-main\resources\sound.wav" -o "banner.bnr"

3dstool.exe -cvtf romfs romfs.bin --romfs-dir "C:\Users\Myuser\Downloads\Windows-PlayStation-3DS-forwarder-main\romfs"

makerom.exe -f cia -o "Resident Evil.cia" -rsf  "C:\Users\Myuser\Downloads\Windows-PlayStation-3DS-forwarder-main\resources\template.rsf" -exefslogo -elf "C:\Users\Myuser\Downloads\Windows-PlayStation-3DS-forwarder-main\resources\retroarch_3ds.elf" -romfs romfs.bin -icon icon.icn -banner banner.bnr -DAPP_UNIQUE_ID=REDC -DAPP_SYSTEM_MODE=64MB -DAPP_SYSTEM_MODE_EXT=124MB -DAPP_ENCRYPTED=false

```

## Final touches
Now that our CIA has been created, let's delete all the assets files we used:
- The icon, sound and banner you used.
- icon.icn
- banner.bnr
- romfs.bin
- game.chd or game.pbp

### Important
If you're gonna inject more games, you have to make sure your CIAs have different Title IDs and Product Codes, if not it will fuck up your previous game.
To check and change that, use the NSUI's Extract and edit feature.

Also, you have to edit every time the "ROMNAME" input. Yeah, this process can feel annoying, but it's the best we have for now.
