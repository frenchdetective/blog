---
title: "Welcome to Jekyll!"
date: 2019-04-18T15:34:30-04:00
categories:
  - blog
tags:
  - Jekyll
  - update
---
# 1. Firewall configuration

# Opnsense 

First, we need to configure our vmware virtual network adapters.

![](assets/K6DmcQ6E1skxwMTRU2VpPgWjcavKEkYpCYET6f-gob0=.png)

At the bottom, click on "Change settings" as this requires administrator privileges.

![](assets/BaVx9JHZN-_o5bU4kXcAhwLOWnX76WnPY6gjQLQmM0E=.png)

Configure two VMnets for our needs, here vmnet0 will be for the WAN and vmnet1 for the LAN.
Vmnet0 is bridged, so the WAN network of our firewall will have it's own IP address on the router but will pass trough the network interface of our host PC.


If DHCP is activated on your internet router, it will assign an IP automatically in the same subnet of your PC. Otherwise you will have to configure the IP manually, we will see that later.

![](assets/3I1vSYd_MEvCho72_gYsqYyr072qzzi2drsX31EhB78=.png)

If we want to avoid to be considered as a potential sandbox, we need to change the ip 192.168.153.0 as it's reserved for local networks ([RFC1918](https://datatracker.ietf.org/doc/html/rfc1918))

![](assets/DSPjX-F6nmS9GqRuEdtGXX9UzLzJE6_og0nSyoY4N5A=.png)

Let's install the Opnsense Virtual machine.

Download the latest **Opnsense** image:
https://opnsense.org/download/

![](assets/QKnnw9wQ4sTAyCtgG6XwIk8KN7L_OPwBxWFYf2E2gRs=.png)

Extract the file with 7-Zip in your desired folder.

![](assets/GH14ihIrGVlcR7Iw_XAemt81E1UlciiyM9cftdR-MsU=.png)

On **Vmware Worstation**, we have to create a new virtual machine and configure it correctly.
Press Ctrl+N to create a VM:

Select Custom.

![](assets/cYMvHTswTsLmbZN55k-OQE0kZY9ya3NWjiUge7IirQU=.png)

Default selection is ok.

![](assets/AK5DlN-lrGhj-dPuiWbk39QWzXUW3b38YggEvV60Sl8=.png)

Select the iso you extracted and click next.

![](assets/kCJLdSqyfVVkNN0_6CXxHqQa1riRWjW347_xL10bmmE=.png)

Name you machine (Firewall) and select where you want to put the files of the vm.

![](assets/mglh8j_RyhlOksA4smI0i7KoOy8-MJwuUGnaJsKK5XY=.png)

I choose 2 cores but 1 could be ok as we go for a little homelab, we can change it later if we need to.

![](assets/dEWI2AQZzIsR288loewm-jn6lRWKSyiDDBbWKHD6JLg=.png)

4Gb of RAM is needed to install opnsense correctly.

![](assets/Pkly5IiZFoWd9vOpIDbX4zOFtpBEKWetiSNZKC9x24M=.png)

Add a bridged networking, but we will use vmnet0 and vmnet1 that we configured after, to have specific virtual adapters dedicated to this homelab.

![](assets/POclHgqnRfItJ-p6osGekkHuFuMu6HsWwF7C_xeJH9U=.png)

![](assets/kXunK2OslyjKhzIXRnd7R7ecMl7huPkcAbWgXFGkSpU=.png)

![](assets/Vfpx3AbfsDk-9WUBs-GG-jS2foHrXxGXWf9lygyauh4=.png)

![](assets/ItsFGMKHC5h3luEVhx_XrvDBi4qTcZzXOU-QI6CipS0=.png)

20Gb of disk drive is fine.

![](assets/QVEsCaOOPi0xCEJ0NiaBk_0Ff_-PP70lB1qpHNVIg80=.png)

![](assets/C3z8g29aWqq7_B0fW1jUAW6OvTZtR7hm8ypcxE4DpDM=.png)

![](assets/lFua9APVk286kj2S_MElbC9qj6vds-sKAD3l68gY2y8=.png)

Let's configure our network virtual NICs

![](assets/Crd-dIitHypkEhXY_3PZZNpomOZlihbODKv1Tr_PSV8=.png)

![](assets/gC7hZ1-hYy0uqspIFX3c_kyHUWy3RovSQg89Ee-Pngc=.png)

Selecto the first adapter and choose Custom: Specific virtual network.
Then select VMnet0

![](assets/lLtkgBvyNG326dkr3OuGvs-L3-Ztbr8hmpri_fMFps4=.png)

Select the second adapter and choose the VMnet1 (Host-only)

![](assets/vDTPgyqmy3HIh4Zl0Q-B0a9UM3yVntW-iEV8SHPuU_0=.png)

