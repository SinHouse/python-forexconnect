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
First, give FXCM account username, password, type ("Real" or "Demo"), and url to login.
Next, download and print historical data
Finally, logout.

::

   >> import forexconnect
   >> import datetime
   >>
   >> client = forexconnect.ForexConnectClient('usermane',
   >>                                          'password',
   >>                                          'Demo',
   >>                                          'http://www.fxcorporate.com/Hosts.jsp')
   >>
   >> data = client.get_historical_prices('EUR/USD',
   >>                                     datetime.datetime(2016, 11, 8, 10, 0),
   >>                                     datetime.datetime(2016, 11, 9, 17, 0),
   >>                                     'm5')
   >> print(data)
   >> client.logout()

Requirements
------------

* boost 1.54
* ForexConnectAPI 1.4.1
* Python 3
