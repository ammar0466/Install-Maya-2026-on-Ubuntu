# Install Maya 2026 on Ubuntu 22.04
Step to Install and running Autodesk Maya 2026 on Ubuntu

1. Install Package :
    ```
    sudo apt update
    sudo apt install -y libaudiofile1 libxss1 libgconf-2-4 libxrandr2 libxcursor1 libxcomposite1 libxdamage1 libxfixes3 libxi6 libxrender1 libxtst6 libxxf86vm1 libgl1-mesa-glx libglu1-mesa libegl1-mesa libxkbcommon-x11-0 libxkbfile1 libxmu6 libxpm4 libxaw7 libxinerama1 libfontconfig1 libfreetype6 libxft2 libxss1 libgconf-2-4 rpm alien
    ```

2. Download Maya 2026, later will need to convert .rpm to .deb

    <img width="1478" height="795" alt="Pasted image 20250714140816" src="https://github.com/user-attachments/assets/b0595294-d05c-491c-a455-f8f81262f5ff" />

3. Extract file :

    ```
    mkdir maya2026
    tar -xzf Autodesk_Maya_2026_1_Update_ML_Linux_64bit.tgz -C maya2026
    cd maya2026/
    
    
    ```
4. Convert

   ```
   sudo alien -vc *.rpm
   ```

5. Install licensing :
    ```
    sudo dpkg -i adlmapps31_31.0.4-1_amd64.deb
    sudo dpkg -i adskflexnetclient_11.18.3-2_amd64.deb
    sudo dpkg -i adskflexnetserveripv6_11.19.4-2_amd64.deb
    sudo dpkg -i adsklicensing15.1.0.12339_0-1_amd64.deb
    ```

6. Install adODIS (It comes in Maya extracted package), this package is dangerous, you need to careful read the term and condition, and force you to accept. :

    ```
    ./AdODIS-installer.run
    ```

7. Install dummy webkit2gtk3

    Can create own .rpm package by using tutorial found on autodesk forum or use mine download from this repo.

    Install these package :

    note: Don't use libwebkit2gtk-4.1
    ```
    sudo apt install libwebkit2gtk-4.0-37
    sudo apt install libwebkitgtk-6.0-4
    ```

    ```
    sudo rpm --define "_dbpath /var/lib/rpm" -ivh --nodeps --force webkit2gtk3-1-0.x86_64.rpm
    mkdir -p /etc/rpm
    ```

    ```
    echo '%_dbpath /var/lib/rpm' | sudo tee /etc/rpm/macros
    %_dbpath /var/lib/rpm
    ```

    Need to test if rpm called success :
    ```
    rpm -q webkit2gtk3
    ```
    Show :
    ```
    webkit2gtk3-1-0.x86_64
    ```

8. Create symlink for tls cert
   because maya is try to check cert on `/etc/pki/tls/certs` but on Ubuntu it on different path `/etc/ssl/certs/`
   ```
   mkdir -p /etc/pki/tls/certs
   ln -sf /etc/ssl/certs/ca-certificates.crt /etc/pki/tls/certs/ca-bundle.crt
   ```

9. Install Maya 2026
   ```
   sudo dpkg -i maya2026-64_2026.1-4785_amd64.deb
   ```

10. Run maya


    ## P/s :
    
    If still cant run, something you can try :
    
    install adskIdentityManager, but adODIS should automatic handle this.
    
    remove and reinstall adsklicensing.
    
    restart machine.
    
    set your default browser to google-chrome.
    
    after launch maya launch google-chrome also.

