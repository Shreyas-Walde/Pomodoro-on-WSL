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

## Set Up the Environment in WSL

1. **Open your newly installed Linux distribution** from the Start menu.

2. **Update the package lists:**

    ```bash
    sudo apt update
    sudo apt upgrade
    ```

3. **Install the necessary packages (`espeak` and `lolcat`)**. Note that `timer` might not be available in the default repositories, so you might need to build it from source or use an alternative:

    ```bash
    sudo apt install espeak
    sudo apt install lolcat
    ```

4. **Install `timer` from source** (you may need to install `go` to build it):

    ```bash
    sudo apt install golang
    git clone https://github.com/caarlos0/timer.git
    cd timer
    go build
    sudo mv timer /usr/local/bin/timer
    ```

## Create and Run Your Script

1. **Save the provided script to a file**, e.g., `pomodoro.sh`:

    ```bash
    nano pomodoro.sh
    ```

2. **Paste the script content into `pomodoro.sh`:**

    ```bash
    #!/bin/bash
    
    declare -A pomo_options
    pomo_options["work"]="45"
    pomo_options["break"]="10"
    
    pomodoro () {
      if [ -n "$1" -a -n "${pomo_options["$1"]}" ]; then
      val=$1
      echo $val | lolcat
      timer ${pomo_options["$val"]}m
      spd-say "'$val' session done"
      fi
    }
    
    alias wo="pomodoro 'work'"
    alias br="pomodoro 'break'"
    ```

3. **Make the script executable:**

    ```bash
    chmod +x pomodoro.sh
    ```

4. **Source the script to use the aliases:**

    ```bash
    source pomodoro.sh
    ```

## Run the Aliases

Now you can run the aliases `wo` and `br` from your terminal:

```bash
wo
br
```
