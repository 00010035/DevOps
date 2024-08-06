## Installation Guide

### Step 1: No Need for Program Files

You don't need to install the program to `Program Files`. You can choose any location on your system for the installation.

### Step 2: Locate the Executable File

After the installation is complete, navigate to the installation directory. Here, you will find the executable file, for example, `HELLO.exe`.

### Step 3: Create a Batch File

To ensure the program runs with the correct settings, you'll need to create a batch file. Follow these instructions:

1. Open a text editor of your choice.
2. Copy and paste the following lines into the file:

    ```batch
    Set __COMPAT_LAYER=RunAsInvoker
    Start HELLO.exe
    ```

   Replace `HELLO.exe` with the name of your program's executable file if it is different.

3. Save the file with a `.bat` extension. For instance, you could name it `run_program.bat`.

### Step 4: Run the Program

Double-click the `.bat` file you just created to run your program. 

### Step 5: Create a Desktop Shortcut

For easy access, you can create a shortcut on your desktop:

1. Right-click the `.bat` file.
2. Select `Send to` > `Desktop (create shortcut)`.

You can now run the program directly from your desktop shortcut.

