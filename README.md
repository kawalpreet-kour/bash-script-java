#  Java Installer Script 
---
<img width="512" height="180" alt="image" src="https://dac.digital/wp-content/uploads/2023/04/backend-java-optimized.png" />

---


---
## Author Information
| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|------------------|-----------------|------------------------|
| 18-07-2025      | V1.0    | Kawalpreet Kour  | Internal Review | Pritam                 |
| 25-07-2025      | V1.0    | Kawalpreet Kour  | L0              | Shreya/Sharvani        |
|                 |         | Kawalpreet Kour  | L1              | Abhishek V             |
|                 |         | Kawalpreet Kour  | L2              | Abhishek Dubey/Rishabh sharma |


 ---
## Table of Contents

- [Introduction](#Introduction)
                         
- [Prerequisites](#prerequisites)                      
- [Script Breakdown](#script-breakdown)      
- [Troubleshooting](#troubleshooting)
- [Features](#features) 
  FAQ
 Conclusiom
- [Contact Information](#Contact-Information)
- [References](#References)      

---
## Introduction

This script helps you quickly install and manage Java (OpenJDK) on Ubuntu or Debian Linux systems.

---

## Features

| Feature                             | Description                                                                 |
|-------------------------------------|-----------------------------------------------------------------------------|
|  Multi-Version Support            | Supports OpenJDK 8, 11, 17+ versions                                        |
|  Upgrade-Safe                     | Skips installation if the specified version already exists                 |
|   Custom Default Version          | Allows setting a preferred default Java version                            |
|  Optional Cleanup                 | Can remove previously installed Java versions (optional)                   |
|  OS Compatibility                 | Works seamlessly on Ubuntu and Debian-based Linux systems                  |
|  Auto Configuration              | Automatically sets `JAVA_HOME` and updates `PATH` environment variables    |

---
## Prerequisites


| Requirement       | Description                                                  |
|-------------------|--------------------------------------------------------------|
|  Linux System    | Ubuntu or Debian-based distribution preferred                |
|  Required Tools  | `curl` and `sudo` must be installed                          |
|  User Privileges | The script must be run by a user with `sudo` access          |

---
## Script Breakdown

```bash
#!/bin/bash

install_openjdk() {
    local version=$1
    echo "Installing OpenJDK $version..."
    sudo apt update && sudo apt upgrade -y
    sudo apt install -y openjdk-${version}-jdk
    if [ $? -eq 0 ]; then
        echo "OpenJDK $version installed successfully."

        # Automatically set this Java version as default
        JAVA_PATH="/usr/lib/jvm/java-${version}-openjdk-amd64"
        if [ -d "$JAVA_PATH" ]; then
            echo "Setting Java $version as the default version..."
            sudo update-alternatives --set java "$JAVA_PATH/bin/java"
            sudo update-alternatives --set javac "$JAVA_PATH/bin/javac"
        else
            echo "Error: Java path not found at $JAVA_PATH"
        fi

    else
        echo "Error installing OpenJDK $version."
    fi
}

switch_java_version() {
    echo -e "\nConfiguring Java alternatives (java)..."
    sudo update-alternatives --config java
    echo -e "\nConfiguring Java alternatives (javac)..."
    sudo update-alternatives --config javac
}

show_java_version() {
    echo -e "\nCurrent Java Version:"
    java -version
}

show_menu() {
    echo -e "\nPlease choose one of the Java Installation Options:"
    echo "1. Install OpenJDK 8"
    echo "2. Install OpenJDK 11"
    echo "3. Install OpenJDK 17"
    echo "4. Install OpenJDK 21"
    echo "5. Switch default Java version (interactive)"
    echo "6. Exit"
}

# Loop for repeated use
while true; do
    show_menu
    echo -n "Enter your choice (1-6): "
    read -r choice

    case $choice in
        1)
            install_openjdk 8
            ;;
        2)
            install_openjdk 11
            ;;
        3)
            install_openjdk 17
            ;;
        4)
            install_openjdk 21
            ;;
        5)
            switch_java_version
            ;;
        6)
            echo -e "\nExiting... Goodbye!"
            break
            ;;
        *)
            echo "Invalid choice. Please enter a number between 1–6."
            ;;
    esac

    show_java_version
    echo -e "\nReturning to main menu...\n"
done
```
---
## How to Use

1. **Save the script** with the name:

   ```bash
   java_manager.sh
   ```

2. **Make the script executable:**

   ```bash
   chmod +x java_manager.sh
   ```

3. **Run the script:**

   ```bash
   ./java_manager.sh
   ```



---
## Features

| Feature                   | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| Easy Java Installation    | Install OpenJDK versions 8, 11, 17, or 21 with one simple menu choice       |
| Smart Version Handling    | Automatically skips reinstallation if a version is already installed       |
| Set Default Java Easily   | Automatically sets the newly installed Java version as the system default  |
| Manual Version Switching  | Lets you manually switch between installed Java versions using a menu       |
| Ubuntu/Debian Support     | Works smoothly on Ubuntu and other Debian-based Linux systems               |
| Shows Current Version     | Displays the current default Java version after each operation             |

---

## FAQ

1. **Which Java versions can I install using this script?**  
   You can install OpenJDK versions 8, 11, 17, and 21 directly through the script menu.

2. **Can I switch between Java versions after installing?**  
   Yes, the script allows you to manually switch between installed versions using the "Switch default Java version" option.

3. **Will this script work on all Linux systems?**  
   This script is tested and designed for Debian-based systems like Ubuntu. It may not work correctly on RedHat, CentOS, or Arch-based systems.

---
- ##  Conclusion

> This script offers a quick and hassle-free way to manage Java installations on Ubuntu and Debian systems — ideal for both beginners and advanced users.

---
## Contact Information

| Name             | Email                                         |
|------------------|-----------------------------------------------|
| Kawalpreet Kour  | Kawalpreet.kour.snaatak@mygurukulam.co        |

---


## References

| Title        | Link |
|--------------|------|
| Official Java Download Options | [https://www.java.com/en/download/help/download_options.html](https://www.java.com/en/download/help/download_options.html) |
| GeeksforGeeks Java Install Guide | [https://www.geeksforgeeks.org/linux-unix/download-install-java-windows-linux-macos/](https://www.geeksforgeeks.org/linux-unix/download-install-java-windows-linux-macos/) |
| Oracle Java SE Installation Overview | [https://docs.oracle.com/en/java/javase/17/install/overview-jdk-installation.html](https://docs.oracle.com/en/java/javase/17/install/overview-jdk-installation.html) |

---
