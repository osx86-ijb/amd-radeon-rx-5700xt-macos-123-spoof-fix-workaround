
# Spoofing the AMD Radeon RX 5700 XT to the AMD Radeon Pro W5700X via DeviceProperties

This Repository contains the information necessary to spoof the AMD Radeon RX 5700 XT Navi 10 GPU to the AMD Radeon Pro W5700X GPU via adding in some XML property list formatted keys and strings in efforts of mitigating unwanted behaviors and performance degradation in macOS.
I have tested this on an XFX AMD Radeon RX 5700 XT Triple Dissipation, and can confirm that it works in both macOS Big Sur 11.6.5, and in macOS Monterey 12.3.


## Acknowledgements

 - [Feartech, for the original post](https://www.tonymacx86.com/members/feartech.877703/)
 - [aldaro, aka aldaro#0355 on Discord, for informing me about this.]()
 - [Everyone who cares, for being awesome.](https://www.youtube.com/watch?v=daBrCsDOOtk)


## Usage/Examples

```<key>DeviceProperties</key>
    <dict>
        <key>Add</key>
        <dict>
            <key>PciRoot(0x0)/Pci(0x3,0x1)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)</key>
            <dict>
                <key>@0,name</key>
                <string>ATY,Adder</string>
                <key>@1,name</key>
                <string>ATY,Adder</string>
                <key>@2,name</key>
                <string>ATY,Adder</string>
                <key>@3,name</key>
                <string>ATY,Adder</string>
                <key>device_type</key>
                <string>ATY,AdderParent</string>
                <key>AAPL00,DualLink</key>
                <data>AQAAAA==</data>
                <key>ATY,Card#</key>
                <string>102-D32200-00</string>
                <key>ATY,Copyright</key>
                <string>Copyright AMD Inc. All Rights Reserved. 2005-2019</string>
                <key>ATY,DeviceName</key>
                <string>W5700X</string>
                <key>ATY,EFIVersion</key>
                <string>01.01.190</string>
                <key>ATY,FamilyName</key>
                <string>Radeon Pro</string>
                <key>ATY,Rom#</key>
                <string>113-D3220E-190</string>
                <key>CAIL_EnableLBPWSupport</key>
                <integer>0</integer>
                <key>CAIL_EnableMaxPlayloadSizeSync</key>
                <integer>1</integer>
                <key>CFG_CAA</key>
                <integer>0</integer>
                <key>CFG_FB_LIMIT</key>
                <integer>0</integer>
                <key>CFG_FORCE_MAX_DPS</key>
                <integer>1</integer>
                <key>CFG_GEN_FLAGS</key>
                <integer>0</integer>
                <key>CFG_NO_MST</key>
                <integer>0</integer>
                <key>CFG_NVV</key>
                <integer>2</integer>
                <key>CFG_PAA</key>
                <integer>0</integer>
                <key>CFG_PULSE_INT</key>
                <integer>1</integer>
                <key>CFG_TPS1S</key>
                <integer>1</integer>
                <key>CFG_TRANS_WSRV</key>
                <integer>1</integer>
                <key>CFG_UFL_CHK</key>
                <integer>0</integer>
                <key>CFG_UFL_STP</key>
                <integer>0</integer>
                <key>CFG_USE_AGDC</key>
                <integer>1</integer>
                <key>CFG_USE_CP2</key>
                <integer>1</integer>
                <key>CFG_USE_CPSTATUS</key>
                <integer>1</integer>
                <key>CFG_USE_DPT</key>
                <integer>1</integer>
                <key>CFG_USE_FBC</key>
                <integer>0</integer>
                <key>CFG_USE_FBWRKLP</key>
                <integer>1</integer>
                <key>CFG_USE_FEDS</key>
                <integer>1</integer>
                <key>CFG_USE_LPT</key>
                <integer>1</integer>
                <key>CFG_USE_PSR</key>
                <integer>0</integer>
                <key>CFG_USE_SCANOUT</key>
                <integer>1</integer>
                <key>CFG_USE_SRRB</key>
                <integer>0</integer>
                <key>CFG_USE_STUTTER</key>
                <integer>1</integer>
                <key>CFG_USE_TCON</key>
                <integer>1</integer>
                <key>PP_DisableDIDT</key>
                <integer>1</integer>
                <key>PP_DisablePowerContainment</key>
                <integer>1</integer>
                <key>PP_DisableVoltageIsland</key>
                <integer>0</integer>
                <key>PP_FuzzyFanControl</key>
                <integer>1</integer>
                <key>hda-gfx</key>
                <string>onboard-1</string>
                <key>model</key>
                <string>Radeon Pro W5700X</string>
                <key>name</key>
                <string>ATY_GPU</string>
            </dict>
        </dict>
        <key>Delete</key>
        <dict/>
    </dict>
```


## Documentation

### In order to fully utilize this method, we're going to need to apply this to the appropriate section of our config.plist, under DeviceProperties, and then subsequently whatever path it is that your GPU is (this can be found by looking up such in IORegistryExplorer, or gfxutil).

Upon adding everything, make sure that you place the code in appropriately, IE: making accomodations or necessary changes at the end of the code by the Delete key to make sure that everything goes into your config.plist correctly.

Upon restarting your machine, you should now see in all locations referencing the GPU that it has been spoofed correctly as a Radeon Pro W5700X 8GB.

I've personally found that this has alleviated a lot of the issues I was facing, especially quite a few dealing with Electron.js based applications that would on occasion cause my machine to at random grind to a halt. There has been reports that it has fixed various other GPU related slowdowns as well.

I hope that you find this as useful as I have, and I will update this guide accordingly to explain things further in depth as time goes on and permits.
