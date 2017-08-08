### Lenovo Thinkpad T430
Now start.
 
Before installing fprint, make sure your hardware is supported, you can see the list on here.

    http://www.thinkwiki.org/wiki/Integrated_Fingerprint_Reader

Wiki ```fprint``` on Arch 

    https://wiki.archlinux.org/index.php/fprint    

Check ``` lsusb ```  first, on my machines: 

![Screenshot](img/lsusb.png)


Bus 001 Device 003: ID ```147e:2020``` Upek TouchChip Fingerprint Coprocessor (WBF advanced mode)
![Screenshot](img/thinkwiki.png)

### Install Fprint:
    $sudo pacman -S fprintd 
    
 ``` imagemagick ``` might also be needed. 

Configuration:

    $sudo su
    #groupadd plugdev
    #gpasswd -a yourusername plugdev
    #chgrp -R plugdev /dev/bus/usb/

Now set your finger:
For User:

    $fprintd-enroll
For Su:

    $su
    #fprintd-enroll
 
You will be asked to scan the given finger. Swipe your right index 
finger five times. After that, the signature is created in /var/lib/fprint/. 

Then now modify ``` /etc/pam.d/... ```
 
For Login gdm/kdm:
 
Modify: login
 
    $sudo vim /etc/pam.d/login
    
add this
 
     auth required pam_env.so
     auth sufficient pam_fprintd.so
     auth sufficient pam_unix.so try_first_pass likeauth nullok
     auth required pam_deny.so
     
     #auth required pam_securetty.so
     # ...
     
And for ``` /su```, ``` /sudo``` same as above.

      $sudo vim /etc/pam.d/su
      $sudo vim /etc/pam.d/sudo  
      
OK. Now try fingerprint.
### My login
![Screenshot](img/mylogin.jpg)

![img](https://gifs.com/?source=https://www.youtube.com/watch?v=XJMl-YN3yOY&feature=youtu.be)

### Other config
- ```Thinkfan``` [my-dotfiles](https://github.com/duyhenryer/dotfiles/blob/master/thinkfan.conf)  
     
     
  
  