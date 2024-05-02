Windows Server Security

1.  Server Hardening

    1.  Cryptography

> <img src="/media/image1a.png" style="width:4.34646in;height:0.73973in"
> alt="Text Description automatically generated" />
>
> <img src="/media/image1b.png" style="width:4.2126in;height:1.07835in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="/media/image1c.png" style="width:3.97638in;height:1.1585in"
> alt="A picture containing diagram Description automatically generated" />
>
> <img src="/media/image1d.png" style="width:4.71986in;height:1.77953in"
> alt="Graphical user interface, text, application, email Description automatically generated" />

2.  Public key configuration

> <img src="/media/imagea.png" style="width:4.97638in;height:1.79224in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="/media/imageb.png" style="width:4.2015in;height:2.3023in"
> alt="Text Description automatically generated" />
>
> <img src="/media/imagec.png" style="width:4.57431in;height:1.60736in"
> alt="Graphical user interface, text, application Description automatically generated" />
>
> <img src="/media/imaged.png" style="width:4.5748in;height:1.64175in"
> alt="Graphical user interface, text, application, email Description automatically generated" />

3.  EFS Overview

> <img src="/media/image1e.png" style="width:5in;height:2.44792in" />

John is going to take that file and he put it in a box. Now once that
data is in the box, he is going to use a symmetric encryption key, which
in the case of EFS is called a FEK (File Encryption Key), he‘s going to
lock the box or encrypt the data using that symmetric key.

<img src="/media/image1f.png" style="width:5in;height:2.55208in" />

There are 3 boxes that are going to be attached to the box with the file
in it, 3 little boxes at the header. There’re 3 of them because John is
going to make 3 copies of that FEK, that one symmetric key, and put one
in each box, then he’s going to encrypt 1 box using his own public key.

<img src="/media/image10.png" style="width:5in;height:2.53125in" />

Then he‘s going to encrypt another box, or lock another box, using
Mary’s public key. John needs to have access, Mary needs to have access,
third box is for EFS recovery agent. The third box is then encrypted or
locked using the recovery agent’s public key.

<img src="/media/image11.png" style="width:5in;height:2.54167in" />

These little boxes are actually known as headers that are attached to
the file and the 2 that had John’s key and Mary’s key in it, those are
known as DDF (Data Decryption Fields) fields, and the one with the
recovery agent called the DRF (Data recovery field)

<img src="/media/image12.png" style="width:5in;height:2.41667in" />

<img src="/media/image13.png" style="width:5in;height:2.41667in" />

John goes to access the data, John would go ahead and grab his own
private key and he would unlock the one data decryption field that was
originally encrypted using his public key, that way the key pair
actually fits, and then he can take out that file encryption key and use
it to unlock or decrypt the big box that has the data in it and then
John gets access to the data.

Now Mary could do the same thing, or the recovery agent could do the
same thing because they have their own private key that would match up
with a public key that was used to originally encrypt one of the header
fields.

If another user comes up to access this data, they’re going to find 4
locked boxes and they don’t have the key that would unlock any of these
4 locks, because you need a specific private key, for the 3 locks, which
is in the headers field, and need to file encryption key, the symmetric
key, to open the box and the only copies of those, they’re locked in the
header fields.

1.4. Implementing EFS

- EFS \> Properties \> Advanced \> Encrypts contents to secure data

<!-- -->

- View \> Options \> Change folder and search options \> View \> Show
  encrypted or compressed files in color

<!-- -->

- Add User: EFS \> Properties \> Advanced \> Encrypts contents to secure
  data \> Details \> Add

1.5. Malware protection

- Any type of malicious code intended to harm your environment.

<img src="/media/image14.png" style="width:5in;height:2.69792in" />

- Viruses: a form of malware to where executable code, a malicious
  executable code, is embedded into either an application or OS files,
  sometimes just within data, it can even get into some of your hardware
  components like BIOS or boot sector on your hard drive.

- Worms: self-propagating, a user actually doing anything or clicking on
  anything to get the virus to spread from one system to another. A worm
  can actually hop from 1 computer to another across the network all by
  itself.

- Trojan horses: looks like something friendly or looks like something
  favorable or fun or something you’d like to have. It presents itself
  as something that you want to have, and then as soon as you invite it
  in and open it up, it’s actually malicious software. They come in the
  form of an email, and that email will come from somebody else you know
  (inside or outside the company), open up the attachment (malware).

- Ransomware: nastiest form of malware, come in the form of a Troạn
  horse, but it doesn’t have to. When you get hit with some form of
  ransomware, what that software will do is will lock you out of system,
  you ‘ll just get a message on screen “U’ve been locked out”. System is
  held for ransom. What the malware will do is it will come in and it
  will encrypt all your data using a public key of the owner of the
  ransomware.

