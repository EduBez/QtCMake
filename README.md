# Setup & Build Instructions
You can build the application under Ubuntu release 18.04 and Windows 10
  
  Follow the instructions for each platform

## Ubuntu 18.04
### Update GCC to the latest version

Install GCC 10.x

		sudo apt install build-essential
		sudo apt install software-properties-common
		
		sudo add-apt-repository ppa:ubuntu-toolchain-r/test
		sudo apt update
		sudo apt upgrade
		sudo apt install gcc-10 g++10
		
Update alternatives

		sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-10 10 --slave /usr/bin/g++ g++ /usr/bin/g++-10 --slave /usr/bin/gcov gcov /usr/bin/gcov-10
		sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 70 --slave /usr/bin/g++ g++ /usr/bin/g++-7 --slave /usr/bin/gcov gcov /usr/bin/gcov-7
	
	
Change system compiler to GCC 10.x

		sudo update-alternatives --config gcc
		
You will be presented with a list of all installed GCC versions on your Ubuntu system. Enter the number of the version you want to be used as a default and press Enter

### Remove Old Qt Versions

Remove any previous version of Qt using the MaintenanceTool application located under the old Qt home directory

### Download and Install Qt 5.15

Download Qt 5.15

		cd $HOME
		wget -q --show-progress -P $HOME/Downloads/ http://linorg.usp.br/Qt/archive/online_installers/3.2/qt-unified-linux-x64-3.2.3-online.run


Install Qt 5.15

		cd $HOME/Downloads
		chmod +x qt-unified-linux-x64-3.2.3-online.run
		./qt-unified-linux-x64-3.2.3-online.run

Log to your Qt account
Under Qt 5.15.0 select the following components

- Desktop gcc 64-bit
- Sources
- Qt Charts
- Qt Quick 3D
- Qt Data Visualization
- Qt Lottie Animation
- Qt Purchansing
- Qt Virtual Keyboard
- Qt Wayland Compositor
- Qt WebEngine
- Qt Network Authorization
- Qt WebGL Streaming Plugin
- Qt Debug Information Files
- Qt Quick Timeline

Under Developer and Designer Tools select the following components

- Qt Creator 4.13.0 CDB Debugger Support
- Qt 3D Studio 2.7.0
- Qt Design Studio 1.5.0-community
- Qt Installer Framework 3.2
- Qt 3D Studio OpenGL Runtime 2.7.0 for Qt 5.15.0
- CMake 3.17.1
- Ninja 1.10.0
- OpenSSL 1.1.1d Toolkit

After finishing the installation edit **.bashrc** and add the following line
  
		cd $HOME
		nano .bashrc
		export QT_PLUGIN_PATH="$HOME/Qt/5.15.0/gcc_64/plugins"

Save the file and execute source
  
		source .bashrc

Remove all existent Qt5 libraries from **/usr/lib/x86_64-linux-gnu**, keep only the Qt5 libraries from your home Qt directory

		sudo rm /usr/lib/x86_64-linux-gnu/libQt5*.so*
		
Add Qt 5.15 libraries directory to the system *LIBRARY PATH*
  
		sudo touch /etc/ld.so.conf.d/qt_5-15-0.conf

Edit **qt_5-15-0.conf** and add the following line. 
Change user name according, in this case, the default user name is 'valemobi'
  
		sudo nano /etc/ld.so.conf.d/qt_5-15-0.conf
		/home/valemobi/Qt/5.15.0/gcc_64/lib

Save the file, exit and run **ldconfig**
  
		sudo ldconfig

### Install Qt Dependencies

		sudo apt install libxcb-xinerama0 libgl1-mesa-dev mesa-common-dev

### Install VcPkg C++ Package Manager

In order to build the project we need VcPkg
  
		cd $HOME
		git clone https://github.com/microsoft/vcpkg.git

Compile and build VcPkg

		cd $HOME/vcpkg
		sudo apt install curl unzip tar
		./bootstrap-vcpkg.sh
		./vcpkg integrate install

Install the following packages

		./vcpkg install chartdir
		./vcpkg install gflags
		./vcpkg install glog
		./vcpkg install lua
		./vcpkg install zlib
		
Add **ChartDir library** to the system *LIBRARY PATH*
  
		sudo touch /etc/ld.so.conf.d/chartdir.conf

Edit **chartdir.conf** and add the following line
Change user name according, in this case, the default user name is 'valemobi'
  
		sudo nano /etc/ld.so.conf.d/chartdir.conf
		/home/valemobi/vcpkg/installed/x64-linux/lib

Save the file, exit and run **ldconfig**
  
		sudo ldconfig

### Install OpenSSL Developer Package

Install the OpenSSL developer libraries

		 sudo apt install libssl-dev

### Install LUA Developer Package

Install the LUA developer libraries

		 sudo apt install liblua5.3-dev

### Clone the 'plataforma' repository from GitLab using HTTP
		git clone https://raposa.valebroker.com.br/2020/plataforma.git

### Install Application Config Files

