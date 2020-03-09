# 1. INSTALLATION OF ECLIPSE IDE AND PLUGIN

## 1.1  Installing Eclipse IDE
- Download eclipse installer from [here] (https://www.eclipse.org/downloads/download.php?file=/oomph/epp/2019-12/R/eclipse-inst-linux64.tar.gz&mirror_id=105)
- unzip with 
    tar -xvf eclipse-inst-linux64.tar.gz
- navigate inside the unzipped folder and run ./eclipse-inst
- Select "Eclipse IDE for C/C++ Developers" and install it.
- Select "Launch"

----
    __After this point it is recommended to use a private or any other network connection as your office network could 
    cause errors in fetching the required libraries and other files.__
----   

## 1.2 Installing Oxygen Version of Eclipse  
   
- Select "Install New Software" from the "Help" pull-down menu. 
- Select "Oxygen - http://download.eclipse.org/releases/oxygen" from the "Work with:" pull-down menu.

- Expand the box next to "Linux Tools" and select the following

     C/C++ Remote (Over TCF/TE) Run/Debug Launcher
     TM Terminal
                            
- Expand the box next to "Mobile and Device Development" and select the following boxes:

     C/C++ Remote (Over TCF/TE) Run/Debug Launcher
     Remote System Explorer User Actions
     TM Terminal
     TCF Remote System Explorer add-in
     TCF Target Explorer
                            
- Expand the box next to "Programming Languages" and select the following box:

     C/C++ Development Tools SDK
                            

- Complete the installation by clicking through appropriate "Next" and "Finish" buttons. 

## 1.3 Installing the PLUGIN 

- Through the same window as above (#1.2), Click "Add..." in the "Work with:" area and in URL section paste "http://downloads.yoctoproject.org/releases/eclipse-plugin/2.6/oxygen"
    and can give any name in "Name" field
- Check the boxes next to the following:

     Yocto Project SDK Plug-in
     Yocto Project Documentation plug-in
                            
**Complete the remaining software installation steps and then restart the Eclipse IDE to finish the installation of the plug-in.** 


<br>


# 2. CONFIGURING THE OXYGEN ECLIPSE YOCTO PLUG-IN 

- Choose "Preferences" from the "Window" menu to display the Preferences Dialog.
- Click "Yocto Project SDK" to display the configuration screen. 

    - Select the toolchain type as "Standalone pre-built Toolchain" 
    - For specifying the location of toolchain, select the directory where you have extracted the Extensible Toolchain                      with the help of the .sh script i.e. the directory you specified in the below commands.

-----------------------------------------------------------------

     Poky (Yocto Project Reference Distro) SDK installer version 2.6.2
     =================================================================
     Enter target directory for SDK (default: /opt/poky/2.6.2): 
------------------------------------------------------------------

- Select the sysroot location, This location is where the root filesystem for the target hardware resides.
  for example :- /home/cdac/poky_armsdk_ext/tmp/sysroots/qemuarm
  ..see the images included in the screen_shots directory
- Select the target architecture 
- While selecting kernel image (the .bin file), you can select the image in the build directory of poky where you bitbaked. ex:-[/home/cdac/build/tmp/deploy/images/qemuarm/zImage.bin]      
        
<br>

# 3. CREATING AND DEBUGGING THE PROJECT

## 3.1 Creating the Project
 
   - Select "C Project" from the "File -> New" menu.
   - Expand "Yocto Project SDK Autotools Project".
   - Select "Hello World ANSI C Autotools Projects". This is an Autotools-based project based on a Yocto template.
   - Put a name in the "Project name:" field. Do not use hyphens as part of the name (e.g. "hello").
   - Click "Next".
   - Add appropriate information in the various fields.
   - Click "Finish".
   - If the "open perspective" prompt appears, click "Yes" so that you are in the C/C++ perspective. 
   - Right click on the project displaying on the left navigation plane and "Reconfigure Project"

   **NOTE:-** 
        In configure.ac replace "AC_OUTPUT([Makefile src/Makefile])" with AC_OUTPUT.
        Also add  "AC_CONFIG_FILES([Makefile	src/Makefile])" in configure.ac .


## 3.2 Building The project

   - To build the project select "Build All" from the "Project" menu. The console should update and you can note the cross-compiler you are using.                             

## 3.3 Starting QEMU in User-Space NFS Mode

   - To start the QEMU emulator from within Eclipse, follow these steps:

   - Expose and select "External Tools Configurations ..." from the "Run -> External Tools" menu.
    
   - Now, the Arguments Panel contains the commands for sourcing the environment script, and runqemu command with parameters as the path to the kernel image and the path to rootfile system of the image.
   - So here by default the path to root file system is given to sysroot directory which we declared at the Preference window while configuring.
   - Now change the rootfs path to the <name of rootfs>.ext4 file (present the same directory as image directory path).(Example of directory is included in screeshot directory)

-------------------------------------------------------------------------------------------------------------
    -e "source /home/cdac/poky_armsdk_ext/environment-setup-armv5e-poky-linux-gnueabi
    runqemu qemuarm /home/cdac/poky_armsdk_ext/tmp/deploy/images/qemuarm/zImage-qemuarm.bin <PATH TO ROOTFS>;
    bash"
------------------------------------------------------------------------------------------------------------

   Locate and select your image in the navigation panel to the left (e.g. qemu_i586-poky-linux).
   Click "Run" to launch QEMU. 


## 3.4 DEBUGGING LIVE OVER QEMU

   - Run -> Debug Configurations.. -> C/C++ Remote Application
   - Now select the local configuration (something with your project name with _gdb_<architectire>).
   - Change the connection to Remote Host (if present) or click on New, Choose connection type as SSH. write the IP of the image in place of host.
   - In Remote Absolute Path, enter the path in the image where you want to place your executable. ex:- /home/root/hello and click "debug"



# **References:**
1. (https://wiki.yoctoproject.org/wiki/TipsAndTricks/RunningEclipseAgainstBuiltImage)
2. (https://www.yoctoproject.org/docs/3.0.2/sdk-manual/sdk-manual.html)
3. (https://www.yoctoproject.org/docs/2.6/sdk-manual/sdk-manual.html#oxygen-configuring-the-eclipse-yocto-plug-in)
4. (https://elinux.org/images/4/4a/ELCE_Yocto_Plugin_2011_latest.pdf)
5. (https://mariapilot.noblogs.org/files/2017/03/w_pacb44-1.pdf)
6. Local screen_shots directory.