- Spyware: software that’s put in on your system, put on your networks
  to watch what you’re doing. It just gathers information about you. It
  doesn’t necessarily damage anything.

<!-- -->

- Windows Defender is a bult-in malware protection tool.

2.  Secure the Network

2.1. Network Security Threats

<img src="/media/image15.png"
style="width:5.34375in;height:3.00586in" />

- DDoS attacks (distributed denial of service attacks): attack that does
  not damage your data or steal your data, but just simply focuses on
  inconvenience and taking down some of your service. For instance, a
  web server either be really slow or shutdown altogether so that your
  customers aren’t happy with you or aren’t able to gain your services,
  and this is done by an attacker pretty much putting both software out
  on many different computers, sometimes referred to as zombie computers
  out on the internet and then giving instruction for them all at once
  to just simply make a request of your web server to where it gets
  inundated it has an inability to be productive the way you need it to
  be.

- Malware

- Man-in-the-middle attacks: occur when a malicious hacker can intercept
  your network traffic, examine it or possibly even modify it, and then
  send it on to its intended destination. In the middle of the
  conversation, and in some cases, a man-in-the-middle attack is just
  there to intercept your information and just gather information. In
  some cases, user A sends some information out to user B, now we have a
  man-in-the-middle attacker who grabs the information and then
  manipulates it, and says something different to user B who then
  responds to that information and then, again it’s captured and
  converted again before sending it back to user A.

It’s to completely control the conversation and sometimes grab hold of
even more secure information than what otherwise would’ve been
transmitted.

<img src="/media/image16.png"
style="width:5.26042in;height:2.86035in" />

2.2. Windows Firewall & advanced security

\- Search \> Windows Defender Firewall with Advanced Security

- Inbound rules: which help control data that’s coming in

- Outbound rules: which has to do with data that’s leaving the system
  and then we have some connection-specific security rules

- Monitoring

- Right click Inbound rules \> New Rule \> Custom \> ICMPv4 \> Customize
  \> Specific ICMP types \> Echo Request (ping) \> Allow/Block
  Connection \>

<img src="/media/image19.png" style="width:5in;height:2.35417in" />

- ALG: operate at the application layer, acts as an endpoint, for
  communications from internet-based clients to internal applications.
  The gateway will accept the connection, examine the network packet for
  malicious content, then establish the connection to the internal
  application. Firewalls that understand applications can examine the
  actual contents of the application layer traffic and decide whether to
  accept that traffic based upon the contents of the packet.

- CLG: operates at the session layer and monitors the datagrams between
  communicating hosts to verify that requested sessions are legitimate.
  CLG monitors the TCP hand-shaking process that is used to establish
  TCP sessions between hosts and determine whether the session is
  legitimate. Now, the common name is PROXY server. PROXY allows
  responses from the Internet to requests made by internal clients while
  blocking unsolicited requests that come in from the Internet. Also the
  information that is passed from your network out to the Internet
  appears to originate from the actual PROXY server, not from the
  legitimate IP address of the internal client.

- PAcket filter: operates at the Network layer, implementing in consumer
  markets as just part of the routers that are out there. We have cable
  modem, DSL router very often packet filtering is built in. Packet
  filter is itself filtered and compared with an action list to
  determine what to do with that packet, whether it’s an allow or
  blocking packet,

- SMLI: combines the aspects of all the other 3 firewall types for
  helping provide a high level of security, multi-layers, operates at
  all different layers, so it has the ability to go through all the
  different aspects of these different types of gateways, and really
  give a high level of protection.

<img src="/media/image20.png" style="width:5in;height:1.88542in" />

<img src="/media/image21.png" style="width:5in;height:2.11458in" />

<img src="/media/image22.png" style="width:5in;height:2in" />

<img src="/media/image23.png" style="width:5in;height:0.96875in" />

- NC: provides centralized management, configuration, monitoring, and
  troubleshooting of both your virtual and physical network
  infrastructure

- HVV: to abstract applications and workloads from underlying physical
  network by using virtual networks.

- HVS: to connect VMs to both virtual networks and physical networks.
  Provides security, isolation and service level policy enforcement.

- Routing & remote access MTG: extend network boundaries to Azure or
  another provider to deliver an on-demand hybrid infrastructure.

- NIC: to configure multiple network adapters as a team for bandwidth
  aggregation and traffic failover to guard against the loss of
  connectivity if having a specific network component failure.

- MOM: provides infrastructure monitoring for DC, and for private and
  public clouds.

- VNM: provision and manage virtual networks as well as providing
  central control of virtual network policies that link to applications
  or workloads.

- GW: virtual software router and gateway that allows U to route DC and
  cloud traffic between virtual and physical networks.

<img src="/media/image24.png" style="width:5in;height:1.23958in" />

Configure, monitor and troubleshoot

<img src="/media/image25.png" style="width:5in;height:2.95833in" />

