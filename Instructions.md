### Step 1: Update and Upgrade Your System
First, ensure your system is up to date by running the following commands:

```bash
sudo apt update
sudo apt upgrade -y
```

### Step 2: Install Required Dependencies
ArduPilot requires several dependencies. Install them using the following commands:

```bash
sudo apt install -y git python3 python3-pip python3-dev python3-setuptools build-essential ccache g++-arm-linux-gnueabihf g++-arm-linux-gnueabi gcc-arm-linux-gnueabihf gcc-arm-linux-gnueabi make pkg-config libtool autoconf automake libncurses5-dev libncursesw5-dev
```

### Step 3: Install Additional Tools
Install additional tools required for building and running ArduPilot:

```bash
sudo apt install -y cmake gawk genromfs ninja-build exiftool
```

### Step 4: Clone the ArduPilot Repository
Clone the ArduPilot repository from GitHub:

```bash
git clone https://github.com/ArduPilot/ardupilot.git
cd ardupilot
```

### Step 5: Install Python Dependencies
Navigate to the `Tools/environment_install` directory and run the installation script for Python dependencies:

```bash
cd Tools/environment_install
./install-prereqs-ubuntu.sh -y
. ~/.profile
```

### Step 6: Install SITL (Software In The Loop)
SITL allows you to simulate ArduPilot without hardware. Install it using the following commands:

```bash
cd ~/ardupilot
Tools/environment_install/install-prereqs-ubuntu.sh -y
. ~/.profile
```

### Step 7: Build ArduPilot
Navigate to the ArduPilot directory and build the project. For example, to build the copter firmware:

```bash
cd ~/ardupilot/ArduCopter
./waf configure --board sitl
./waf copter
```

### Step 8: Run SITL
You can now run SITL to simulate a flight controller:

```bash
cd ~/ardupilot/ArduCopter
sim_vehicle.py -v ArduCopter
```

### Step 9: Install Ground Control Software
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
