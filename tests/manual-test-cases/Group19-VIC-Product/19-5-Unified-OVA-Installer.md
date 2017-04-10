Test 19-5 - Unified OVA Installer
=======

#Purpose:
To verify the procedure to install VIC via the unified OVA installer procedure

#References:
[1 - VIC Setup Requirements](https://vmware.github.io/vic-product/assets/files/html/latest/vic_installation/vic_installation_prereqs.html)

#Environment:
* This test requires access to VMWare vCenter system that is meets the requirements from [1]

#Test Steps:
1. Download the latest unified OVA installer for VIC
2. Using the VC OVA installer process, walk through the unified installer steps
    - only required options should be to set the passwords
3. After the install process, power on the VIC VM and wait for it to boot
4. Login to VIC UI via the URL provided from the console output after boot
5. Switch over to the Harbor UI portion of the UI
6. Click on admin->download root cert and download the self-signed certs from Harbor
7. Install the self-signed certs into your local docker client and restart the docker daemon
    - mkdir -p /etc/docker/certs.d/<harbor_ip>
    - cp ca.crt  /etc/docker/certs.d/<harbor_ip>/ca.crt
    - systemctl daemon-reload
    - systemctl restart docker
8. Create a new project in harbor called vic-test
9. Using a local docker client, download busybox image and tag it for the harbor project:
    - docker pull busybox
    - docker tag busybox <harbor-ip>/vic-test/busybox
    - docker push <harbor-ip>/vic-test/busybox
10. Navigate your browser to the included UI and VCH bundle
    - https://<VIC-IP>:9443
11. Download the UI and VCH bundle
12. Install the UI bundle 

#Expected Outcome:


#Possible Problems:
* 