- NC allows you to automate the configuration of both physical and
  virtual network infrastructure, including Datacenter Firewall

<img src="/media/image26.png" style="width:5in;height:0.97917in" />

Use in Hyper-V environments.

<img src="/media/image27.png" style="width:5in;height:2.88542in" />

DF acts as a distributed multitenant firewall that’s built into the
Hyper-V environment. As a component in the Hyper-V infrastructure, DF
can help protect any host VM, regardless of OS.

<img src="/media/image28.png" style="width:5in;height:2.04167in" />

<img src="/media/image29.png" style="width:5in;height:1.67708in" />

<img src="/media/image2a.png" style="width:5in;height:1.09375in" />

<img src="/media/image2b.png" style="width:3.73958in;height:5in" />

An NSG contains an ACL rule, that either allows or denies traffic to or
from a virtual subnet or a VM. These rules are applied at the VM level
with separate rules for inbound and outbound traffic.

<img src="/media/image2c.png" style="width:5in;height:1.77083in" />

Provide security for internal resources. You can easily expand the
design. If U want to expand the network, such as adding a development
subnet, you could create a new NSG and then create new DF rules.

2.3. IPSec

\- Can help protect data in transit through a node by providing
authentication, integrity checking and encryption. It provides better
security than some other methods like TLS, SSH which only provide
partial protection. All of the network traffic between any specified
hosts is going to be protected by IPSec.

\- Is a protocol suite that allows secure, encrypted communication
between 2 computers.

\- Uses for IPSec:

\- Authenticate and encrypt host-to-host traffic, used as secure
communications between the hosts in our network

\- Authenticate and encrypt traffic to specific servers

\- Use L2TP/IpSec for VPN connections because IPSec layer 2 Tunneling
protocol

\- Site-to-site tunneling: to create a VPN, or tunnel between 2
locations within your organization

- Enforce logical networks: refer to domain or server isolation

<img src="/media/image17.png" style="width:5.59375in;height:2.086in" />

<img src="/media/image18.png"
style="width:5.59211in;height:1.77083in" />

Configure IPSec:

- Use GPOs or firewall rules

- Predefined IPSec policies for the GPO method

  - Client (Respond Only): set up your clients so if they end up needing
    to communicate with another server that’s calling for IPSec, it will
    be able to respond accordingly.

  - Server (Request Only): request security, if you’re going to initiate
    communiation, ask for IPSec secure communication. If the other side
    is not equipped, then go ahead and use the less secure
    communication. Trying to improve security where you can but not
    preventing communication if you can’t.

  - Secure Server (require Security): the one truly requires IPSec
    communication

2.4. Implementing IPSec

\- Windows Defender Firewall with Advanced Security

\- Inbound Rules \> New Rule \> Custom \> All Programs \> ICMPv4 \>
Customize \> Echo Request \> Allow the connection if it is secure \>
Allow Secure Ping

\- Connection Security Rules \> New Rule \> Server-to-server \> Require
authentication for inbound and outbound \> Advanced \> Customize \> Add
\> Preshared Key (Secret-Key) \> Secure Server to Server

\- Ping again

\- Security Associations: Main mode, Quick mode

2.5. Configure DNSSec

\- DNS Manager \> Forward Zone \> Primary Zone

\- New Host \> Add Host

\- PowerShell \> Resolve-DnsName \<hostname.zone\> -dnssecok

\- Right click \<zone\> \> DNSSEC \> Sign the zone \> Customize \>
Keymaster \> Add Key Signing Key \> Add Zone Signing Key \> Zone Signing
Wizard \> Next Secure (NSEC) \> Trust Anchors (TAs) \> Enable \> Signing
and Polling Parameters.

\- PowerShell \> Resolve-DnsName \<hostname.zone\> -dnssecok again

2.6. Microsoft Message Analyzer & Secure Server Message Block traffic
(SMB)

\- SMB shares, your typical file shares are not encrypted and can be
easily viewed using a tool like MMA

\- Need to enable SMB encryption on our SMB shares to protect more.

\- Windows PowerShell \> New-SmbShare –Name “SecureSMB” -Path
“c:\SecureSMB” -EncryptData \$true

Grant-FileShareAccess –Name SecureSMB –AccountName “Everyone”
-AccessRight Full

- Open MMA, Start Local Trace

<img src="/media/image2d.png" style="width:5in;height:0.76042in" />

3.  Secure File Services

3.1. Install File Server Resource Manager

\- Set of tools that allows you to understand, control and manage the
quantity and types of data that is stored out on your servers.

\- Add Roles and Features \> File Server Resource Manager

\- Tools \> File Server Resource Manager

3.2. Quota Templates

\- Help to control the quantity of data that is allowed to be stored on
your servers.

