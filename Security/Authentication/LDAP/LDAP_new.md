**LDAP**

1.  **LDAP Server**

    1.  **Overview**

> <img src="media/image1.png" style="width:4.81254in;height:2.40216in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="media/image2.png" style="width:4.47389in;height:1.23271in"
> alt="Text Description automatically generated with medium confidence" />
>
> <img src="media/image3.png" style="width:5.31789in;height:2.18965in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="media/image4.png" style="width:5.42602in;height:3.03358in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="media/image5.png" style="width:5.40025in;height:2.15779in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="media/image6.png" style="width:5.29442in;height:1.17541in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="/media/image35.png" style="width:5.1259in;height:1.58706in"
> alt="Text Description automatically generated with medium confidence" />
>
> <img src="media/image8.png" style="width:5.62503in;height:2.71997in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="media/image9.png" style="width:5.14239in;height:0.80982in"
> alt="A picture containing text Description automatically generated" />
>
> <img src="media/image10.png" style="width:5.41319in;height:2.61348in"
> alt="Graphical user interface, text, application Description automatically generated with medium confidence" />

2.  **Install OpenLDAP server**

> <img src="/media/image36.png" style="width:4.36997in;height:2.42636in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="/media/image37.png" style="width:4.17506in;height:0.69986in"
> alt="A picture containing graphical user interface Description automatically generated" />
>
> \# yum install -y openldap-clients openldap-servers oddjob-mkhomedir
>
> <img src="/media/image38.png" style="width:5.11023in;height:2.55894in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="/media/image39.png" style="width:4.84589in;height:1.58993in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="/media/image3a.png" style="width:5.0036in;height:2.29813in"
> alt="Text Description automatically generated with medium confidence" />
>
> <img src="/media/image3b.png" style="width:5.43504in;height:2.67223in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="/media/image3c.png" style="width:5.17626in;height:0.79911in"
> alt="Text Description automatically generated with medium confidence" />
>
> <img src="/media/image3d.png" style="width:5.55036in;height:2.64176in"
> alt="Graphical user interface, application Description automatically generated" />
>
> <img src="media/image19.png" style="width:5.87779in;height:0.84211in"
> alt="A picture containing text Description automatically generated" />
>
> <img src="media/image20.png" style="width:5.45165in;height:1.66462in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> \# setsebool -P allow_ypbind=1
>
> \# setsebool -P authlogin_nsswitch_use_ldap=1
>
> \# systemctl start slapd.service
>
> \# ss -lntu \| grep 389
>
> \# netstat -antup \| grep 389
>
> \# systemctl enable slapd.service
>
> \# systemctl start oddjobd
>
> \# systemctl enable oddjobd

3.  **Configure LDAP server**

> <img src="media/image21.png" style="width:4.57682in;height:1.71386in" />
>
> <img src="media/image22.png" style="width:5.5039in;height:2.50018in"
> alt="Graphical user interface, text Description automatically generated" />
>
> <img src="media/image23.png" style="width:3.96853in;height:0.81209in"
> alt="Text Description automatically generated" />
>
> <img src="media/image24.png" style="width:4.96231in;height:0.24024in" />
>
> <img src="media/image25.png" style="width:5.4646in;height:2.33609in" />
>
> <img src="media/image26.png" style="width:6.5in;height:1.81458in" />

<img src="media/image27.png" style="width:6.84213in;height:0.98904in"
alt="Graphical user interface, text Description automatically generated" />

<img src="media/image28.png" style="width:6.5in;height:1.05069in"
alt="Text Description automatically generated" />

<img src="media/image29.png" style="width:6.10784in;height:0.5762in" />

4.  **Set up LDAP database**

> <img src="/media/image3e.png" style="width:6.5in;height:0.52986in" />
>
> <img src="media/image31.png" style="width:5.63094in;height:0.42533in" />
>
> <img src="/media/image3f.png" style="width:6.5in;height:1.65468in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="/media/image40.png" style="width:6.5in;height:0.83194in" />
>
> <img src="media/image34.png" style="width:3.73635in;height:2.45619in"
> alt="Text Description automatically generated" />
>
> <img src="media/image35.png" style="width:6.5in;height:1.27569in"
> alt="Graphical user interface Description automatically generated with low confidence" />

5.  **Create an LDAP user**

> <img src="media/image36.png" style="width:4.55178in;height:2.98589in"
> alt="Text Description automatically generated" />

<img src="media/image37.png" style="width:6.28164in;height:0.91195in"
alt="Graphical user interface, text Description automatically generated" />

<img src="/media/image41.png"
style="width:7.15095in;height:0.51799in" />

<img src="media/image39.png" style="width:6.5in;height:0.24097in" />

<img src="media/image40.png" style="width:6.5in;height:0.39653in" />

6.  **Finish config**

<img src="media/image41.png" style="width:6.5in;height:0.96944in"
alt="Chart Description automatically generated with medium confidence" />

<img src="media/image42.png" style="width:5.39933in;height:0.3513in" />

<img src="/media/image42.png" style="width:4.62223in;height:0.72196in"
alt="Text Description automatically generated" />

<img src="/media/image43.png" style="width:6.05755in;height:0.98435in"
alt="Text Description automatically generated" />

2.  **Setting up an LDAP client**

    1.  **Install LDAP client**

> <img src="media/image45.png" style="width:5.73881in;height:0.3783in" />

2.  **Configure by CLI**

> <img src="media/image46.png" style="width:6.5in;height:0.47708in" />
>
> <img src="media/image47.png" style="width:6.5in;height:0.71042in" />

3.  **Configure by graphically**

> <img src="media/image48.png" style="width:6.5in;height:0.19028in" />

<img src="media/image49.png" style="width:4.76845in;height:3.70101in"
alt="Graphical user interface, text, application, chat or text message Description automatically generated" />

<img src="media/image50.png" style="width:5.6875in;height:6.97917in"
alt="Graphical user interface, application Description automatically generated" />

<img src="media/image51.png" style="width:5.6875in;height:6.85417in"
alt="Graphical user interface, text, application Description automatically generated" />

<img src="media/image52.png" style="width:5.63542in;height:6.90625in"
alt="Graphical user interface, application Description automatically generated" />
