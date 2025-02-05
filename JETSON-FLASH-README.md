# How to flash Jetson with latest Jetpack + OS

## Installing the SDKManager
1. Find the SDK deb files on the [downloads page of Nvidia](https://developer.nvidia.com/embedded/downloads)
2. Ensure that the current working directory on your terminal contains the `sdkmanager_*-*_amd64.deb`
3. Install using the following command:
   ```
   sudo apt install ./sdkmanager_*-*_amd64.deb 
   ```
## Jetson to Recovery mode
1. Visit [Jetson](https://developer.nvidia.com/embedded/learn/jetson-agx-orin-devkit-user-guide/developer_kit_layout.html) to know hardware layout
2. Ensure that the Jetson is powered `OFF`
3. Hold the recovery button and press the power button while holding the recovery button.
4. After a few seconds let go of the recovery button
5. Connect the Jetson to a `Host-PC` (Your PC) using the USB-C port (Port that supports flashing)

## Flashing the Jetson using SDK
1. Run the SDK using the following command and login to your Nvidia account:
   ```
   sdkmanager    
   ```
2. Once the Jetson is connected to the `HOST-PC` and is in recovery mode, you will notice a pop-up on the `sdkmanager` when it finds a device in recovery mode.

   <img src="https://github.com/user-attachments/assets/25b7c953-8c96-45bc-8b4d-ba0f4a95f9d1" height="400" width="auto">
   
3. Select the approporiate module and ensure that you uncheck the host machine on the setup and continue to the next step. (In the image below, the jetson already detects the board. If you see a message `could not detect a board`, this will fix it)

   <img src="https://github.com/user-attachments/assets/78641055-656c-4135-b765-ad5961a91d73" width="600" height="auto">

4. Select the relevant components and the folder location for the image and continue to the next step.
5. Set your username and password and click `Flash` to now flash the Jetson.
   
   <img src="https://github.com/user-attachments/assets/4db751ba-7477-4f3e-8edd-6ee53c3b0601" width="600" height="auto">

6. Once it is flashed, the latest Linux OS must be available on your jetson (Plug in a monitor to verify!)
7. Once the jetson reboots, hit install after entering the username and password you set in step 6.

   <img src="https://github.com/user-attachments/assets/bc22ca9d-ffc1-40d6-8a73-dae7323b459b" width="600" height="auto">

8. Once the installlation is done you are good to go!

