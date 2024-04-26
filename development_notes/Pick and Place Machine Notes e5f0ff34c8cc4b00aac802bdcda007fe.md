# Pick and Place Machine Notes

Status: In Progress

### Development:

### Objectives:

- Determine whether or not the machine’s native file conversion is accurate enough for our purposes
- If the native file conversion isn’t accurate enough, find a way to more accurately convert the files to DPV format straight from Altium using a python scraper.
- Create a simplified guide for future students/shop employees to use the pick-and-place.
- (Possibly?) Create a PCB design guide/best practices for students designing for the pick-and-place.

### Machine Specs:

Manufacturer: Charm High

Model number: CHMT36VA

Principle manual author / videographer: Kimi Liu ([https://www.youtube.com/@KimiLiuCharmhigh](https://www.youtube.com/@KimiLiuCharmhigh))

Mrs. Liu’s videos are a great resource to the operation of these machines.

All the files we have: [https://www.dropbox.com/sh/oiarplve0a2dm02/AACaSeTSLxZ1Q307Eu2BxXO6a?dl=0](https://www.dropbox.com/sh/oiarplve0a2dm02/AACaSeTSLxZ1Q307Eu2BxXO6a?dl=0)

### Research

- Machine-performed CSV - DPV
    
    CSV file (input):
    
    [Pick Place for test2_0722.csv](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Pick_Place_for_test2_0722.csv)
    
    DPV file (output):
    
    [Pick Place for test2_1006.dpv](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Pick_Place_for_test2_1006.dpv)
    
    Discussion:
    
    Should be working fairly well. The package size is the designator in this specific instance. So, we should probably see if that can be changed.
    
- Existing Procedure:
    
    ### Standard Operating Procedure:
    
    1. **Prepare PCB (see below).**
    2. **Export PCB BOM (bill of materials) to CSV file (see below).**
    3. **Move CSV file to USB drive.**
    4. **Plug USB into machine.**
    5. **Convert CSV file to DPV file (see below).**
    6. **Load required reels according to DPV file (see below).**
    7. **Click “Run.”**
    
    ### How to Export PCB File as CSV (Altium):
    
    1. Having made sure the part numbers are associated with each of your parts, **navigate to “Reports” —> “Bill of Materials”**
    2. **Scroll to the left banner menu under “all columns.”**
    3. The machine needs eight very specific columns: **ID, designator, footprint, x coord, y coord, layer, angle, and comment. Make sure all these columns are checked.**
    4. **Next, make sure “Microsoft Excel Worksheet” is selected in “File Format” under “Export Options.”**
        
        ### Altium
        
        - Include the following in the CSV: Designator, Footprint, Mid X, Mid Y, Pad X, Pad Y, Layer, Rotation, Comment
    
    ### How to Export PCB File as CSV (Eagle):
    
    Disclaimer: yes, this is an excel file. Try not to think about it.
    
    1. **Navigate to “File” —> “Export” —> “BOM” (bill of materials)**
    2. **Click “CSV” under “Output Format”**
    3. **Click “Save”**
    
    A video representation of this process is found below:
    
    [https://www.youtube.com/watch?v=DfVLRfl_vwQ](https://www.youtube.com/watch?v=DfVLRfl_vwQ)
    
    ### How to Convert CSV file to DPV file:
    
    1. **On machine UI, navigate to “Files” —> “File Import.”**
    2. A UI should appear showing all files of a certain type. If the machine is only showing DPV files, **click the “CSV Files” button in the lower left corner.**
    3. **Select the “Import All” button in the lower right corner.** This should move all CSV files from the USB onto the machine itself. If need be, click the “OK” button to confirm you wish to overwrite any existing files.
    4. **Next, click the back arrow in the upper right corner.**
    5. **Navigate to “Convert File.”**
    6. **Click the file you wish to convert.**
    7. At this point, a menu will open and the machine will start displaying the info contained in your CSV file. HOWEVER, the machine won’t be able to do anything with it until you **click the “convert” button on the bottom of the screen.**
    8. **Click the “save” button on the bottom of the screen.**
    9. **Rename the file (if applicable).**
    10. **Click “OK” to save file.**
    
    A video representation of this process is found below:
    
    [https://www.youtube.com/watch?v=PBV9IBjbXTw](https://www.youtube.com/watch?v=PBV9IBjbXTw)
    
- Videos Showing Full Operation:
    
    [https://www.youtube.com/watch?v=WwKw0BdrqLs](https://www.youtube.com/watch?v=WwKw0BdrqLs)
    
    [https://www.youtube.com/watch?v=Bx-xghzDx4I](https://www.youtube.com/watch?v=Bx-xghzDx4I)
    
    Discussion: the second video shows the machine rotating and placing some parts very clear
    
    [https://www.youtube.com/watch?v=ZnSAb77M-P0](https://www.youtube.com/watch?v=ZnSAb77M-P0)
    
    Discussion: this video details how to add parts that are much larger than what reels can normally handle.
    
- Development Updates:
    - 8 May 2023:
        
        We are making steady progress!
        
        Milestones:
        
        - We got the machine moving!
        - It picks up stuff
        - It puts that stuff down
        - Previous development status: investigation (how does this work?)
        - Current development status: inspection (dialing in)
        - Analogy: it’s like the first time you make bread: the dough is chunky and you’re missing some ingredients, but you’ve got the idea that you’re in the process of aligning to.
        
        Goals:
        
        - Know how to dynamically change reel position
        - Manually declare bulk material
        - Switch between heads
    - 15 May 2023:
        
        Why we should switch to OpenPNP:
        
        - More support
            - Open source = community driven VS Charm High is *never* going to update their OEM support anyway
            - Most people in a 869 person-strong group meant only for our machine, the majority of people switch to OpenPNP
            - There are very VERY detailed guides for flashing this firmware online
        - Better UI
            - Camera, movement, and parts all in one screen VS all those things being mutually exclusive with OEM software
            - Native support for Eagle, Altium, and KiCAD  —> no DPV neccesary
        - Better accuracy:
            - No DPV conversion necessary
            - Eliminates phantom 90* offset bug
- OpenPnP exploration
    
    [https://github.com/openpnp/openpnp/wiki/CharmHigh-CHMT36VA](https://github.com/openpnp/openpnp/wiki/CharmHigh-CHMT36VA)
    
    - Notes on above:
        - In the OEM software, there is no command to rotate the nozzle
        - “[OpenPnP] does not reach the same level of performance as the original software, but there are many new features and functions in OpenPnP that are not available in the OEM software.”
        - It will take longer to configure the system + learning curve with OpenPnP
        - The re-flashing process is pretty intense, involves removing the base of the machine and cutting wires
    
    Thread on Sparkfun’s Google Group on our machine detailing the switch:
    
    [Desktop Pick and Place - Google Groups](https://groups.google.com/g/desktop-pick-and-place/c/qaoGrnM7pPw/m/-2k-5FBHCAAJ)
    
    Below is a link to SwitcherCamera, a plugin that enables OpenPnP to work with the CHMT36VA’s camera setup
    
    [SwitcherCamera](https://github.com/openpnp/openpnp/wiki/SwitcherCamera)
    
    Tips on installation:
    
    - [Google forum post](https://groups.google.com/g/desktop-pick-and-place/c/SeDQnsoxRA0/m/u5Dt1ZHFBAAJ)
    - [More recent Github article](https://github.com/openpnp/openpnp/wiki/CharmHigh-CHMT36VA)
    
    [More in-depth guide for our machine](https://mcuoneclipse.com/2020/05/03/retrofitting-a-charmhigh-chm-t36va-machine-with-openpnp/)
    
    Upon further inspection, the original GoFundMe page for OpenPNP had an example of how it worked on our exact machine. This leads me to believe that our machine will be one of the best supported PNP machines on the OpenPNP platform.
    
    [OpenPnP + CHMT36VA Driver First Demo](https://youtu.be/LWPcQJbo2mg)
    
    **Build Smoothieware:** [http://smoothieware.org/compiling-smoothie](http://smoothieware.org/compiling-smoothie)
    
    **FOR THE CHMT36VA USE:** [https://github.com/janm012012/Smoothieware-CHMT](https://github.com/janm012012/Smoothieware-CHMT)
    

### Flashing

- Creating better flashing documentation
    
    To take the front cover off:
    
    1. Unscrew the emergency button
    2. Tear off the front veneer / cover 
    3. Unscrew the now-revealed screws
    4. Lift the plate off
    
    [20230526_143953.mp4](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/20230526_143953.mp4)
    
    At this point, you’ll see the motherboard in all of its complexity. Right next to the CPU, there are four header pins labeled SWD. Directly to the right of the SWD pins is a UART connector (characterized by the GD, RX, TX, and VC markings). We use the GD as a ground later.
    
    The great markmaker has already characterized each of the SWD pins as shown in the lower right corner of the picture below. The rest of his masterful guide can be found [here](https://github.com/openpnp/openpnp/wiki/Charmhigh-modifications-for-OpenPnP).
    
    ![IMAG1221-20190916-141902825.jpg](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/IMAG1221-20190916-141902825.jpg)
    
    For description of the pins used, see [STLink-V3SET datasheet,](https://www.st.com/resource/en/user_manual/um2448-stlinkv3set-debuggerprogrammer-for-stm8-and-stm32-stmicroelectronics.pdf) section 8.2.2
    
    ![topdownheader.jpg](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/topdownheader.jpg)
    
    Note the spacing and placement of our wires here.
    
    ![IMG_7168.jpg](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/IMG_7168.jpg)
    
    Note: this is the output header bank we used.
    
    ![IMG_7174.jpg](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/IMG_7174.jpg)
    
    Note: the black wire terminates on the ground pin of the UART we referenced earlier.
    
    Just to reiterate, this is the order of the pins on each part from left to right:
    
    PWD: orange, purple, white, red
    
    UART (GD): black
    
    Before we actually flash anything, though, we will need to . . . 
    
    - Update the firmware on the STM32 device.
        
        To accomplish this, do the following:
        
        1. Download and install STM32CubeProgrammer
        
        Note: those with Linux distributions might need to run the following in order to establish stable communication to their reprogrammer
        
        ```bash
        #Install libusb 
        sudo apt-get install libusb-1.0-0  #For debian distributions
        
        #Get udev rules from the STMCube
        cd <your STM32CubeProgrammer install directory>/Drivers/rules
        sudo cp *.* /etc/udev/rules.d/
        
        #reload udev rules
        sudo udevadm control --reload-rules
        ```
        
        Credit: Alex Mantaut in [this Stack Overflow thread](https://stackoverflow.com/questions/68009635/st-link-error-on-stm32cubeprogrammer-problem-occurred-while-trying-to-connect). 
        
        1. Boot STM32CubeProgrammer
        2. Connect your reprogrammer
        3. Press the refresh icon. It is located at the top of the upper right hand corner of the screen in the blue banner menu next to the option “Serial number” 
        4. Press “Firmware upgrade.” This button is located immediately after the settings for your particular reprogrammer in the same banner menu as before.  
        5. Press “Open in update mode” on the popup menu.
        6. Press “Upgrade”
        7. DON’T TOUCH ANYTHING until the new firmware is flashed
        8. That’s it!
        
        Below is a video detailing what we just described.
        
        [STM32CubeProgrammerExplorationAllegro-2023-05-26_16.49.03.mp4](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/STM32CubeProgrammerExplorationAllegro-2023-05-26_16.49.03.mp4)
        
    - A simple guide to the STM32CubeProgrammer user interface
        
        Once you have your STM32’s firmware updated, you can go in and play around with features
        
        Open the sidebar by clicking on the three lines in the upper left corner
        
        ![does this work-2023-06-01_11.56.13.gif](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/does_this_work-2023-06-01_11.56.13.gif)
        
        Once you’ve expanded this menu, you can see a few options. 
        
        - Memory & file editing
            
            This screen is where you can configure your STM32 programmer and edit your .bin, .hex, or .elf files here.
            
        - Erasing & programming
            
            ![Screenshot from 2023-06-01 14-00-35.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Screenshot_from_2023-06-01_14-00-35.png)
            
            This is the erasing and programming screen. If and only if your programmer is connected to a target, then the upper right menu will be populated according to the data saved in the existing flash files. You can choose to erase a specific part or the entire flash memory bank.
            
            The upper left screen is where you can load your .bin, .hex, or .elf file. Once your file is loaded and your options are set, you can select “start program” to flash your new file to your target.
            
        - Option bytes
            
            This screen only appears if and only if you’re able to connect to your target. Once it loads, it will display a series of fields that all do one thing: protect or allow writing / erasing. In order for you to flash your target, all of these option bytes must be flipped to whatever setting allows the board to be written on.
            
        - MCU core, Serial Wire Viewer, Secure Programming
            
            We haven’t had a chance to look at these screens yet.
            
- Flashing log
    - 26 May 2023
        
        First experimented with the STM32. Discovered and wrote a workflow for updating its firmware.
        
    - 31 May 2023
        
        [First tried to flash device.] 
        
        Connected everything up. Checked and double checked everything was connected right.
        
        Experienced connection bugs with the machine. Kept getting an error saying to check the connection with the device
        
        After checking connections, we saw nothing wrong so we moved forward.
        
        We moved to the “Erasing & programming” screen and attempted to erase the machine’s flash, but found it to be write protected. So, we moved to the “Option bytes” menu and changed all settings that prevented us from erasing / writing to the board.
        
        After this, we were successfully able to erase the board. 
        
        We loaded our .hex file and attempted to reflash the board, but an error occurred. Connection to the STM32 programmer was lost halfway through the flashing and stopped prematurely. 
        
        Connection couldn’t be established after this.
        
    - 1 Jun 2023
        
        Picked up where we left off yesterday. For the better part of two hours, we tried — and failed — to reestablish connection to the device. 
        
        It is a possibility that we’ve bricked the motherboard. However, we have a post out on the forum serving as the world’s central hub for people doing what we’re doing asking for help.
        
    - 5 Jun 2023
        
        *Hindsight note: I did not disconnect the pumps here. - Brady*
        
        Got advice to disconnect the pumps. After disconnecting the power and then reconnecting (because I didn’t realize it wasn’t the pumps) I am able to connect for a moment before it breaks again. Current error: unable to get core ID
        
        ![Untitled](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Untitled.png)
        
    - 6 Jun 2023
        
        🎵Hallelujah it’s raining bits 🎵 
        
        After fully disconnecting the pumps so that they’re no longer on, we were able to easily connect to the board.
        
        Other notes to ensure it works:
        
        - Make sure the USB cable is high quality.
        - Use short jumper cables.
        - Pray.
        - Use a battery powered laptop as weird ground loops can cause problems connecting

### OpenPNP Development

- Setup
    
    One of the many great things about OpenPNP is that you can clone our exact settings, calibration, and feeder setup by simply copying and pasting our settings files (see glossary). We HIGHLY recommend that you do that first before proceeding.
    
    - Longform explanation of the development process.
        - 2023 Notes:
            - Progress to 08/18/2023
                - Calibration steps completed before beginning work:
                    
                    ![Untitled](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Untitled%201.png)
                    
                    **NOTE**: ****If you want to do anything that includes the secondary fiducial position, you will have to reopen and redo the secondary calibration fiducial position step because I knocked if off.
                    
                - Current issues:
                    - ~~For some reason when homing the Z axis goes to -4.74, it doesn’t home to 0 on the Z axis despite being set to do that.~~ Fixed by redoing N1 save Z setting
                    - The following error happens when attempting to do nozzle tip calibration:
                        - ~~“Nozzle tip calibration: too many vision misdetects. Check pipeline and threshold.~~” > solution: turned off nozzle tip calibration lololol. We may be able to reenable nozzle tip calibration later by assigning the up led actuator.
                    - After setting the worklight actuator, it sometimes flickers rapidly. This may be due to a conflict, e.g. one actuator is trying to turn it off and the other is trying to turn it on.
                    - ~~When doing “calibrate precise camear ↔ nozzle N2 offsets” it returns the error: can’t move Z to 45.858mm, higher than soft limit of 45mm. This is related to the ReferenceControllerAxis Z high soft limit. However, the tool shouldn’t be going all the way to 45 anyway.~~ Solved by disabling soft limit and recalibrating nozzle N2 offsets for the primary fiducial. UPDATE: after recalibrating again the same issue happened again. UPDATE: fixed by changing soft Z limit to 48mm
                    - 
                - Predicted future work:
                    - Work through remaining issues and solutions, do first job, write documentation
            - 09/26/2023 Script update
                
                After watching [this video](https://youtu.be/75hHtclelN4?si=2-9w07jr4W_m5_--), I decided adding in some of the author’s amazing scripts would be a good idea. They streamline aspects of actually getting boards loaded and filled out in OpenPNP a breeze.
                
                The scripts are meant to be used for large boards, but why not use them for all boards (where applicable)?
                
                A copy of his script repo can be found [here](https://github.com/psychogenic/psypnp) 
                
            - October
                - Starting 10/11
                    
                    I’ve been trying to figure out the difference between these two files:
                    
                    [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine.xml)
                    
                    [oldmachine.xml]
                    
                    [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine%201.xml)
                    
                    [loadedmachine.xml / newmachine.xml]
                    
                    It’s been very difficult. Both files are titanic in size and dense as titanium.
                    
                    The first machine is the older version
                    
                    The second machine is the newer version (as far as I can tell)
                    
                    - Old Machine Characteristics:
                        - Has a “home” value within the soft limits
                        - Made earlier
                        - Has a mapped z axis
                        - Enabled dynamic safe z
                        - Feeder not present
                    - New Machine Characteristics:
                        - Home value hits the soft limits
                        - Made later
                        - Feeders present (but barebones)
                    - Diff file
                        
                        loadedmachine.xml = newmachine.xml
                        
                        [easiertoreaddifference.txt](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/easiertoreaddifference.txt)
                        
                    
                    **Analysis:**
                    
                    If I had to choose between either of the machine files, I’d go with the one that has a mapped z axis and dynamic safe Z enabled since both of those things will save us some headaches. The other machine file doesn’t look filled out at all besides that so it’s safe to say that oldmachine.xml is probably the way to go. 
                    
                    AH I stand corrected. oldmachine.xml was the one that *didn’t* have those things. My apologies for getting them mixed up.
                    
                    Wait . . . the soft limits persisted even when I switched machine.xml files
                    
                    They do persist! Odd . . . 
                    
                    I’ll move the dynamic safe z file back into the machine’s settings.
                    
                    **Important Update:**
                    
                    Okay. I remember why this has taken as long as it has. 
                    
                    I originally started this old/new/loaded machine.xml file goose chase because of this screen in the issues and solutions tab
                    
                    ![ohno.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/ohno.png)
                    
                    The second issue is a problem. We had already done this before. However, full control of this project switched hands almost immediately after that. I don’t think it was completed. This is a small issue mainly because we moved the marker we had used to denote the primary fiducial location because of how we thought we were done with calibrating the machine. That is an even larger problem since the primary fiducial and its location shouldn’t be messed with when you’re calibrating the machine. 
                    
                    What are my options here?:
                    
                    - Perform the entirety of the advanced calibration again
                    - Tape the marker back on the PCB we used to denote the primary fiducial, move it back *roughly* into position, then do the nozzle offset calibration.
                    
                    Oh hold on this might be a non-issue. There was a calibration issue that we ended up dismissing because certain curves didn’t converge. No . . . that wouldn’t be this otherwise it wouldn’t be visible (you can see I’ve left “Include Dismissed?” unchecked). 
                    
                    So it’s confirmed that this is an issue.
                    
                    How to we access the position of the primary calibration fiducial?
                    
                    Eureka! We can access it through the machine.xml file.
                    
                    ```xml
                    <calibration-primary-fiducial-location units="Millimeters" x="152.60892925550306" y="106.72961242248313" z="-12.496485280314811" rotation="0.0"/>
                    ```
                    
                    Great! How can we move the head to exactly that location? 
                    
                    Figured out a workaround! I put the fiducial location in the start location for the feeder 
                    
                    Turns out, we had set the z axis distance for the primary fiducial when we were using the old, broken head that had been smashed into its short location configuration. 
                    
                    Not the best, but as long we don’t have to calibrate again it should be fine. 
                    
                    If we ever *do* have to calibrate again, use this z axis value: 
                    
                    ```xml
                    z="-9.9"
                    ```
                    
                    In any case, I’ve updated the machine.xml file to match this one:
                    
                    [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine%202.xml)
                    
                - Starting 10/23
                    - Investigating machine.xml issues (again)
                        
                        It’s a new week and it’s good to come back to the machine
                        
                        In the last section, I noted how some of the settings “remained persistent.” That was a natural byproduct of the fact that when OpenPNP is open, it overwrites the machine.xml that’s loaded to match the settings currently uploaded. 
                        
                        So, basically, the settings I had set last week are null and void.
                        
                        Well, not completely null or void, just . . . incomplete.
                        
                        I’ll upload the old machine.xml file to OpenPNP and report.
                        
                        Ah okay. Even with OpenPNP off, I still got the same error. Interesting.
                        
                        I’ll revert back to the machine.xml file I made last week, then report back.
                        
                        Uh oh. 
                        
                        The machine.xml file I made last week didn’t . . . it didn’t keep any of the changes I made. Odd. Let me confirm that, real quick.
                        
                        Yup. ODD.
                        
                        Well, I’ve performed the offset calibration again . . . I hope I don’t have to do this every time. 
                        
                    
                    Okay. Sweet. Moving on.
                    
                    The next milestone is getting the feeders setup. 
                    
                    - Feeders setup
                        
                        I can do that by setting up the two feeders that’s closest to the up-looking camera, then copying the data for those feeders to the other slots.
                        
                        Or I could just move the same reel to each of the feeders. That might be what I end up having to do. Maybe.
                        
                        In any case, [this one thread in the OpenPNP Google group](https://groups.google.com/g/openpnp/c/N6IVhO_xbrw/m/6mbJlUsdCQAJ) will help immensely: 
                        
                        For starters, this picture originally posted by Vespaman and a follow-up comment by Mark Maker (the maker of OpenPNP) is vital: 
                        
                        ![vespaman's master plan.jpg](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/vespamans_master_plan.jpg)
                        
                        1 is the initial pick location. The upper-left hole is where the drag pin will go into and drag until the upper-right hole. 
                        
                        TL;DR: autosetup works well now ever since Vespaman worked with Mark.
                        
            - November
                - Starting 11/01
                    
                    Something struck me when I came to work on the machine today: I have an awful lot of actuator errors in the “Issues and solutions” tab.
                    
                    The base machine actuators are working fine, but the user-defined ones attached to the head of the machine aren’t. 
                    
                    [matt_the_baker_machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/matt_the_baker_machine.xml)
                    
                    [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine%203.xml)
                    
                    I looked at two examples of machine.xml files (see above) from other users and found two things: 
                    
                    1. Every actuator is defined like a variable with a declaration and a definition. 
                    2. The character name (“N1VAC”, for example) is defined by a “ACTxxxxxx” variable
                    3. That “ACTxxxx” variable is defined elsewhere. 
                    
                    With our variables, the character name is given a “ACTxxxx” variable, but is never defined. A completely random “ACTxxxx” variable is defined with the same comments linking it to where “N1VAC” should go, but nothing is defined. 
                    
                    Odd. The next time I’m here, I’ll copy over Matt The Baker’s actuators and see if that fixes things. 
                    
                - Starting 11/06
                    - Setting up feeders
                        
                        Okay. Suddenly the autocalibration feature for the feeders isn’t working anymore.
                        
                        I see this screen when I go to activate the autocalibration feature from the feeders tab (once I’ve selected a feeder I want to set up)
                        
                        ![feederoverride.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/feederoverride.png)
                        
                        I press “yes” and I see the following screen
                        
                        ![feederoverride2.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/feederoverride2.png)
                        
                        The error message that appears says the following: 
                        
                        > Feeder ReferencePushPullFeeder: Please set the Pick Location Z coordinate first, it is required to determine the true scale of the camera view for accurate computer vision.
                        > 
                        
                        I haven’t seen this before. A while ago, I worked with Brady and was able to get well past this screen. Computer vision kicks in at this point, then identifies two or three sprocket holes.
                        
                        I’m starting to get concerned about some configuration errors. Possibly.
                        
                        I captured the z location coordinate using the blue outlined in red below:
                        
                        ![feedercalibration3.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/feedercalibration3.png)
                        
                        That didn’t save, though. For some reason, whenever I try to “Auto-Setup with Camera at Pick Location” the z location is cleared back to 0. 
                        
                        The value it *should* be is -11.2000 but that doesn’t save. 
                        
                        Uh oh. Not only that, but the vacuum isn’t actually picking up any components.
                        
                        That’s . . . bad.
                        
                        What changed? I hate to harp on this again, but it might be a question of the machine.xml file
                        
                        I went to Matt The Baker’s machine.xml again he has a few lines that deal with this feeder that ALMOST worked. 
                        
                        ```xml
                        <feeder class="org.openpnp.machine.reference.feeder.ReferencePushPullFeeder" version="1.1" id="FDR16ce65822417e6e8" name="DragFeeder 18?" enabled="true" part-id="603-Dummy" retry-count="3" feed-retry-count="3" pick-retry-count="0" rotation-in-feeder="90.0" normalize-pick-location="true" snap-to-axis="true" used-as-template="false" feed-multiplier="1" feed-speed-push-2="1.0" feed-speed-push-3="1.0" feed-speed-push-end="0.5" feed-speed-pull-3="1.0" feed-speed-pull-2="1.0" feed-speed-pull-1="1.0" feed-speed-pull-0="1.0" included-push-1="false" included-push-2="false" included-push-3="true" included-push-end="true" included-multi-0="false" included-multi-1="false" included-multi-2="false" included-multi-3="false" included-multi-end="false" included-pull-0="false" included-pull-1="false" included-pull-2="false" included-pull-3="false" actuator-name="DRAGPIN" peel-off-actuator-name="PEELER" feed-count="2" ocr-font-name="" ocr-font-size-pt="7.0" ocr-wrong-part-action="None" ocr-discover-on-job-start="true" ocr-stop-after-wrong-part="false" calibration-count="2" calibration-tolerance-mm="1.95" sprocket-hole-tolerance-mm="0.6" row-location-tolerance-mm="4.0" row-Z-location-tolerance-mm="1.0" calibrate-max-passes="3" calibrate-tolerance-mm="0.3" calibrate-min-statistic="2" calibration-trigger="UntilConfident">
                                    <location units="Millimeters" x="59.735" y="310.276" z="-9.5" rotation="-0.35393532690100094"/>
                                    <hole-1-location units="Millimeters" x="57.768" y="313.788" z="0.0" rotation="0.0"/>
                                    <hole-2-location units="Millimeters" x="61.815" y="313.763" z="0.0" rotation="0.0"/>
                                    <feed-start-location units="Millimeters" x="57.856" y="313.663" z="0.0" rotation="0.0"/>
                                    <feed-mid-1-location units="Millimeters" x="0.0" y="0.0" z="0.0" rotation="0.0"/>
                                    <feed-mid-2-location units="Millimeters" x="0.0" y="0.0" z="0.0" rotation="0.0"/>
                                    <feed-mid-3-location units="Millimeters" x="62.056" y="313.663" z="0.0" rotation="0.0"/>
                                    <feed-end-location units="Millimeters" x="61.856" y="313.663" z="0.0" rotation="0.0"/>
                                    <part-pitch value="4.0" units="Millimeters"/>
                                    <feed-pitch value="4.0" units="Millimeters"/>
                                    <feed-speed-push-1>1.0</feed-speed-push-1>
                                    <pipeline>
                                       <stages>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.ImageCapture" name="0" enabled="true" default-light="true" settle-first="true" count="1"/>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.ImageWriteDebug" name="deb0" enabled="false" prefix="push_pull_" suffix=".png"/>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.BlurGaussian" name="1" enabled="false" kernel-size="5"/>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.AffineWarp" name="2" enabled="false" length-unit="Millimeters" x-0="0.0" y-0="0.0" x-1="0.0" y-1="0.0" x-2="0.0" y-2="0.0" scale="1.0" rectify="true" region-of-interest-property="regionOfInterest"/>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.ConvertColor" name="3" enabled="false" conversion="Bgr2Gray"/>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.SimpleOcr" name="OCR" enabled="false" alphabet="0123456789.-+_RCLDQYXJIVAFH%GMKkmuµnp" font-name="Liberation Mono" font-size-pt="7.0" font-max-pixel-size="20" auto-detect-size="false" threshold="0.75" draw-style="OverOriginalImage" debug="false"/>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.ImageRecall" name="5" enabled="false" image-stage-name="0"/>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.DetectCircularSymmetry" name="results" enabled="true" min-diameter="10" max-diameter="100" max-distance="100" search-width="0" search-height="0" max-target-count="10" min-symmetry="1.2" corr-symmetry="0.2" property-name="sprocketHole" outer-margin="0.2" inner-margin="0.2" sub-sampling="8" super-sampling="1" diagnostics="false" heat-map="false"/>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.ImageRecall" name="7" enabled="false" image-stage-name="0"/>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.DrawCircles" name="8" enabled="true" circles-stage-name="results" thickness="1">
                                             <color r="255" g="0" b="0" a="255"/>
                                          </cv-stage>
                                          <cv-stage class="org.openpnp.vision.pipeline.stages.ImageWriteDebug" name="deb1" enabled="false" prefix="push_pull_result_" suffix=".png"/>
                                       </stages>
                                    </pipeline>
                                    <ocr-region rectify="true">
                                       <upper-left-corner units="Millimeters" x="-2.029319392887599" y="0.8967272489601557" z="0.0" rotation="0.0"/>
                                       <upper-right-corner units="Millimeters" x="2.7763081264658562" y="0.821999978213476" z="0.0" rotation="0.0"/>
                                       <lower-left-corner units="Millimeters" x="-1.9795201439823817" y="-0.6476363464712236" z="0.0" rotation="0.0"/>
                                    </ocr-region>
                                    <precision-wanted value="0.1" units="Millimeters"/>
                                    <sum-of-errors value="0.169060714692873" units="Millimeters"/>
                                    <sum-of-error-squares value="0.014555631856539854" units="Millimeters"/>
                                 </feeder>
                        ```
                        
                        I paid specific attention to this line:
                        
                        ```xml
                        <location units="Millimeters" x="59.735" y="310.276" z="-9.5" rotation="-0.35393532690100094"/>
                        ```
                        
                        This is the general location of the feeder itself. Not necessarily the pick location, but I wanted to see if it was in a good spot. I inputted `x="59.735" y="310.276" z="-9.5”` in their respective fields.
                        
                        Then, something bad happened. 
                        
                        I tried to home the machine when it . . . stopped. The head reached the end pillar (closest to the pc) and it just . . . froze.
                        
                        ![feederoverride4.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/feederoverride4.png)
                        
                        I don’t know why I tried to catch the documentation up *as* the machine was frozen, but here we are. 
                        
                        Since I took so long, I ran into the above error which reads as follows: 
                        
                        > GcodeDriver timeout waiting for response to M114; get position
                        > 
                        
                        I then promptly came to my senses and turned off the machine.
                        
                        I tried turning the machine on again (without moving the head away from the front left pillar), and the exact same thing happened.
                        
                        I turned the machine off again, then moved the head further away from the pillar. I then turned the machine back on, and homed the device. 
                        
                        I’ve done that twice now and it’s working just fine. 
                        
                        I’m honestly at a loss as to the following:
                        
                        1. What changed so that the autocalibration isn’t working
                        2. Why the head froze
                        3. What to do about this
                        
                        I think we MIGHT need to go back to basics. Months ago, Brady and I tried to import the machine.xml file from another maker named Jan after the legendary Mark from Makr Zone suggested he do so.
                        
                        I have to go. So, I’ll (unfortunately) have to pick this up next week.
                        
                - Starting 11/13
                    
                    Going to try to upload Jan / C-Reigel / Matt The Baker’s machine.xml file.
                    
                    - Our current machine.xml file
                        
                        [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine%204.xml)
                        
                    - Tried using Matt The Baker’s machin.xml file and received this error
                    
                    ![Reading Error OpenPnP.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Reading_Error_OpenPnP.png)
                    
                    Going to ask in the Desktop Pick N’ Place Google Group for solutions.
                    
                    - Jan’s machine.xml file
                        - [https://github.com/janm012012/Smoothieware-CHMT/tree/chmt/machine.xml](https://github.com/janm012012/Smoothieware-CHMT/tree/chmt/machine.xml)
                - Starting 11/27
                    
                    Goals for this week:
                    
                    - Get our machine talking to the computer so we can run Jan’s machine.xml file
                    - Once we’ve done that, diagnose where we need to go from there
                    
                    Update:
                    
                    [Jan suggested we do the following:](https://groups.google.com/g/desktop-pick-and-place/c/OgCSCdeo67I)
                    
                    > Hi Nathaniel!
                    Please consider asking OpenPnP related questions in the OpenPnP group.
                    There are others running this machines successful for years that are
                    very happy to help you.
                    Your error message suggests, that the COM port on your computer is
                    different (or the serial link is broken). Please visit Machine Setup ->
                    Drivers -> GCodeAsyncDriver -> Configuration and find the Serial Port
                    setup at the end.
                    > 
                    > 
                    > Jan
                    > 
                    - We went to machine setup and configured the program like this:
                        - Machine setup > Drivers > GcodeAsyncDriver > Port: COM6
                        - Doing that, the computer got in touch with the machine quite nicely
                    
                    Once we got the machine turning on, we came to a few shocking realizations:
                    
                    1. Jan’s machine.xml file is bare-bones / blank.
                    2. Our cameras (even with our past setup) weren’t working
                    3. We don’t have a GitHub for this project
                    
                    What followed was a mad scramble to figure out why our cameras weren’t working like they should’ve been. 
                    
                    At first, we tried to switch around where our USBs were connected. That didn’t end up helping at all, so we switched to trying to set up our cameras again.
                    
                    We came to the realization again that using the standard, default OpenPNP cameras wouldn’t work since these default cameras need their own, dedicated USB cable / bus in order to send data to the computer. This was the entire reason we started using SwitcherCam to begin with!
                    
                    So, we ended up following [this](https://github.com/openpnp/openpnp/wiki/SwitcherCamera) guide on how to setup a switchercam. 
                    
                    Turns out the problem was with our base `OpenPnpCaptureCamer CaptureDevice` . We needed to go into `Device Settings` then change `Device` to `AV TO USB2.0` with a format of `720 x 480, 30 FPS, YUY2` .
                    
                    Success! Kind of. We’re back where we started.
                    
                    Tomorrow, I’ll get to work on starting a GitHub on this. I wonder if there’s a way we can link GitHub and Notion so we can continually commit this doc onto it . . . 
                    
                    - Future note from Nathaniel
                        
                        No. No there is not. Well . . . there *is*, but it just doesn’t work for us since our config files are so large. 
                        
                        Tyler and I spent WAY too long trying to get a repo set up. 
                        
                        TL;DR: you (the reader) will just have to deal with this huge paper trail. Sorry.
                        
                    
                    Sadly, the `114; get position` error described earlier is still happening. I might open a bug report on the repo housing OpenPNP itself and see if anyone has any idea what’s going on.
                    
                    Just to reiterate: we’ve switched back to our machine.xml file at this point
                    
        - 2024 Notes:
            - January
                
                After finals week and winter break, we finally have a chance to attack this machine. Let’s just get this guy done.
                
                - *SUMMARY OF WORK UP UNTIL THIS POINT:*
                    1. Brady Bowerbank and Nathaniel Horne (with Tyler Andersen coming in later) received the machine and did the following:
                        1. Confirmed the original software for the machine wasn’t adequate through experimentation.
                        2. Rewrote the firmware of the motherboard to work with Smoothieware
                        3. Began to setup OpenPNP and largely succeeded, but major functionalities (listed below) were left unresolved
                            1. Actuation of the dragpin
                            2. Setup of the feeders
                            3. Vacuum declaration / actuation 
                    2. Efforts to find the solution to these problems were frustrated
                    3. The team then tried to circumvent these challenges by finding a working machine.xml file from “the wild” but were largely told to start from scratch.
                    4. They did so, but these same problems still persist.
                    5. Projected efforts not consist (largely) of two possibilities: 
                        1. Continue to try to find a working, configured machine.xml file from someone running a machine like ours. 
                        2. Work out issues the hard way.
                    
                    Understandably, the team isn’t too . . . excited for option b.
                    
                - Starting 1/8
                    
                    It might be worth another stab at trying to find someone’s `machine.xml` file that is already working. 
                    
                    I’ll write up something real quick and run it by Tyler to see if it’s worth sending.
                    
                    - Draft message:
                        
                        Hello all and happy new year! 
                        
                        My colleagues and I have been trying to set up our Charmhigh chmt36va for a few months now and have been running into many issues. We’ve been trying our best to identify what the source of our issues are, but we’re running into more roadblocks than solutions. 
                        
                        We wanted to rule out the possibility of hardware-related issues by obtaining a copy of a working `machine.xml` file someone is currently using for their chmt36va. “Working” meaning you can populate a simple board using the machine’s stock feeders.
                        
                        This would also help us identify what our current `machine.xml` file is missing from a working copy and work backwards to get to that same place.
                        
                        If anyone would like to send us a copy of their `machine.xml` file for their chmt36va, that would be *very* much appreciated.
                        
                        Thank you, 
                        
                        Nathaniel and Tyler
                        
                        Our current `machine.xml` file is attached below.
                        
                        Here is some general background for our chmt36va:
                        
                        - The motherboard is running Smoothieware
                        - We’re using SwitcherCam to access both of our cameras. We wanted to avoid the complexity of removing and replacing both cameras.
                        - Other than that, we’re using completely OEM parts.
                    
                - Starting 1/15
                    - Fixing the camera-led feeder auto-setup bug
                        
                        Today held a massive breakthrough! We have had major difficulty in getting Open PNP to hold a z-value for the push pin action necessary to move the tape forward. To fix this, we hard coded the value -11.2 into the file itself. Additionally, we deleted two empty feeders that had been stored under the feeders tab. After doing so, the machine was able to recognize the two sprocket hole locations as well as the feeder hole location instead of flashing an error.
                        
                        Next steps include getting the machine to pick up components and move the tape forward using the push pin.
                        
                    - Getting the head to actually pick up components
                        
                        Another breakthrough! We were able to get the machine to actually pick up components!
                        
                        In the issues and solutions tab, we found an issue that said something along the lines of “add an ACTUATE_DOUBLE_COMMAND for nozzle 1”  
                        
                        Lines 686 - 707 of our `machine.xml` file read as follows: 
                        
                        ```jsx
                        <command type="ENABLE_COMMAND">
                           <text><![CDATA[; Default ENABLE_COMMAND]]></text>
                           <text><![CDATA[M809   		; Turn off VAC]]></text>
                           <text><![CDATA[M811		; Turn off BLOW]]></text>
                           <text><![CDATA[M801   		; Vacuum nozzle 1 off]]></text>
                           <text><![CDATA[M805   		; Vacuum nozzle 2 off]]></text>
                           <text><![CDATA[M813   		; Turn off BLOW]]></text>
                           <text><![CDATA[M814   		; Turn on DOWNLED]]></text>
                           <text><![CDATA[M820   		; Turn on BUZZER]]></text>
                           <text><![CDATA[G4P100 		; Wait 100 milliseconds]]></text>
                           <text><![CDATA[M821   		; Turn off BUZZER]]></text>
                           <text><![CDATA[M92 X31.93	; Set X steps/mm]]></text>
                           <text><![CDATA[M92 Y31.97	; Set Y steps/mm]]></text>
                        </command>
                        <command type="DISABLE_COMMAND">
                           <text><![CDATA[; Default DISABLE_COMMAND]]></text>
                           <text><![CDATA[M84    ; Disable all steppers]]></text>
                           <text><![CDATA[M815   ; Turn off DOWNLED]]></text>
                           <text><![CDATA[M811   ; Turn off UPLED]]></text>
                           <text><![CDATA[M813   ; Turn off BLOW]]></text>
                           <text><![CDATA[M809   ; Turn off VAC]]></text>
                           <text><![CDATA[M801   ; Vacuum nozzle 1 off]]></text>
                           <text><![CDATA[M805   ; Vacuum nozzle 2 off]]></text>
                        </command>
                        ```
                        
                        This particular section of the `machine.xml` file is dedicated to defining machine code. `M809` is the code to toggle the machine’s main vacuum, for example. 
                        
                        The fact that `Vacuum nozzle 1 off` was included in the `ENABLE_COMMAND` and `DISABLE_COMMAND` sections gave us a clue that this nozzle was really a boolean-related actuator instead of a double actuator like we had misled OpenPNP to believe. 
                        
                        That wasn’t reflected in our machine setup. So, we went into the `Machine Setup / Heads / ReferenceHead H1 / Actuators / Reference Actuator N1VAC` directory, scrolled all the way down to the `Value Type` under the `General` tab, and changed it to `Boolean` instead of `Double`.
                        
                    - Fixing headcam downward-facing LED light
                        
                        Following `Issues & Solutions`, we found that we didn’t set up the light for our down-facing camera (defined as `SwitcherCamera HeadCam` in our files)
                        
                        We turned to `machine.xml` for insight. 
                        
                        The file is split as to what machine code command is on and off for the light (if it exists)
                        
                        One section of the file says that `M814` and `M815` are on and off respectively while *another* section references it as `M822` and `M823` (I think)
                        
                        Since this is just a warning (and thus non-essential for the machine to function), then we might skip this for now.
                        
                        The fact that there are two codes for this is significant, though.
                        
                    - Identifying which sprocket holes the machine would normally use in operation
                        
                        We watched [this video](https://youtu.be/T_83L8rDSIg?t=90) on a large screen. If you do so, you’re able to identify that the machine uses the first two sprocket holes *after* the pincers at the pick location to advance the tape.
                        
                        We had originally assumed that the holes the dragpin would use were the two holes *before* the pincers. Another large breakthrough!
                        
                    - Figuring out what feeder to go with
                        
                        In the past when we had tried to set up a feeder, it ended up being overly complicated to the point of being ridiculous. 
                        
                        More than likely, I (Nathan) was just doing it wrong, but I wanted to check again that we were even headed in the right direction. 
                        
                        The only other option besides a `ReferencePushPullFeeder` (the kind we were trying to set up before) is a `ReferenceStripFeeder` . The latter are better suited for the trays on the front of the machine than the actual *feeders* on the side. We’ll still develop a SOP for the `ReferenceStripFeeder` , but right now our priority is the `ReferencePushPullFeeder` .
                        
                    - Setting up a `ReferencePushPullFeeder`
                        
                        [This is the setup guide on the OpenPNP Wiki](https://github.com/openpnp/openpnp/wiki/ReferencePushPullFeeder)
                        
                        We’ll be following this closely
                        
                - Starting 1/22
                    
                    
            - February
                - Happy Leap Day!!!
                    
                    ![Push Pull Motion Settings.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Push_Pull_Motion_Settings.png)
                    
                    (Here is the configuration of the push pull feeder)
                    
                    We’ve been fighting for quite a while with the drag pin. We have been able to fairly consistently advance the tape with the drag pin but it gets stuck (it doesn’t come back up) due to friction with the sprocket hole in the tape. 
                    
                    To overcome that issue, I set the midpoint 3 location to where we wanted to sprocket hole to end up and set the end location so that the drag pin would be moved slightly in the x-negative direction so that it could escape the sprocket hole. 
                    
                    One problem I’ve noticed is that the tape slackens a little bit after being advanced. Over the course of a few picks, the target hole eventually becomes partially covered by the metal piece that holds the tape in place. This leads to an error because the sprocket holes cannot be identified. 
                    
                    We need to figure out how to somehow compensate for that.
                    
                - March 1
                    
                    I managed to get the machine to advance the tape very consistently by continuing to empirically find the best values.
                    
                    ![Push Pull Motion Settings 2.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Push_Pull_Motion_Settings_2.png)
                    
                    With the remainder of my time today, I configured a second push pull feeder. I’ve detailed how to do so below ✅
                    
                    One problem I need to sort out is where the files are. The file location is a bit of a mess right now and I’m unable to locate and update the file location. That’s what I’ll figure out tomorrow.
                    
                    - Feeder Setup
                        
                        
                        To set up a new push pull feeder, go to the “Feeders” tab and click the green plus button.
                        
                        Select *ReferencePushPullFeeder* and press *Accept.*
                        
                        Under *General Settings*, select the part that the feeder will carry under the *Part* drop-down menu
                        
                        In the *configuration* tab, you’ll need to carefully set the x and y values for different positions of sprocket and feeder holes.
                        
                        You’ll see an *Auto-Setup with Camera at Pick Location* button.
                        
                        In all honesty, It’s way easier not to use the Auto-Setup and to input the values manually. (This option usually identifies the holes incorrectly)
                        
                        Here’s how to set it up manually…
                        
                        ### Pick Location:
                        
                        1. Position the camera over the pick location 
                        
                        ![Pick location.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Pick_location.png)
                        
                        1. Input the x and y values found in the the bottom right hand corner of the screen. (the z-value should be set at -11.200)
                            
                            ![Pick coords.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Pick_coords.png)
                            
                        2. Press apply in the bottom right hand corner
                        
                        ### Hole 1 Location:
                        
                        1. Use the same method as with the *pick location* to find and input the coordinates with this hole:
                            
                            ![Hole 1 Location.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Hole_1_Location.png)
                            
                        
                        ### Hole 2 Location:
                        
                        1. Repeat
                            
                            ![Hole 2 Location.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Hole_2_Location.png)
                            
                        
                        Once you’ve done this, you’re going to configure the *Push-Pull Motion* tab.
                        
                        Check that the *Feed Actuator* and *Auxiliary Actuator* are set to *DRAGPIN.*
                        
                        ### Y-values:
                        
                        1. In the *configuration* tab, copy the Y-value found in the *Hole 1* *Location*. 
                            
                            Switch to the *Push-Pull Motion* tab and paste this value into the y-values of *Start Location, Mid 3 Location,* and *End Location*
                            
                            Press Apply
                            
                        
                        ### X-values:
                        
                        1. In the *Configuration* tab, copy X-value found in the *Hole 1 Location*.
                            
                            Return to the *Push Pull Motion* tab and paste that value in the *Start Location*.
                            
                            Subtract 0.5 from that value (For example: if the value you pasted originally was 67.500, change it to 67.000)
                            
                            Press Apply
                            
                        2. Copy the value found in the *Start Location* X-value and paste it in the *Mid 3 Location*
                            
                            Add 4.5 to that value (For example: if the value you pasted originally was 67.000, change it to 71.500)
                            
                            Press Apply
                            
                        3. Copy the value found in the *Start Location* X-value and paste it in the *End Location*
                            
                            Add 4.0 to that value (For example: if the value you pasted originally was 67.000, change it to 71.000)
                            
                            Press Apply
                            
                        
                        ### Check boxes:
                        
                        1. Check the far left boxes associated with the *Mid 3 Location* and *End Location*
                            
                            Should look like this:
                            
                            ![Push Pull boxes.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Push_Pull_boxes.png)
                            
                            Press apply
                            
                        
                        Double check that the *Feed Actuator* and *Auxiliary Actuator* are set to *DRAGPIN*
                        
                        Lastly, to ensure that the nozzle tips are marked as compatible with the feeder and capable to picking the component, if such is the case, go to the *Packages* tab at the very top.
                        
                        Select the component and under the nozzle tips, check the boxes of the nozzles with which it is compatible.
                        
            - March
                - March 5
                    
                    Today was a bit of a setback. We tried advancing the tape with the drag pin and it did so inconsistently. We learned that the reason for this is that the x and y offsets (the location of the drag pin relative to the camera) were slightly off. 
                    
                    These settings can be found under *Machine Setup > Heads > Actuators > ReferenceActuator DRAGPIN* 
                    
                    We got really close to resolving that problem when we broke the drag pin. We needed to alter the x offset by 0.4 mm and the y offset by 0.1 mm. We aren’t entirely sure in which direction but we can definitely get that figured out quickly.
                    
                    We might be set back a couple of week due to that error, but we might be able to figure out a temporary solution while we wait on the part.
                    
                    Once we correct the offsets, we won’t have to compensate with the push pull motion settings. Each new feeder we set up will be able to be set up automatically and very quickly.
                    
            - April
                - Here is the vision pipeline for nozzle calibration
                
                <cv-pipeline>
                <stages>
                <cv-stage class="org.openpnp.vision.pipeline.stages.ImageCapture" name="image" enabled="true" default-light="true" settle-option="Settle" count="1"/>
                <cv-stage class="org.openpnp.vision.pipeline.stages.MaskCircle" name="mask" enabled="true" diameter="100" property-name="MaskCircle"/>
                <cv-stage class="org.openpnp.vision.pipeline.stages.DetectCircularSymmetry" name="cir" enabled="true" min-diameter="5" max-diameter="25" max-distance="250" search-width="0" search-height="0" max-target-count="1" min-symmetry="1.2" corr-symmetry="0.0" outer-margin="0.2" inner-margin="0.4" sub-sampling="8" super-sampling="1" symmetry-score="OverallVarianceVsRingVarianceSum" property-name="" diagnostics="true" heat-map="true"/>
                <cv-stage class="org.openpnp.vision.pipeline.stages.ConvertModelToKeyPoints" name="results" enabled="true" model-stage-name="cir"/>
                </stages>
                </cv-pipeline>
                
                You can copy and paste this into the pipeline.
                

- Current machine setting files
    
    [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine%205.xml)
    
    [packages.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/packages.xml)
    
    [parts.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/parts.xml)
    
    [vision-settings.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/vision-settings.xml)
    
- Demo Board and Related Changes
    - Demo board files
        
        [test_board.zip](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/test_board.zip)
        
    
    Okay. We’ve had to do the following in order to get the demo board working:
    
    - Getting pick and place machine files generated
        - Altium
            
            All we need to generate for OpenPNP to be happy is something called a “named CSV”
            
            1. Select the board you want to generate files for
            2. Select “Select File > New > Output Job File**”**
                
                ![Jobfile.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Jobfile.png)
                
            3. Right click on “Generates pick and place files” under “Assembly Outputs”
                
                ![Right click on jobfile.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Right_click_on_jobfile.png)
                
            4. Select “Configure…”
                
                ![Click on configure.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Click_on_configure.png)
                
            5. Do the following:
                
                ![Configure splash.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Configure_splash.png)
                
                1. Check the following columns under “All Columns” on the left banner:
                    1. Comment
                    2. Description
                    3. Designator
                    4. Footprint
                    5. Height(mil)
                    6. Layer
                    7. Pad-X(mil)
                    8. Pad-Y(mil)
                    9. Ref-X(mil)
                    10. Ref-Y(mil)
                    11. Rotation
                    12. Value
                2. Select the following under “Output Settings” in the lower left corner:
                    1. Check “Imperial” under “Units”
                    2. Select “,” under “Separator”
                3. Check “CSV” under “Formats” in the lower middle of the screen
                4. Press “OK”
            6. Open OpenPNP
            7. Click the green plus icon under “Boards”
            8. Navigate to the directory where you’ve stored your project files using the popup menu
            9. Select “Pick and place for [project_name]” and press “save”
                
                ![Add board file.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Add_board_file.png)
                
            10. Mark fiducials as fiducials using the drop down menu under the “part” column for each component
                
                ![Mark fiducials as fiducials.png](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Mark_fiducials_as_fiducials.png)
                
            11. [something for later]
        - KiCAD

### Deprecated files

- 10/19/2023 machine settings
    
    [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine%201.xml)
    
    [packages.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/packages%201.xml)
    
    [parts.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/parts%201.xml)
    
    [vision-settings.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/vision-settings%201.xml)
    
- 08/23/2023 machine settings
    
    [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine%206.xml)
    
    [packages.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/packages%202.xml)
    
    [parts.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/parts%202.xml)
    
    [vision-settings.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/vision-settings%202.xml)
    
- Pre 08/23/2023 machine settings
    - machine.xml
        - Previous versions
            - ~Late June
                
                [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine%207.xml)
                
            - 18 Jul. 2023
                
                [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine%208.xml)
                
            - 23 Aug. 2023
            - 26 Sep. 2023
                
                [machine.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/machine%209.xml)
                
- Named CSV
    
    [Pick Place for TestBoard.csv](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Pick_Place_for_TestBoard.csv)
    
- OpenPNP project file
    
    [OpenPNP_test_board.job.xml](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/OpenPNP_test_board.job.xml)
    

### Standard operating procedure

## TIPS:

- Turn on the machine before opening software.
- If you’re unable to delete a file
    - Go to C:\Program Files (x86)\CHJD\CHMT-36VA\files and manually delete it there.
- Only one user can have OpenPnP open on the computer at the same time. If another user has it open it will return a serial port error.
- THESE ARE GREAT FOR SOLVING ISSUES IN THE “Issues & Solutions” TAB!!!
    - [https://github.com/openpnp/openpnp/wiki/Setup-and-Calibration](https://github.com/openpnp/openpnp/wiki/Setup-and-Calibration)
    - Machine Setup > Drivers > GcodeAsyncDriver Gcode Driver > Gcode
- If complete shutdown neccesary —> shutdown / startup process
    1. Use “Task Manager” to forcibly stop OpenPNP
    2. Turn off the machine
    3. Turn on the machine
    4. Open OpenPNP
    5. Press the green “ON” button on the main screen of OpenPNP
- 

### Technical Glossary

Purpose: I reference many things in this guide. I shudder to think about what it’s like to read this document without having a reference to double-check my meaning. This glossary will be true to the best of my knowledge, but may contain errors and won’t be comprehensive.

- Safe Z
    
    Safe Z is the maximum height a component can be without smashing into other components on the machine itself. Our machine has a safe z of 0.9 cm. The limiting factor is the retracted length of the dragpin. 
    
- Soft Limits
    
    Every axis on the machine as a software-defined limit to their movements. This helps ensure that the hardware isn’t damaged when the machine moves. I recommend not changing them too drastically.
    
    These limits can be easily changed under “Machine Setup” / “Axes” / [name of the axis you want to change] / “Kinematic Settings” / Soft Limit [High / Low]
    
- What files does OpenPNP like when importing a board?
    
    That’s something magic about OpenPNP: it accepts boards from KiCAD, Eagle, and Altium. Just as long as you format it right, then it’ll accept the board’s information.
    
- Main U.I. Menus
    - “Job” Menu
        
        This is where you’ll import and interact with the files needed to tell the machine to actually populate your boards.
        
    - “Parts” Menu
        
        The information for all the parts you’ve ever imported into OpenPNP will be here. You can also create a new part definition based off of a current part definition.
        
    - “Packages” Menu
        
        This menu holds the information for the packages you’ve imported into OpenPNP.
        
    - “Vision” Menu
        
        This is where the specifics of the vision settings can be accessed. Edits can be made in this menu, but they should be made through specific issues in the “Issues & Solutions” tab. 
        
    - “Machine Setup” Menu
        
        When you’re setting up your machine, you’ll be spending most of your time here. 
        
        Once your machine is setup, though, use extreme caution while making changes in this menu. 
        
        Changes made here are immediately applied to the machine.xml file
        
    - “Issues & Solutions” Menu
        
        This menu saves more of your time than should be logically possible. It runs a check on the machine’s setting files and looks for issues and suggests solutions. Some of these issues will lead you to calibrate various parts of the machine when you’re first setting up the machine and point out errors that come up during normal operation. 
        
        Every issue that comes up has an associated page on the OpenPNP Wiki.
        
    - “Log” Menu
        
        This is where errors or changes in machine state will be printed. 
        
- Machine settings files
    - Machine.xml
        
        This is where most of the configuration details about the machine are stored. Mechanical and camera offsets, axes maps, feeder information, etc.
        
        Why does this file exist? If a machine’s machine.xml file is replaced with another, the settings from the other machine will be imported. 
        
        This allows people with the same machine to share configuration details. In our own research, we’ve used this system to make incremental changes on the machine, then share it with other technicians.
        
- Actuators
    
    These are aspects about the machine that can be turned off or on. Some examples include the work light, vacuums, and dragpin.
    
- Fiducial
    
    A fiducial is a location on a PCB or on the bed of the machine itself that has a known location. Using two or more fiducials, the machine is able to calibrate itself and account for variations in the board’s placement.
    
    There are fiducial “components” that you can add to a board from the ECAD software (Eagle, KiCAD, Altium, etc) of your choice. These are essentially circles or holes carved into the surface of the PCB itself. This type of fiducial is the most accurate as OpenPNP can simply snap to them using circle detection.
    
    Regular components can be used as fiducials as well. However, this isn’t as accurate. user error can pin the location of a resistor mils away from where it is actually located in the board’s schematic.
    
- Dragpin
    
    This is the pin that extends from the bottom of the machine to advance the tape. It is defined on a boolean actuator. When false, the dragpin is retracted. When true, the pin is extended.
    
- SwitcherCam
    
    Our machine uses a single USB port to let our PC access both cameras. Normally, a pick and place machine has a dedicated USB for each camera. SwitcherCam circumvents these issues. It allows us to access both cameras through a single USB cable. 
    
    Why go through the effort of installing this software? If we *had* upgraded our cameras to each have their own USB cable, then we would have needed to tear fundamental parts of the head assembly apart to replace the bottom-looking camera; same with the bed itself for the up-looking camera. This could have seriously affected the overall calibration of the machine.
    
- Tape / reels
    
    On the left of the machine, there are 29 spaces for reels of component-holding tape.
    
    While component-holding tape comes in different sizes, they’re standardized. Almost all fabs internationally use tape to deliver their components to their machines and / or workers. Tape is perfect for our purposes as it gives the machine a consistent pick location and orientation of the target part.
    
    Tape comes in multiple varieties. The largest and most expensive of these are tape reels. This allows thousands of 0603 resistors, for example, to be shipped to a client without them spilling everywhere. Another type is cut tape — ideal for small part quantities or for physically large and / or expensive components.
    

TO ADD:

### Weird Glitches

- knocking against the forward-most post, then complete machine shutdown (happens after homing when close to the origin post)
    
    

### Feeder Setup

To set up a new push pull feeder, go to the “Feeders” tab and click the green plus button.

Select *ReferencePushPullFeeder* and press *Accept.*

Under *General Settings*, select the part that the feeder will carry under the *Part* drop-down menu

In the *configuration* tab, you’ll need to carefully set the x and y values for different positions of sprocket and feeder holes.

You’ll see an *Auto-Setup with Camera at Pick Location* button.

In all honesty, It’s way easier not to use the Auto-Setup and to input the values manually. (This option usually identifies the holes incorrectly)

Here’s how to set it up manually…

### Pick Location:

1. Position the camera over the pick location 

![Pick location.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Pick_location.png)

1. Input the x and y values found in the the bottom right hand corner of the screen. (the z-value should be set at -11.200)
    
    ![Pick coords.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Pick_coords.png)
    
2. Press apply in the bottom right hand corner

### Hole 1 Location:

1. Use the same method as with the *pick location* to find and input the coordinates with this hole:
    
    ![Hole 1 Location.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Hole_1_Location.png)
    

### Hole 2 Location:

1. Repeat
    
    ![Hole 2 Location.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Hole_2_Location.png)
    

Once you’ve done this, you’re going to configure the *Push-Pull Motion* tab.

Check that the *Feed Actuator* and *Auxiliary Actuator* are set to *DRAGPIN.*

### Y-values:

1. In the *configuration* tab, copy the Y-value found in the *Hole 1* *Location*. 
    
    Switch to the *Push-Pull Motion* tab and paste this value into the y-values of *Start Location, Mid 3 Location,* and *End Location*
    
    Press Apply
    

### X-values:

1. In the *Configuration* tab, copy X-value found in the *Hole 1 Location*.
    
    Return to the *Push Pull Motion* tab and paste that value in the *Start Location*.
    
    Subtract 0.5 from that value (For example: if the value you pasted originally was 67.500, change it to 67.000)
    
    Press Apply
    
2. Copy the value found in the *Start Location* X-value and paste it in the *Mid 3 Location*
    
    Add 4.5 to that value (For example: if the value you pasted originally was 67.000, change it to 71.500)
    
    Press Apply
    
3. Copy the value found in the *Start Location* X-value and paste it in the *End Location*
    
    Add 4.0 to that value (For example: if the value you pasted originally was 67.000, change it to 71.000)
    
    Press Apply
    

### Check boxes:

1. Check the far left boxes associated with the *Mid 3 Location* and *End Location*
    
    Should look like this:
    
    ![Push Pull boxes.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Push_Pull_boxes.png)
    
    Press apply
    

Double check that the *Feed Actuator* and *Auxiliary Actuator* are set to *DRAGPIN*

Lastly, to ensure that the nozzle tips are marked as compatible with the feeder and capable to picking the component, if such is the case, go to the *Packages* tab at the very top.

Select the component and under the nozzle tips, check the boxes of the nozzles with which it is compatible.

## Running a Job Step by Step

- **Importing the File**
    - Download your file as a KiCAD.pos file
    - In OpenPNP under the *Job* tab press the green ‘*+’*  button.
    - Select *New Board* and choose your board (You should see your board name in the upper section and the lower section should be empty)
    - Assure that the coordinates of the board are all set to 0
    - Under *Machine Controls* located below Cameras select *Nozzle: N1 - 503 (Head: H1)* under the drop down
    - Jog the camera over to the board until the camera is positioned exactly over its origin
    - Press this button to save the location of the origin:
    
    ![Save Location.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Save_Location.png)
    
    - Assure that the x and y positions now contain values
    - To obtain the z position of the board, jog the nozzle over the board and carefully lower it using these controls until the nozzle barely touches the board.
        
        ![Z move.PNG](Pick%20and%20Place%20Machine%20Notes%20e5f0ff34c8cc4b00aac802bdcda007fe/Z_move.png)
        
    - You can find the z position of the nozzle in the bottom right hand corner of the screen
    - Insert this value into the Z value of the board
    - If you don’t see your component placements, do the following:
        - In the far upper left above the Camera select the *File* tab
        - Select *Import Board* and then select KiCAD.pos
        - Under options select *Assign Parts, Create Missing Parts,* and *Use only Value as PartId*
        - In the *TopFile(.pos)* bar select browse and open your file
        - If you have a bottom file, do the same in the *BottomFile(.pos) bar*
        - Select Import (You should see all your parts and their positions now)
    - Under the *Type* column of the *Placements* section, select *Fiducial* for each fiducial
    - Finally, if they aren’t already checked, select the boxes indicating that the board itself as well as the placements are enabled.

**Assigning Parts to Feeders**

- If you have not yet loaded the machine with the components for your board, do so now.
- Under the *Parts* tab, give each part its height and assign it to its corresponding package.
- Under the *Packages* tab, select each part and mark the nozzles it is compatible with. (fiducials don’t need to be marked as compatible with either nozzle)
- Under the *Feeders* tab you will find several preconfigured feeders (PLEASE DO NOT MESS WITH THESE). Select enabled under as many Push-Pull and Tray Feeders as you need.
- Under the *Configuration* tab and *General Settings* section of each feeder, select the part that is loaded in the machine at that location. (Again, touch nothing else)
- Finally select *Enabled* for each feeder being used

You job should now be ready to run. Press the play button to run the job