Power on the virtual machine.

![](assets/cCnGKazJ2YRPj4lTBIy5j4NBioRgGhBExopJLW-c_QQ=.png)

Let the initialization begin.
Enter the login "installer" and the password "opnsense".

![](assets/FAhksv_otTGTlT3Ux8JwcsBh1eYvgMeS9uya67nnwaY=.png)

If you need to change your keyboard layout. Otherwise choose to continue with the default one.

![](assets/_m0l-oAwIonqlEsIMrzJ_zsPTD8Cj4LPONQQaMnjTXM=.png)

ZFS filesystem is the best option.

![](assets/y_7sIERxHIhh3oMNXcrtQGjIw6QV-8Fue7_N4ARiMB8=.png)

Partitioning, choose stripe.

![](assets/Tl50LfVS0j7XLxZ7L8pDeQxD5qAi1qNGOzHdSGdxAcg=.png)

No choice here lol, press space to choose the disk and press enter.

![](assets/NVVzkmbfstZHGs7ZCfnblxLr8Hi2sf92nc_Jk23F5Vc=.png)

Confirm.

![](assets/daBZnMNDcOJYndRDdhsR8-GIUHL95PMGjU1YraQknDk=.png)

![](assets/tyPbTt6F7mq0JgIDYKvPY93V1dE5TA6CJMoIQ-Zc5HU=.png)

Let's configure a strong password for root user.

![](assets/OaKCkr1e_wi3Ma2lyj4pHfbgfx_OV0cmtfb_1_pxGH8=.png)

![](assets/vzdLwuEiz5wA_wqRJ5k9j3TJ3Mb4UNceYe-eKQWhrJI=.png)

Confirm and then reboot opnsense.


Login as root with your password

![](assets/XIkgKglE9SP5YC7YeHK0_88CVYq2YBD32x14C4p8eU4=.png)

![](assets/shFJhxTdIuP0-53AzrN40i60vRXAqSoJNQe5oGfa5F0=.png)

![](assets/EQFDXR7lQx1VNlTmkGLxfeK-VY1lHuWaGNX_NuLKF-4=.png)

Now we need to choose the network interface for WAN and for LAN
As we have only the MAC addresses here, we have to verify our configuration in the VM settings in Vmware.

![](assets/kpyOYpncRpefn2uUFdTcyxeaVj5G1kCJqjQT_EzTfHE=.png)

In the settings, choose your WAN bridged adapter, and click on advanced...
Here it's VMnet0 and his MAC is 00:0C:29:1A:EE:D9

![](assets/tDqYK4Wm2pVV2iT5eVFERa4xZrvQSYsDqZJsM-fUYrk=.png)

Back in our VM, we can now choose the WAN adapter (em0).
And LAN is em1.

Skip the Optionnal interface 1 name by pressing enter.
Press y to validate the configuration.

![](assets/sh4YZeyJfZanMUCbwbuyKV9w2PEEwQP9-03B5Nvug1A=.png)

Now, select the 2 to Set the ip addresses of our two interfaces.

![](assets/rAPuZ9lnchq9BLJbNZlcYmZ6jxH_FYGFFmbv0E3U6E8=.png)

Select the LAN

![](assets/6j3amaH5EQXK3Dwz49QMFDUQasOhkC-SUM1amGSgvKY=.png)



![](assets/8qbzFpAOJ6JP831olOYY_dIs4eLL1zKKo4dozh_EbeY=.png)

We need our virtual machines to have static ip to communicate with each other and for a better understanding of the network logs later.
let's don't use DHCP for the LAN interface.
Here i choose 10.77.0.1/24 as ou vmnet1 interface is configured on this network in vmware (10.77.0.0/24)

![](assets/INnbiDyDHRATJHuANWXbO1IELsL5r2HVWeGsA6GE08I=.png)

Subnet 24 and don't configure IPV6 here.
You can say no to everything else in our case.

![](assets/K4Bx6CghBMr4Xurn_kH8DOmkduCMSH5bv917oJlHnqI=.png)

Now we can configure the WAN interface in DHCP this time, because we will simply block all the WAN subnet to the LAN devices, so they will have internet access without being able to communicate with ou host pc and network (Very crucial thing).

![](assets/oJd6q3C9ABwjHKK6l4ThxQLzYjUL8D2e6s_HN5buhfo=.png)

As before, don't configure IPV6 and say no to the rest.

![](assets/LRBBCLvTdECDKbKVe4-bOycOczLOgl-TjQyt2bhNIc4=.png)



That's it, we have correctly configured ou interfaces and have ip addresses for both now.

![](assets/UfzhhkFtr188q0wGEh1yujnMPXMwCsYsGTe4_YVhyFY=.png)

