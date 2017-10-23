---
title: "Playground Setup"
---

In this document we will install a set of components that are fundamental for the BigClown projects and will help you to get started quickly on your workstation or laptop.

These fundamental components are:

* The MQTT broker **Mosquitto** (with client tools)

* The web-based tool **Node-RED** for automation flows

* The process manager **PM2** to start the components automatically on boot

* The Python application **BigClown Gateway** for MQTT/gateway bridging

    {{% note "info" %}}This component works as a bridge between the serial port of **BigClown USB Dongle** or **BigClown Core Module** and an MQTT broker.{{% /note %}}

Once you install this setup, you will be able to start designing your automation flows quickly and easily.

## Requirements

* Workstation with **Windows**, **macOS** or **Ubuntu**

* **BigClown USB Dongle**

* One of the **BigClown IoT kits**

## Platform Guides

Select the setup procedure on one of the supported operating systems:

* [**Playground Setup on Windows**]({{< relref "#playground-setup-on-windows" >}})

* [**Playground Setup on macOS**]({{< relref "#playground-setup-on-macos" >}})

* [**Playground Setup on Ubuntu**]({{< relref "#playground-setup-on-ubuntu" >}})

If you already have previously installed playground, you can upgrade it at any time:

* [**Playground Upgrade on Windows**]({{< relref "#playground-upgrade-on-windows" >}})

* [**Playground Upgrade on macOS**]({{< relref "#playground-upgrade-on-macos" >}})

* [**Playground Upgrade on Ubuntu**]({{< relref "#playground-upgrade-on-ubuntu" >}})

## Playground Setup on Windows

**TODO**

## Playground Upgrade on Windows

**TODO**

## Playground Setup on macOS

1. Install the driver for the **BigClown USB Dongle**:

    {{% download "Download from FTDI" "http://www.ftdichip.com/Drivers/VCP/MacOSX/FTDIUSBSerialDriver_v2_4_2.dmg" %}}

    {{% note "info" %}}This is a driver for the FT231X USB UART bridge.{{% /note %}}

2. Restart your computer.

3. Open the **Terminal** application.