Create a **Valemobi** directory structure under **.config**
  
		 mkdir -p $HOME/.config/Valemobi/Valebroker/Valebroker

Copy all **db.gz** files from **plataforma/config** to your Valemobi **.config** folder
		cd $HOME
		cp plataforma/config/*.db.gz $HOME/.config/Valemobi/Valebroker

### Build the Application

Execute **Qt Creator**
  
		File, Open File or Project...
		Navigate to plataforma/gui and select CMakeLists.txt
		Build the project

## Windows 10
### Install Visual Studio 2019

Download Visual Studio 2019 Community from
https://visualstudio.microsoft.com/vs/

The following workloads must be selected for installation

- Desktop development with C++
- Linux development with C++

The following individual components must be selected for installation

Under Compilers, build tools and runtimes

- C++ 2019 Redistributable MSMs
- C++ 2019 Redistributable Update
- C++ Clang Compiler for Windows
- C++ Clang-cl for v142 build tools (x64/x86)
- C++ CMake tools for Windows

Under Code tools

- Git for Windows
- GitHub extension for Visual Studio

Under Development activities

- C++ CMake tools for Linux
- C++ core features
- C++ for Linux Development

Under SDKs, libraries and frameworks

- Windows 10 SDK (10.0.19041.0)

### Remove Old Qt Versions

Remove any previous version of Qt using the MaintenanceTool application located under the old Qt home directory

### Download and Install Qt 5.15

Download Qt 5.15 from
https://www.qt.io/download-open-source

Log to your Qt account
Under Qt 5.15.0 select the following components

- MSVC 2019 64-bit
- Sources
- Qt Charts
- Qt Quick 3D
- Qt Data Visualization
- Qt Lottie Animation
- Qt Purchansing
- Qt Virtual Keyboard
- Qt WebEngine
- Qt Network Authorization
- Qt WebGL Streaming Plugin
- Qt Debug Information Files
- Qt Quick Timeline

Under Developer and Designer Tools select the following components

- Qt Creator 4.13.0 CDB Debugger Support
- Debugging Tools for Windows
- Qt 3D Studio 2.7.0
- Qt Design Studio 1.5.0-community
- Qt Installer Framework 3.2
- Qt 3D Studio OpenGL Runtime 2.7.0 for Qt 5.15.0
- CMake 3.17.1 64-bit
- Ninja 1.10.0
- OpenSSL 1.1.1d Toolkit

Click the Start Menu and type: 'Edit the system environment variables'
Click 'Environment Variables...'
On the 'System variables' pane click 'New...'

        Variable name: QT_PLUGIN_PATH
        Variable value: C:\Qt\5.15.0\msvc2019_64\plugins

On the 'System variables' pane edit the 'PATH' variable and add the Qt binaries directory

        Variable name: PATH
        Variable value: C:\Qt\5.15.0\msvc2019_64\bin

### Install Git

Download Git at
https://github.com/git-for-windows/git/releases/download/v2.28.0.windows.1/Git-2.28.0-64-bit.exe
Execute Git-2.28.0-64-bit.exe to install Git

### Install CMake

Download CMake at https://github.com/Kitware/CMake/releases/download/v3.18.2/cmake-3.18.2-win64-x64.msi
Execute cmake-3.18.2-win64-x64.msi to install CMake
Check 'Add CMake to the system PATH for all users'

### Define VCPKG_DEFAULT_TRIPLET Global Environment Variable

Click the Start Menu and type: 'Edit the system environment variables'
Click 'Environment Variables...'
On the 'System variables' pane click 'New...'

		Variable name: VCPKG_DEFAULT_TRIPLET
		Variable value: x64-windows

### Install VcPkg C++ Package Manager

In order to build the project we need VcPkg
  
		C:
		cd C:\
		git clone https://github.com/microsoft/vcpkg.git

Compile and build VcPkg

		cd vcpkg
		bootstrap-vcpkg.bat
		vcpkg integrate install

Install the following packages

		vcpkg install chartdir
		vcpkg install gflags
		vcpkg install glog
		vcpkg install lua
		vcpkg install zlib

### Install OpenSSL Developer Package

Download OpenSSL developer package at
https://slproweb.com/download/Win64OpenSSL-1_1_1g.msi

		 Execute Win64OpenSSL-1_1_1g.msi to install OpenSSL in your system
		 Check the option: Copy OpenSSL DLLs to: The Windows system directory

### Clone the 'plataforma' repository from GitLab using HTTP
		git clone https://raposa.valebroker.com.br/2020/plataforma.git

### Install Application Config Files

Open File Explorer and create a directory structure **Valemobi** under
  
		 C:\Users\<YourUserNameHere>\AppData\Local

Copy all **db.gz** files from **C:\plataforma\config** to your Valemobi **AppData\Local** folder
  
		C:\Users\<YourUserNameHere>\AppData\Local\Valemobi\Valebroker

### Build the Application

Execute **Qt Creator**
  
		File, Open File or Project...
		Navigate to plataforma/gui and select CMakeLists.txt
		Build the project

