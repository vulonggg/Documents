**Package management**

1.  **Linux Software Overview**

    1.  **Downloads packages & install**

- Contents of a Package

  - Binary programs

  - Data files

  - Metadata about the programs

  - Scripts that run during installation/uninstallation

- Package naming format: zip-3.0-11.el7.x86_64.rpm

  - Program name (zip)

  - Major/Minor version (3.0)

  - Package release num (11)

  - OS type (el7)

  - Processor Architecture (i386, i686, x86_64)

  - Software package format (rpm)

  1.  **Install from a software repos**

- File server with software packages

- Index of packages

- Meta-data about packages

- Public key

- Server on the network

- Uses FTP or HTTP protocol

- Could be hosted on several OSs

- Easiest for the host and client to be alike

  1.  **Install from a source code**

- A listing of computer instructions usually stored as plaintext

- Steps:

  - Download source code

  - Install Development Tools

  - Install associated source files

  - Compile Software

  - Install Software

  1.  **Why multiple package formats?**

\`<img src="media/image1.png" style="width:5.60115in;height:3.0178in"
alt="Table Description automatically generated" />

<img src="media/image2.png" style="width:5.76817in;height:3.12566in"
alt="Table Description automatically generated" />

2.  **Package management systems**

- apt, yum, zypper, ...

> <img src="media/image3.png" style="width:5.53477in;height:2.98736in"
> alt="Table Description automatically generated" />

2.  **Manage packages with RPM**

> <img src="media/image4.png" style="width:5.37524in;height:1.67345in"
> alt="Graphical user interface, text, application Description automatically generated with medium confidence" />

1.  **RPM Query**

> \# rpm -qa Query all packages
>
> \# rpm -qa \| sort Query all packages and sort
>
> \# rpm -qi bash Query information
>
> \# rpm -qa Group=”System Environment/Shells”
>
> \# rpm -qa –last
>
> \# rpm -ql yum query list of file
>
> \# rpm -qd yum query documentation
>
> \# rpm -qc yum query config files
>
> \# rpm -qf /bin/bash query file for bash
>
> \# rpm -qdf query document for bash
>
> \# mkdir /tmp/packages
>
> \# yum install –downloadonly –downloaddir=/tmp/packages \<package\>
>
> \# rpm -qlp \<package\> query list of files in packages and where
> installed
>
> \# rpm -qip query database of packages

2.  **Install/remove packages**

> \# rpm -ivh \<package\> install with verbose & hashes
>
> \# rpm -ev \<package\> remove

3.  **Upgrade/Verify integrity packages**

> \# rpm -Uvh \<package\> upgrade
>
> \# rpm -K \<package\> Key
>
> \# rpm -q gpg-pubkey
>
> \# rpm -qi \<key\>

4.  **Troubleshoot RPM**

> \# rpm –rebuilddb rebuild DB
>
> \# rpm –setperms put permissions back

3.  **Manage Packages with Yum**

> <img src="media/image5.png" style="width:4.92848in;height:2.90707in"
> alt="Graphical user interface, text, application, email Description automatically generated" />

1.  **Search**

> \# yum search \<\>
>
> \# yum list all \| grep \<\>
>
> \# yum list available \<\>

2.  **Install/Remove**

> \# yum install \<\>
>
> \# yum localinstall \<\> install local package
>
> \# yum reinstall \<\>
>
> \# yum remove \<\>
>
> \# yum autoremove \<\> remove dependencies
>
> \# yum group install \<\>
>
> \# yum group update

3.  **Manage OS updates**

> \# yum check-update
>
> \# yum update
>
> <img src="media/image6.png" style="width:4.54748in;height:2.15082in"
> alt="Text Description automatically generated" />

4.  **Yum Clients**

    1.  Configure yum clients

> <img src="media/image7.png" style="width:4.78689in;height:2.72024in"
> alt="Graphical user interface, text, application, email Description automatically generated" />

2.  **Manage Repositories**

> \# cd /etc/yum.repos.d/
>
> \# yum repolist
>
> \# yum repolist enabled/disabled
>
> \# yum repoinfo
>
> \# yum –disablerepo=”\*” --enablerepo=”centosplus” list available
>
> \# yum –disablerepo=”\*” --enablerepo=”centosplus” install golang

3.  **Troubleshooting yum**

> <img src="media/image8.png" style="width:5.46474in;height:2.03176in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="media/image9.png" style="width:5.39457in;height:3.19121in"
> alt="Graphical user interface, text, application, chat or text message Description automatically generated" />