4. Install [**Homebrew**](https://brew.sh) (unless you already have it).

5. Upgrade the **Homebrew** packages:

        brew update && brew upgrade

6. Install **Mosquitto** server and clients:

        brew install mosquitto

        brew services start mosquitto

7. Install **Node.js** version 6 (required by **Node-RED**).

        brew install node node@6
    \

        brew unlink node
    \

        echo 'export PATH="/usr/local/opt/node@6/bin:$PATH"' >> ~/.bash_profile
    \

        source ~/.bash_profile

8. Install **Node-RED**:

        sudo npm install -g --unsafe-perm node-red

9. Install **PM2**:

        sudo npm install -g pm2

    {{% note "info" %}}**PM2** is a process manager that will help you to start **Node-RED** and other processes on boot.{{% /note %}}

10. Tell **PM2** to run **Node-RED**:

        pm2 start `which node-red` -- -v

11. Tell **PM2** to run on boot:

        pm2 save
        pm2 startup

    {{% note "danger" %}}Follow the instructions provided by the command `pm2 startup`.{{% /note %}}

12. Install **Python 3** (required by the **BigClown Gateway**).

        brew install python3

13. Install the **BigClown Firmware Tool**:

        sudo pip3 install --upgrade bcf

14. Install the **BigClown Gateway**:

        sudo pip3 install --upgrade bcg

15. Plug the **BigClown USB Dongle** into a USB port.

16. List the available devices:

        bcf devices

    {{% note "warning" %}}You can have multiple devices connected at the same time, but then you must specify which one you want to use. Otherwise the first device in the list is used implicitly.{{% /note %}}

17. Upload the latest firmware into the **BigClown USB Dongle**:

        bcf update
    \

        bcf flash bigclownlabs/bcf-usb-dongle:latest

    {{% note "warning" %}}If you have multiple devices, please specify it as `bcf flash --device <device>`.{{% /note %}}

18. Start the **BigClown Gateway** (in the background):

        bcg --device ...

    {{% note "note" %}}Replace `...` with the device listed using `bcf devices`.{{% /note %}}

19. Start **Node-RED**:

        node-red

20. Open your web browser with the URL:

    **https://localhost:1880/**

21. Continue in the document [**Playground Starter**]({{< relref "doc/tutorials/playground-starter.en.md" >}}).

## Playground Upgrade on macOS

1. Upgrade the **Homebrew** packages:

        brew update && brew upgrade

2. Upgrade **Node-RED**:

        sudo npm update -g node-red

3. Upgrade **PM2**:

        sudo npm update -g pm2

4. Upgrade the **BigClown Firmware Tool**:

        sudo pip3 install --upgrade bcf

5. Upgrade the **BigClown Gateway**:

        sudo pip3 install --upgrade bcg

## Playground Setup on Ubuntu

1. Open the **Terminal** application.

2. Upgrade all packages:

        sudo apt update && sudo apt upgrade

3. Install **Mosquitto** server and clients:

        sudo apt install mosquitto mosquitto-clients

4. Install **Node.js** version 6 (required by **Node-RED**).

        sudo apt install nodejs

5. Install **Node-RED**:

        sudo npm install -g --unsafe-perm node-red

6. Install **PM2**:

        sudo npm install -g pm2

    {{% note "info" %}}**PM2** is a process manager that will help you to start **Node-RED** and other processes on boot.{{% /note %}}

7. Tell **PM2** to run **Node-RED**:

        pm2 start `which node-red` -- -v

8. Tell **PM2** to run on boot:

        pm2 save
        pm2 startup systemd

    {{% note "danger" %}}Follow the instructions provided by the command `pm2 startup systemd`.{{% /note %}}

9. Install **Python 3** (required by the **BigClown Gateway**).

        sudo apt install python3.5

10. Install the **BigClown Firmware Tool**:

        sudo pip3 install --upgrade bcf

11. Install the **BigClown Gateway**:

        sudo pip3 install --upgrade bcg

12. Plug the **BigClown USB Dongle** into a USB port.

13. List the available devices:

        bcf devices

    {{% note "warning" %}}You can have multiple devices connected at the same time, but then you must specify which one you want to use. Otherwise the first device in the list is used implicitly.{{% /note %}}

14. Upload the latest firmware into the **BigClown USB Dongle**:

        bcf update
    \

        bcf flash bigclownlabs/bcf-usb-dongle:latest

    {{% note "warning" %}}If you have multiple devices, please specify it as `bcf flash --device <device>`.{{% /note %}}

15. Start the **BigClown Gateway** (in the background):

        bcg --device ...

    {{% note "note" %}}Replace `...` with the device listed using `bcf devices`.{{% /note %}}

16. Start **Node-RED**:

        node-red

17. Open your web browser with the URL:

    **https://localhost:1880/**

18. Continue in the document [**Playground Starter**]({{< relref "doc/tutorials/playground-starter.en.md" >}}).

## Playground Upgrade on Ubuntu

1. Upgrade all the packages:

        sudo apt update && sudo apt upgrade

2. Upgrade **Node-RED**:

        sudo npm update -g node-red

3. Upgrade **PM2**:

        sudo npm update -g pm2

4. Upgrade the **BigClown Firmware Tool**:

        sudo pip3 install --upgrade bcf

5. Upgrade the **BigClown Gateway**:

        sudo pip3 install --upgrade bcg

## Related Documents

* [**Playground Starter**]({{< relref "doc/tutorials/playground-starter.en.md" >}})

* [**Toolchain Setup**]({{< relref "doc/firmware/toolchain-setup.en.md" >}})

* [**Toolchain Guide**]({{< relref "doc/firmware/toolchain-guide.en.md" >}})