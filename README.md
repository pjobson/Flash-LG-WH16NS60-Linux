# Flash LG WH16NS60 with Linux

## Notice

***Flashing your drive can permanently mess it up.***

## Reference

This is abstracted from these guides: 

* https://forum.makemkv.com/forum/viewtopic.php?f=16&t=19634
* https://forum.makemkv.com/forum/viewtopic.php?f=16&t=19928

## MakeMKV

Download & install MakeMKV: https://forum.makemkv.com/forum/viewtopic.php?t=224

Register it or use the Beta Key.

## Buy

Buy a LG WH16NS60

## Check Firmware

Check firmware, your drive is usually `/dev/sr0` unless you have multiple optical drives.

    makemkvcon f -d /dev/sr0 --info
    
Should show the drive information including:

    8003:Firmware version
    :1.00

If the 1.00 is greater than 1.03, you'll need to downgrade to 1.02.

## Download

Download the patched 1.03 firmware.

[HL-DT-ST-BD-RE_WH16NS60-1.03-NM00600-212005081010.zip](https://gist.github.com/pjobson/678e0350506419bab355d7b4392d4104/raw/ddaf392cb8c725da85e4359129e6a4df07ca2dc4/HL-DT-ST-BD-RE_WH16NS60-1.03-NM00600-212005081010.zip)

For downgrading download the 1.02 firmware.

[HL-DT-ST-BD-RE_WH16NS60-1.02-NM00100-211810291936.zip](https://gist.github.com/pjobson/678e0350506419bab355d7b4392d4104/raw/ddaf392cb8c725da85e4359129e6a4df07ca2dc4/HL-DT-ST-BD-RE_WH16NS60-1.02-NM00100-211810291936.zip)

## Back-Up!

Back-up your firmware.

    makemkvcon f -d /dev/sr0 dump auto

Note the `dump_full_HL-DT-ST_BD-RE__WH16NS60_1.00_211704251756_M63IBOA5100.zip` file in the repo is from my personal drive, it is only there as an archive for me, I do not recommend anyone using it.

## Get SDF File

Your SDF files are in your `_private_data.tar` file.

    tar -xf ~/.MakeMKV/_private_data.tar --wildcards --no-anchored 'sdf*'
    ls sdf*

Should show one or more `sdf_########.bin` files, take note of the one with the largest number.

Mine for example is `sdf_0000007e.bin`.

    sdf_0000007c.bin
    sdf_0000007d.bin
    sdf_0000007e.bin

## Flash

### Downgrade (optional)

    sudo makemkvcon f -d /dev/sr0 -f sdf_0000007e.bin rawflash main -i HL-DT-ST-BD-RE_WH16NS60-1.02-NM00100-211810291936.bin

Should return:

    Reading input file RE_WH16NS60-1.02-NM00100-211810291936.bin
    Flashing flags = 0x0 : 0 0 0 0 : ---- ---- ---- ----
    Current Drive ID: HL-DT-ST_BD-RE__WH16NS60_1.04_211704251756_M63IBOA5100
    Ready to write drive flash memory.
    Type "yes" to continue, "no" to abort
    
    Operation started: Sending flash image to drive
     100% Operation finished
    Operation started: Programming flash
     100% Operation finished
    Done successfully

Power off then restart.

### Verify

    makemkvcon f -d /dev/sr0 --info

Should show the 1.02 firmware.

    8003:Firmware version
    :1.02

### Upgrade

    sudo makemkvcon f -d /dev/sr0 -f sdf_0000007e.bin rawflash main -i HL-DT-ST-BD-RE_WH16NS60-1.03-NM00600-212005081010.bin

Should return:

    Reading input file HL-DT-ST-BD-RE_WH16NS60-1.03-NM00600-212005081010.bin
    Flashing flags = 0x0 : 0 0 0 0 : ---- ---- ---- ----
    Current Drive ID: HL-DT-ST_BD-RE__WH16NS60_1.00_211704251756_M63IBOA5100
    Ready to write drive flash memory.
    Type "yes" to continue, "no" to abort
    yes
    Operation started: Sending flash image to drive
     100% Operation finished
    Operation started: Programming flash
     100% Operation finished
    Done successfully

### Verify

    makemkvcon f -d /dev/sr0 --info

Should show the 1.02 firmware.

    8003:Firmware version
    :1.02