\- Create a Quota Templates, \> Quota Templates \> Template name \> Hard
Quota \> Add Threshold \> 100\> Event Log \> Send warning to event log

3.3. Create a Quota

\- Quotas \> create quota \> Browse \> QuotaLimited(created) \> Auto
apply template and create quotas on existing and new subfolders \> 100MB
limit (new) \> create

\- QuotaLimited \> New Folder \> Powershell \> cd C:\quotalimited\demo
\> fsutil file createnew demo1.txt 89400000 \> refresh

\- fsutil file createnew demo2.txt 16400000 (not enough space)

3.4. File Screening

\- File screening management \> file groups \> create file group \> MPx
Media Files \> \*.mp\* (include) \> \*.mpp (exclude)

\- File Screen Templates \> Create \> Block MPx Files \> MPx Media Files

\- File Screens \> Create \> Browse \> FileScreen \> Block MPx Files \>
create

\- create Demo3.mp3 in FileScreen (permission denied), change to .mpp
(successful)

4.  Manage Privileged Identities

4.1. User rights

\- Group Policy management \> Forest \> Domain \> DC \> Default DC
Policy \> Edit \> Policies \> Windows Settings \> Security Settings \>
Local Policies \> User Rights Assignment \> Allow log on locally \> Add
User and Group \> Browse

4.2. Delegate privileges

\- AD users and computers \> Domain \> Users \> Delegate Control \> Add
\> Delegate common/custom tasks

\- View \> Advanced Features \> Users \> Properties \> Security \>
Advanced \> Add \> Select a principal

4.3. Create a taskpad

\- mmc (management console) \> File \> Add/Remove Snap-in \> Add AD
users and computers \> Users \> New Windows from Here (just for Users)
\> New Taskpad View \> Horizontal list \> Selected tree item \> Reset
Passwords

\- New Task \> Menu Command \> Reset Password \> Icon

\- Click on Administrator user \> Reset Password

\- View

4.4. Password Policies

\- GPME \> Computer configuration \> Policies \> Windows Settings \>
Security Settings \> Password Policy

\- Enforce Password history: how many different passwords will be
remembered that the user would have to use before they could reuse the
same password again. How many passwords are remembered?

\- Max/Min password age: longest/shortest that a user can hang on to
their password before they are forced to have to reset it.

\- Min password length: how long must our passwords be?

\- Password complexity: Explain (complexity requirements)

4.5. Account lockout policies

\- Security Settings \> Account Policies \> Account Lockout Policy

\- Account lockout threshold: how many consecutive wrong passwords can
be entered before an account gets locked out. Protecting against
somebody guessing at somebody’s password.

\- Account lockout duration: once an account has been locked out, how
long it will stay locked out

\- Reset account lockout counter after: Cài đặt policy Reset account
lockout counter after giúp xác định số phút trôi qua trước khi tài khoản
của bạn bị khóa. Thiết lập lại số lần cố gắng đăng nhập về 0 sau một
khoảng thời gian quy định. Thiết lập này chỉ có hiệu lực khi “Account
lockout threshold” được thiết lập.

Ví dụ, bạn có thể đặt Account lockout threshold thành 5 lần thử và
policy Reset account lockout counter after thành 5 phút. Điều này sẽ
cung cấp cho người dùng 5 lần nhập mật khẩu trong vòng 5 phút trước khi
tài khoản bị khóa.

5.  Configure Advanced Audit Policies

5.1. Audit Policy

\- Group Policy Management \> Forest \> Domain \> Default Domain Policy
\> edit \> Computer Configuration \> Policies \> Windows Settings \>
Security Settings \> Local Policies \> Audit Policy \> Audit object
access \> Define these policy settings \> Success/Failure

5.2. Audit object access

\- Create a folder Audited Info. To audit people accessing this folder,
\> Properties \> Security \> Advanced \> Auditing \> Add \> Select a
principal \> Everyone \> Type/Applies to

5.3. Manage advanced audit policy

\- Advanced Audit Policy Configuration \> Audit Policies

6.  Secure Virtualization

<img src="/media/image2e.png"
style="width:5.61458in;height:3.39214in" />

<img src="/media/image2f.png" style="width:5.6295in;height:3.26042in" />

<img src="/media/image30.png" style="width:5.4797in;height:3.09375in" />

<img src="/media/image31.png"
style="width:5.45833in;height:1.99002in" />

<img src="/media/image32.png"
style="width:5.53942in;height:2.78125in" />

<img src="/media/image33.png"
style="width:5.38462in;height:2.77083in" />

<img src="/media/image34.png"
style="width:5.51724in;height:1.33333in" />

<img src="/media/image35.png"
style="width:5.52817in;height:3.27083in" />

<img src="/media/image36.png"
style="width:7.14748in;height:3.76732in" />

<img src="/media/image37.png"
style="width:5.59361in;height:2.55208in" />
