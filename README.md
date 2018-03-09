## Building inTime only for x64 processor

### On Ubuntu 16.04 LTS

//Open terminal in home directory

____________________________________________

//Install gnu gcc 5.4.0

sudo apt update

sudo apt upgrade

sudo apt install build-essential

____________________________________________

//Install cmake 3.5.1

sudo apt install cmake

____________________________________________

//Install git 1:2.7.4

sudo apt install git

____________________________________________

//Install Python 2.7.12

sudo wget https://www.python.org/ftp/python/2.7.12/Python-2.7.12.tgz

sudo tar xzf Python-2.7.12.tgz

cd Python-2.7.12

sudo ./configure

sudo make altinstall

cd

____________________________________________

//Install glibcxx 3.4.21

strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBCXX

sudo apt-get install libstdc++6

sudo add-apt-repository ppa:ubuntu-toolchain-r/test

sudo apt-get update

sudo apt-get upgrade

sudo apt-get dist-upgrade

____________________________________________

//Install qt5

sudo apt-get install qt5-default

____________________________________________

//Swapfile (If you install boost 1.58 and get the error: Could not allocate physical memory)

sudo fallocate -l 2G /swapfile

sudo chmod 600 /swapfile

sudo mkswap /swapfile

sudo swapon /swapfile

____________________________________________

//Install boost 1.58

wget -O boost_1_58_0.tar.gz http://sourceforge.net/projects/boost/files/boost/1.58.0/boost_1_58_0.tar.gz/download

tar xzvf boost_1_58_0.tar.gz

cd boost_1_58_0/

sudo apt-get update

sudo apt-get install build-essential g++ python-dev autotools-dev libicu-dev build-essential libbz2-dev

./bootstrap.sh --prefix=/usr/local

user_configFile=`find $PWD -name user-config.jam`

echo "using mpi ;" >> $user_configFile

n=`cat /proc/cpuinfo | grep "cpu cores" | uniq | awk '{print $NF}'`

sudo ./b2 --with=all -j $n install

sudo sh -c 'echo "/usr/local/lib" >> /etc/ld.so.conf.d/local.conf'

sudo ldconfig

cd

____________________________________________

//Get repository

git clone https://github.com/gGluk/intime.git

cd intime

___________________________________________

//Building

make -j3

cd build/release/src

./intimed

___________________________________________

//Mining

//paste your wallet adress in intime terminal

start_mining [your wallet adress] [threads=2]

Good luck!
