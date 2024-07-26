# Pomodoro on WSL

This guide will walk you through setting up a Pomodoro timer script using Windows Subsystem for Linux (WSL) on your Windows 11 system.

## Install Windows Subsystem for Linux (WSL)

WSL allows you to run a Linux distribution alongside your Windows installation. Follow these steps to set it up:

1. **Open PowerShell as Administrator** and run the following command to enable WSL:

    ```powershell
    wsl --install
    ```

2. **Restart your computer** if prompted.

3. After rebooting, **install a Linux distribution** from the Microsoft Store (e.g., Ubuntu).

## Prerequisites

1. **WSL Installed**: Ensure that WSL is installed and a Linux distribution (e.g., Ubuntu) is set up on your system.
2. **Clone the Repository**: Clone this repository to your local machine.

```bash
git clone https://github.com/your-username/pomodoro-wsl.git
cd pomodoro-wsl
```

## Set Up the Environment in WSL

1. **Open your newly installed Linux distribution** 
from the Start menu.


2. **Step 2: Install Necessary Packages**
Install the required packages (`espeak`, `lolcat`, `golang`, `spd-say`, and `notify-send`).

    ```bash
    sudo apt update && sudo apt upgrade -y
    sudo apt install espeak lolcat golang spd-say libnotify-bin -y

    # Install timer from source
    git clone https://github.com/caarlos0/timer.git
    cd timer
    go build
    sudo mv timer /usr/local/bin/timer
    cd ..
    rm -rf timer
    ```

## Usage
**Source the Script** : 
Source the script to load the aliases and functions.


**Make the script executable:**

```bash
# Navigate to the directory where pomodoro.sh is saved
cd /path/to/your/script
chmod +x pomodoro.sh
```

 **Source the script to use the aliases:**

```bash
source pomodoro.sh
```
### Using the Pomodoro Script
You can now use the following commands:

### Start Pomodoro with a specified number of loops (default is 2 loops):

```bash
doro 3  # Start with 3 loops of work and break sessions
doro    # Start with the default number of loops (2 loops)
## Run the Aliases
```
### Change work or break time:
```bash 
cp work 50  # Change work time to 50 minutes
cp break 15  # Change break time to 15 minutes
```
Now you can run the aliases `wo` and `br` from your terminal:

```bash
wo  # Start a work session
br  # Start a break session
```
