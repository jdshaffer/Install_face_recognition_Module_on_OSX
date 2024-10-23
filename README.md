Solving hand\_recognition Module Installation Errors on MacOS
=============================================================

Date: 2024-10-22
----------------

  

Problem
-------

*   Cannot install the hand\_recognition module for Python3 on MacOS

  

Details
-------

*   `pip3 install hand_recognition` throws various errors, particularly issues with `dlib`.
*   `pip3 install dlib` also fails with multiple errors (e.g., wheel issues).
*   Online help is limited, mostly focused on Windows users or older Python versions.

  

My Solution
-----------

1.  We need to have the XCode Tools installed before doing all this as we will be compiling our own `dlib`. Note that this might take awhile:
    
        xcode-select --install
    
2.  Following some advice I found on YouTube, I downloaded the `dlib` repository from GitHub:
    
        https://github.com/davisking/dlib
    
3.  I then unzipped the downloaded file and made a backup for future use. (You can also just double-click the file in a Finder window. That's what I did.):
    
        unzip dlib-master.zip
    
4.  I started up my custom python virtual environment. Perhaps you don't need to, but as I run python3 from a homebrew install (`brew install python3`) homebrew requires me to use a virtual environment to install modules:
    
        source /PATH_TO_MY_ENVIROMENT_FOLDER/bin/activate
    
5.  I then uninstalled all versions of `cmake` on my system. I don't know why I needed to do this, but it was the only way I could get this to work:
    
        brew uninstall cmakepip3 uninstall cmake
    
6.  I then installed a small collection of helper tools called `setuptools`. _This seems to be the key to a successful install._ This module side-steps a problem introduced in newer versions of python (greater than 3.11) where users are not able to install the necessary module `distutils` because it is depreciated and no longer available to install! However, this module **_is included_** in the `setuptools` module! Moment of honesty -- I read about this side-step via an older Japanese post on X (Twitter). It's not my genius at work:
    
        pip3 install setuptools
    
7.  After that, I tried compiling the `dlib` program that I downloaded from GitHub (Step 2 above), but running it at this point causes it to complain about a missing `cmake`. That's OK, as we purposely deleted `cmake` above. However, _for some odd reason_ I need to try running the setup program at this point, even before installing `cmake`. \*shrug\* Just to be clear, the following command seems necessary, but will fail to install:
    
        python3 setup.py install
    
8.  So, now I installed `cmake` inside my virtual environment:
    
        pip3 install cmake
    
9.  Then I ran the `setup.py` program again to compile `dlib`, and it works!:
    
        python3 setup.py install
    
9.  Finally, I could install the desired `face_recognition` module for python:
    
        pip3 install face_recognition
    
10.  Done!
