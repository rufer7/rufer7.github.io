---
layout: post
category: knowledge-base
title: Run deltacloud on a VirtualBox-VM
date: 13 Jan 2015
tags: Apache deltacloud CIMI ruby
---

For getting in touch with the Cloud Infrastructure Management Interface ([CIMI](http://dmtf.org/sites/default/files/standards/documents/DSP0263_1.0.0e.pdf)) I installed the deltacloud server on a VirtualBox-VM.


Deltacloud is an apache open source project, which provides a REST-based API for accessing several different cloud platforms. Deltacloud supports three different frontends: classic Deltacloud, DMTF CIMI and EC2.

The following section describes the installation of deltacloud on a VirtualBox-VM step by step

1. [Download](https://www.virtualbox.org/wiki/Downloads) and install VirtualBox
2. [Download](http://www.ubuntu.com/download/desktop) an ubuntu image
3. Create a new VM in VirtualBox
   1. Click new
   2. Type: Linux; Version: Ubuntu (64bit)
   3. Memory: 1024MB
   4. Click through the wizard without changing the default settings

4. Modify the machine settings in VirtualBox
   1. Select your VM and press `Ctrl + s`
   2. Go to Network
   3. Choose Adapter 2
   4. Select `Host-only Adapter`
5. Start the VM. While first startup you will be asked to reference the previously downloaded ubuntu image.
6. Install ruby and generate symlinks by executing following commands in the terminal

   ```sudo apt-get install ruby1.9.1-full```

   ```sudo ln -s /usr/bin/ruby1.9.1 /usr/bin/ruby```

   ```sudo ln -s /usr/bin/gem1.9.1 /usr/bin/gem```

7. Check the installation

   ```ruby -v```

   ```gem -v```

8. Install the following libraries, which are necessary to run deltacloud

   ```sudo apt-get install g++```

   ```sudo apt-get install libxml++2.6-dev libxml2-dev```

   ```sudo apt-get install libxslt1.1 libxslt-dev```

   ```sudo apt-get install sqlite libsqlite3-dev```

9. Install gem dependencies

   ```
   sudo gem install thin sinatra rack-accept rest-client sinatra-content-for nokogiri
   ```

10. Fetch and install the deltacloud dependencies

      ```sudo gem fetch deltacloud-core```

      ```sudo gem fetch deltacloud-client```

      ```sudo gem install deltacloud-core-<VERSION>.gem```

      ```sudo gem install deltacloud-client-<VERSION>.gem```

      If the installation of deltacloud-core throws an error, install deltacloud-client and afterwards install deltacloud-core again

11. Create a symlink for the launcher

      ```
      sudo ln -s /var/lib/gems/1.9.1/gems/deltacloud-core-1.1.3/bin/deltacloudd /usr/bin/deltacloudd
      ```

12. Start the deltacloud server by executing the following command

      ```
      deltacloudd -i mock -p <PORT> -r <IP-OF-THE-VM> -f cimi
      ```

      The IP-OF-THE-VM can be found by executing `ifconfig` (see `inet addr` of eth1)


The deltacloud server is now accessible under http://IP-OF-THE-HOST-ONLY-ADAPTER:PORT/
