# Add DSTV Explora 2 to current config

Replacing a DSTV Single View SD with a new Explora 2 decoder

* Resources
  * [DSTV Self Service](https://selfservice.dstv.com/)
  * [Explora Manual](http://cdn.dstv.com/selfservice/documentation/DStv%20Explora%20Quick%20Guide.pdf)

* Current Configuration
    * Items
        * DSTV Explora
        * DSTV Single View SD
        * DSTV Switch 5-1
        * Dual LNB
        * Heartbeat cable between Explora and Single View SD
        * XtraView enabled on the account
    * Config
        * Explora in living room
        * Single View SD in bedroom
        * DSTV Multi-switch in living room
        * Cables from satellite dish terminate on switch in living room
        * Explora connected to multi-switch Explora output
        * Single View SD connected to a regular output
        * 2 rg6 coaxial cables from living room to bedroom
            * One cable connects DSTV Switch
            * Other cable connects to rf-in for heartbeat.
    * Explora is configured as primary device in Xtraview
* Going to need
  * DSTV Smart LNB - Model LMX501 - **Don't lose the small piece of paper with the userbands on it**
  * F-type Coaxial RG6 couplers
  * If your current installation is more than 5 years old, expect to need a new LNB holder. Pain to find.
  * Ladder and someone to spot you if the satellite dish is on your roof.

## Notes
* DSTV Switch 5-1 can only support 1 Explora (according to documentation). 
* Need a DSTV Smart LNB to connect multiple Exploras 

## Instructions
### Install new Smart LNB
1. Mark all your cables. I use colored tape.
    * Mark cables coming from satellite dish
    * Mark cables going to bedroom.
        * Mark the cable for the satellite connection
        * Mark the cable being used for the XtraView heartbeat
1. Disconnect DSTV Switch from your current configuration
1. Install DSTV Smart LNB on your satellite dish
    * Replace Dual LNB with DSTV Smart LNB - take note of the installation angle of the LNB.
    * Connect the cables from the Dual LNB to the unicable outputs of the Smart LNB.
    * Leave the terminators on the unused unicable outputs. Universal port does not need a terminator.
1. Reconnect your Explora
    * Connect cable from satellite dish (Smart LNB) directly to the Explora. No need for DSTV switch anymore.
1. Test. Explora should work just like before. No configuration necessary.

### Install new Explora
1. Use coupler to connect 2nd cable from LNB to satellite cable for bedroom.
1. Connect new Explora in bedroom.
    * Connect all cables.
        * Satellite cable from living room to unicable connection on Explora
        * Heartbeat cable to RF-In port.
        * Connect ethernet cable to ethernet port
        * Connect power.
1. Configure satelite bands - **Need the small piece of paper that came with the DSTV Smart LNB**
    * Select language
        * On Satellite Settings
            * Change band and index
                * Use the left arrow to erase the current frequency
                * Use the keypad to enter the digits
                    * User Band Tuner 1 Frequency - User band 3 from user bands list on paper.
                    * User Band Tuner 2 Frequency - User band 4
                    * User Band Tuner 3 Frequency - User band 5
                    * User Band Tuner Index - 3
                    * User Band Tuner 2 Index - 4
                    * User Band Tuner 3 Index - 5
    * Move down to *Scan* and click *OK* on remote.
### Configure XtraView on account
1. Login to your DSTV account.
1. Add device to your account.
1. Click on XtraView.
1. Remove current config.
1. Wait for it to update.
1. Create nex XtraView configuration.
    * Living room explora is probably set as the primary.
    * Select the new explora as the secondary.
1. Confirm configuration.
1. Everything should now work.
