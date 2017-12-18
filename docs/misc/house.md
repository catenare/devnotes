# Non-tech related notes
* Sony KDL-40EX520
    * *No applicable update found* error with Mac OS X
        * [Updating Bravia firmware assistance](https://community.sony.co.uk/t5/other-tvs/updating-your-bravia-firmware-assistance/m-p/616370#M3143)
        ```
        Clem_Dye
        January 2013
        Re: Updating your BRAVIA firmware assistance.
        What system did you use to prepare the USB stick? The filesystem needs to be FAT32, the update needs to be placed on the drive as per instructions and it should work. However, if you prepared the USB stick on a Mac then you need to strip-off any extended attributes from the update using the xattr command. When these attributes are present the update will fail the file checksum routine used by the TV and will be ignored.
        Clem
        ```
