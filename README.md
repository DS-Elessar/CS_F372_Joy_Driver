# Driver For Using An Xbox Controller As An Alternative Mouse
This is a software project aimed at enabling users to utilize an Xbox controller as an alternative input device for controlling the mouse cursor on a computer. This project seeks to enhance accessibility and provide an alternative input method for differently abled individuals who may have difficulty using traditional mouse and keyboard setups due to physical limitations or personal preferences.

**Features:**
1. Xbox Controller Mapping: Develop a system to map the various buttons and joysticks on an Xbox controller to corresponding mouse movements and actions.
2. Cursor Control: Implement precise control over the mouse cursor using the Xbox controller's joysticks for bi-directional movement and fine adjustments.
3. Button Functions: Assign buttons on the Xbox controller for left-click, right-click, scroll, drag-and-drop, and other common mouse functions.
4. Customization Options: Provide users with the ability to customize button mappings and sensitivity settings to suit their individual preferences and needs.
5. Accessibility Features: Include accessibility features such as adjustable cursor speed, gesture-based controls, and compatibility with screen reader software.
6. User Interface: Develop a user-friendly interface for configuring and managing the Xbox controller settings, including visual feedback to aid in customization.
7. Platform Compatibility: Ensure compatibility with major operating systems including Windows, macOS, and Linux, providing a seamless experience across different platforms.
8. Performance Optimization: Optimize the driver for efficient resource utilization and minimal input lag to ensure a smooth and responsive user experience.
9. Documentation and Support: Provide comprehensive documentation and user guides to assist users in setting up and using the Xbox controller as a mouse, along with responsive customer support channels for assistance and troubleshooting.

**Goals:**
- Create a versatile and intuitive software solution that allows users to control their computers effectively using an Xbox controller.
- Enhance accessibility by providing an alternative input method for individuals with disabilities or special needs. 

**Implementation:**
- Developed the driver primarily in a programming language suited for system-level development(C).
- Utilized relevant APIs and libraries for interfacing with the Xbox controller and managing mouse input.
- Employed version control systems like Git for collaborative development and code management.
- Conducted thorough testing across different hardware configurations and operating systems to ensure compatibility and reliability.
- Released the driver under an open-source license, allowing for community contributions, feedback, and ongoing improvement.

By implementing the Xbox Controller Driver for Mouse Control, we aim to empower users with a flexible and accessible means of interacting with their computers, promoting inclusivity and usability for all.

**Prerequisites:**  jstest
```
sudo apt-get install jstest
```

Use jstest to find the joystick device file in /dev/input. Can be done by
```
jstest /dev/input/jsX
```
where X is the number of input joysticks. Find the appropriate one, and make changes in reader.c accordingly

**To setup the LKM:**
In the directory of the files, provide superuser privileges.
```
sudo su
```
and enter your password. Then:
```
make
```
```
gcc -o reader reader.c
```
```
gcc -o caller caller.c
```

Create a dummy character device file /dev/dummy for our Kernel-related operations. 
```
sudo mknod /dev/dummy c 95 0
```

**To install the LKM:**
In the same directory as the files
```
sudo insmod joy_driver.ko
```

This will install the LKM onto the kernel. To verify if the LKM has initialized properly, use: ```dmesg | tail -n 2```
This should give an output similar to:
```
[5958.146652] Initialize Driver!
[5958.146669] joy_driver registered Device number Major: 95, M
inor: 0
```

**To run the application files:**
Call in the following order to avoid errors
```
./reader
```
```
./caller
```

**To unload LKM:**
```
sudo rmmod joy_driver.ko
```

**To clean files made during .ko generation:**
```
make clean
```
