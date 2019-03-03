title: "Linux commands"
date: 2015-01-02 13:57:59
tags: Linux
categories: DevOps
---

**Here is a collection of the Linux commands I used but always forget.**


* Check the system 64 or 22 bit:  
  `getconf LONG_BIT`

* Check space usage:  
  `df -h`

* Check processes:  
  `ps ux ` or `ps -ef` or `lsof -n -i`

* Kill a process:  
  `kill -9 PID`

<!--more-->

* Check Ubuntu version  
  `$cat /etc/lsb-release`

* Check folder size  
  `du -sh /PATH_TO_FOLDER`

* Display information about the contents of ELF files  
  `readelf -h libname.a`

* To create a soft link  
  `ln -s /full/path/of/original/file /full/path/of/soft/link/file`

* To remove all the .svn files from the previous version control system  
  `find . -name .svn -exec rm -rf {} \;`

* `CTRL + ALT + F7` for switching to gui, `CTRL + ALT + F1` to switch to CLI.

* Put down/up interface "eth0"
  `sudo ifconfig eth0 down/up`

* Keep runing after exit,
  refer http://en.wikipedia.org/wiki/Nohup
  `nohup sth &`

* Get a list of packages installed locally,
  refer http://askubuntu.com/questions/17823/how-to-list-all-installed-packages
  `dpkg --get-selections | grep -v deinstall`

* Analysis tcp transport via "eth0" interface on port 1883,
  refer https://danielmiessler.com/study/tcpdump/
  `sudo tcpdump -i eth0 port 1883 -XX`

* Sort the files by size
  `du -sh * | sort -h`

* Remove old files, filtered by year
  `ll | grep 2015 | awk '{print $9}' | xargs rm`

* Apache HTTP server benchmarking load test
  `ab -n 10000 -c 100 http://localhost/`

* Show full path in the Finder window
  defaults write com.apple.finder _FXShowPosixPathInTitle TRUE
  killall Finder
