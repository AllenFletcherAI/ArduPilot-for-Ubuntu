To download and install ArduPilot on Ubuntu 22.04.04, you will need several prerequisites, including Git and other necessary tools and libraries. Here is a list of the main prerequisites and how to install them:

1. **Git**: Git is required to clone the ArduPilot repository.
   ```bash
   sudo apt-get update
   sudo apt-get install git
   ```

2. **Python**: Python is needed for various scripts and tools used by ArduPilot.
   ```bash
   sudo apt-get install python3 python3-pip
   ```

3. **Waf**: Waf is a build system used by ArduPilot.
   ```bash
   sudo pip3 install future
   sudo pip3 install empy
   sudo pip3 install pexpect
   sudo pip3 install pyserial
   sudo pip3 install pymavlink MAVProxy
   ```

4. **Required Libraries**: Several libraries are needed for building and running ArduPilot.
   ```bash
   sudo apt-get install build-essential ccache g++ gawk git make wget
   sudo apt-get install libtool libxml2-dev libxslt1-dev python-dev
   sudo apt-get install python-lxml python-pip python-setuptools
   sudo apt-get install python3-dev python3-lxml python3-pip
   sudo apt-get install libncurses5-dev libncursesw5-dev
   sudo apt-get install libffi-dev libssl-dev
   sudo apt-get install pkg-config
   sudo apt-get install libgmp-dev
   sudo apt-get install libmpfr-dev
   sudo apt-get install libmpc-dev
   sudo apt-get install libfl-dev
   sudo apt-get install bison
   sudo apt-get install flex
   sudo apt-get install gawk
   sudo apt-get install gperf
   sudo apt-get install libtool-bin
   sudo apt-get install texinfo
   sudo apt-get install zlib1g-dev
   sudo apt-get install libexpat1-dev
   sudo apt-get install libusb-1.0-0-dev
   sudo apt-get install libudev-dev
   sudo apt-get install libopencv-dev
   sudo apt-get install python-opencv
   sudo apt-get install python3-opencv
   sudo apt install -y g++-arm-linux-gnueabihf g++-arm-linux-gnueabi gcc-arm-linux-gnueabihf gcc-arm-linux-gnueabi autoconf automake
   ```

5. **Additional Tools**: Some additional tools might be required depending on your specific needs.
   ```bash
   sudo apt-get install cmake
   sudo apt-get install ninja-build
   sudo apt-get install gdb
   sudo apt-get install valgrind
   ```

Once you have installed all the prerequisites, we can proceed:

### Step 1: Update and Upgrade Your System
First, ensure your system is up to date by running the following commands:

```bash
sudo apt update
sudo apt upgrade -y
```

### Step 2: Install Additional Tools
Install additional tools required for building and running ArduPilot:

```bash
sudo apt install -y cmake gawk genromfs ninja-build exiftool
```

### Step 3: Clone the ArduPilot Repository
Clone the ArduPilot repository from GitHub:

```bash
git clone https://github.com/ArduPilot/ardupilot.git
cd ardupilot
```

### Step 4: Install Python Dependencies
Navigate to the `Tools/environment_install` directory and run the installation script for Python dependencies:

```bash
cd Tools/environment_install
./install-prereqs-ubuntu.sh -y
. ~/.profile
```

### Step 5: Install SITL (Software In The Loop)
SITL allows you to simulate ArduPilot without hardware. Install it using the following commands:

```bash
cd ~/ardupilot
Tools/environment_install/install-prereqs-ubuntu.sh -y
. ~/.profile
```

### Step 6: Build ArduPilot
Navigate to the ArduPilot directory and build the project. For example, to build the copter firmware:

```bash
cd ~/ardupilot/ArduCopter
./waf configure --board sitl
./waf copter
```

### Step 7: Run SITL
You can now run SITL to simulate a flight controller:

```bash
cd ~/ardupilot/ArduCopter
sim_vehicle.py -v ArduCopter
```

### Step 8: Install Ground Control Software
To interact with ArduPilot, you have to install a ground control station (GCS) like APM Planner 2. Here’s how you can install APM Planner 2:

1. **Download APM Planner 2:**
   Go to the [APM Planner 2 releases page](https://github.com/ArduPilot/apm_planner/releases) and download the latest `.deb` package for Ubuntu.

   Alternatively, you can use the following command to download it directly (replace `VERSION` with the latest version number):

   ```bash
   wget https://github.com/ArduPilot/apm_planner/releases/download/VERSION/apm_planner_VERSION_ubuntu64.deb
   ```

2. **Install APM Planner 2:**
   Once the download is complete, install the package using `dpkg`:

   ```bash
   sudo dpkg -i apm_planner_VERSION_ubuntu64.deb
   ```

3. **Fix any dependency issues:**
   If there are any missing dependencies, you can fix them by running:

   ```bash
   sudo apt --fix-broken install
   ```

### Step 10: Verify Installation
Ensure everything is working by running SITL and connecting it to APM Planner 2. You should be able to see the simulated vehicle and interact with it.
