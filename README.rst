python-forexconnect for Python 3
================================

This is a Python 3 version of the https://github.com/neka-nat/python-forexconnect.git
work.

About
-----
This library is a Python binding of Forexconnect API
using boost.python3.

Build
-----

First, install the required packages.

    $ sudo apt-get install build-essential cmake libboost-log-dev libboost-date-time-dev libboost-python-dev

And then, download "ForexConnectAPI-1.4.1" from http://www.fxcodebase.com/wiki/index.php/Download
and set environment "FOREXCONNECT_ROOT" which is the path ForexConnectAPI installed.

    $ wget http://fxcodebase.com/bin/forexconnect/1.4.1/ForexConnectAPI-1.4.1-Linux-x86_64.tar.gz

    $ tar xvf ForexConnectAPI-1.4.1-Linux-x86_64.tar.gz

    $ export FOREXCONNECT_ROOT=$(pwd)/ForexConnectAPI-1.4.1-Linux-x86_64

    $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(pwd)/ForexConnectAPI-1.4.1-Linux-x86_64/lib

Next, clone this repository.

    $ git clone https://github.com/SinHouse/python3-forexconnect.git

Edit "python3-forexconnect/CMakeLists.txt" and change below lines to set your system
configuration, the default configuration is for Ubuntu Boost Python 3.5 library:

    # debian and ubuntu (change "python-py35" to your system version)

    find_package(Boost COMPONENTS log date_time python-py35 REQUIRED)

    # Mac and others

    # find_package(Boost COMPONENTS log date_time libboost_python3 REQUIRED)

Build and install.
*Note*: It's highly recommended to activate a target Python venvironment prior to build
the forexconnect module. The module will be installed in the "site-packages" folder of
the current Python interpreter, Ubuntu defaults point to the Python 2.7 version.

    $ cd python3-forexconnect

    $ mkdir build

    $ cd build

    $ cmake .. -DDEFAULT_FOREX_URL="http://<Your forexconnect URL>"

    $ sudo make install


Usage
-----

This tutorial is simple trading using python3-forexconnect.
First, give FXCM account username, password and type ("Real" or "Demo") to login.
Next, send query to open position and get the position list which you have.
Finally, close the opened position and logout.

::

   >> import forexconnect
   >> cl = forexconnect.ForexConnectClient("usrname", "pass", "Real")
   >> cl.open_position("EUR/JPY", forexconnect.BUY, 1)
   >> ti = cl.get_trades()
   >> cl.close_position(ti[0].trade_id)
   >> cl.logout()

Requirements
------------

* boost 1.54
* ForexConnectAPI 1.4.1
* Python 3
