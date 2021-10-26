# Flash LG WH16NS60 with Linux

## Step

This is abstracted from these guides: 

* https://forum.makemkv.com/forum/viewtopic.php?f=16&t=19634
* https://forum.makemkv.com/forum/viewtopic.php?f=16&t=19928

Flashing your drive can permanently mess it up.

## Step

Download & install MakeMKV: https://forum.makemkv.com/forum/viewtopic.php?t=224

Register it or use the Beta Key.

## Step

Buy a LG WH16NS60

## Step

Check firmware, your drive is usually `/dev/sr0` unless you have multiple optical drives.

    makemkvcon f -d /dev/sr0 --info
    
Should show the drive information including:

    8003:Firmware version
    :1.00

If the 1.00 is greater than 1.03, you'll need to downgrade to 1.02.

## Step

Download the patched 1.03 firmware.

[HL-DT-ST-BD-RE_WH16NS60-1.03-NM00600-212005081010.zip](https://gist.github.com/pjobson/678e0350506419bab355d7b4392d4104/raw/ddaf392cb8c725da85e4359129e6a4df07ca2dc4/HL-DT-ST-BD-RE_WH16NS60-1.03-NM00600-212005081010.zip)

For downgrading download the 1.02 firmware.

[HL-DT-ST-BD-RE_WH16NS60-1.02-NM00100-211810291936.zip](https://gist.github.com/pjobson/678e0350506419bab355d7b4392d4104/raw/ddaf392cb8c725da85e4359129e6a4df07ca2dc4/HL-DT-ST-BD-RE_WH16NS60-1.02-NM00100-211810291936.zip)

## Step

Back-up your firmware.

    makemkvcon f -d /dev/sr0 dump auto

## Step

Flash the drive.

Downgrade

    makemkvcon f --all-yes -d /dev/sr0 -i ./HL-DT-ST-BD-RE_WH16NS60-1.02-NM00100-211810291936.bin
    
Power off then restart.

Check firmware as in Step 2.

Upgrade

    makemkvcon f --all-yes -d /dev/sr0 -i ./HL-DT-ST-BD-RE_WH16NS60-1.03-NM00600-212005081010

