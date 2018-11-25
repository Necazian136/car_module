# car_module

Start from a clean state, remove every apt-package you've installed for openaplr if you've already messed it up. Remove the python binding, if you've set up that too.

apt list --installed | grep alpr
sudo apt-get purge libopenalpr
sudo rm -rf /usr/local/lib/python3.5/dist-packages/openalpr*

# Install prerequisites
sudo apt-get install libopencv-dev libtesseract-dev git cmake build-essential libleptonica-dev
sudo apt-get install liblog4cplus-dev libcurl3-dev

# If using the daemon, install beanstalkd
sudo apt-get install beanstalkd

# Clone the latest code from GitHub
git clone https://github.com/openalpr/openalpr.git

# Setup the build directory
cd openalpr/src
mkdir build
cd build

# setup the compile environment
cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_INSTALL_SYSCONFDIR:PATH=/etc ..

# compile the library
make

# Install the binaries/libraries to your local system (prefix is /usr)
sudo make install

cd openalpr/src/bindings/python/
sudo python3 setup.py install

