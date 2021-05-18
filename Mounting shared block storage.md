## Mounting block volumes across multiple compute instances

By Mike Riley, Solutions Architect, Oracle for Research

Content Updated May 2021

A block volume can be shared READ/WRITE by multiple instances (**maximum of 8 within OCI**). 

However for READ/WRITE a cluster file system is required.  The information within this document  shows the OCI console screens for READ/WRITE attachment for sharing a block volume. There are also links to existing content relating to Oracle Linux and some high level commands for achieving this on Ubuntu.

The following example uses node1 & node2 and shares a block volume between them using OCFS2.
It is assumed that the 2 compute instances are already created and that they and the block volume are all within the same Availability Domain (AD). 
To create the Block Volume:-

![image](https://user-images.githubusercontent.com/74327135/118629234-4e98a900-b7c5-11eb-8139-eac760dfaaad.png)

Once created the Block Volume now needs to be attached to both instances.
Note the READ/WRTE select & the acknowledgment that it is understood that a clustered file system is required.

![image](https://user-images.githubusercontent.com/74327135/118629411-7556df80-b7c5-11eb-85cc-c6a67c00f238.png)


This shows volume attached to both instances 
![image](https://user-images.githubusercontent.com/74327135/118629518-915a8100-b7c5-11eb-94d2-aaab42d77df5.png)

For both of these to access the volume READ/WRITE then a cluster volume HAS to be created on the volume.

See the OCI Blog at :- 

https://blogs.oracle.com/cloud-infrastructure/using-the-multi-attach-block-volume-feature-to-create-a-shared-file-system-on-oracle-cloud-infrastructure

Also there is a YouTube Video at :- 

https://www.youtube.com/watch?v=r8hjFOj9Dew


**Brief instructions to implement OCFS2 on Ubuntu 20 are described here below**

The following assumes that you have attached the shared block volume to the instances - see the previous screenshots for attaching READ/WRITE to multiple instances.

1.  Allow Ingress Rules within VCN - for example within the subnet ensure ports 7777 & 3260 allow traffic.

![image](https://user-images.githubusercontent.com/74327135/118629846-e39ba200-b7c5-11eb-9884-80398fc695ec.png)


![image](https://user-images.githubusercontent.com/74327135/118629963-fe6e1680-b7c5-11eb-8ff0-ec5b74407c25.png)

2.  Run the isci commands on all nodes. The commands can be seen from the attached block volume instances.

![image](https://user-images.githubusercontent.com/74327135/118630100-2493b680-b7c6-11eb-9be1-006a313bc52a.png)

Copy these commands & run them on BOTH instances.

![image](https://user-images.githubusercontent.com/74327135/118630197-3aa17700-b7c6-11eb-893c-9cf5e0392368.png)

3.  Change the firewall on BOTH node.

    sudo iptables -I INPUT -m state --state NEW -p tcp --destination-port 7777 -j ACCEPT
    sudo iptables -I INPUT -m state --state NEW -p tcp --destination-port 3260 -j ACCEPT

    sudo su - 

    iptables-save > /etc/iptables/rules.v4

![image](https://user-images.githubusercontent.com/74327135/118630531-818f6c80-b7c6-11eb-864e-32f64ea8b77c.png)

4.  On all nodes run.

    sudo apt-get install ocfs2-tools

![image](https://user-images.githubusercontent.com/74327135/118630617-9835c380-b7c6-11eb-8150-115e39dde5f2.png)

5.  Edit /etc/hosts on ALL nodes
 Place short node names & FQDN (retrieve from the oci console main page for each instance). The FQDN can be found from the console for each instance.

    sudo vi /etc/hosts

![image](https://user-images.githubusercontent.com/74327135/118630697-b00d4780-b7c6-11eb-8b02-97a9947f6857.png)

6.  edit the /etc/ocfs2/cluster.conf file on ALL nodes.

change this file on both nodes - ensuring IP address, node short names match your configuration

![image](https://user-images.githubusercontent.com/74327135/118630783-c3201780-b7c6-11eb-9c4c-0e8ab062c7a5.png)

7.  edit the o2cb file on BOTH nodes.

    change 
    O2CB_ENABLE to true
    O2CB_BOOTCLUSTER=ocfs2
  
![image](https://user-images.githubusercontent.com/74327135/118630868-d92dd800-b7c6-11eb-93ec-58ee2466e2d6.png)

8.  Restart the OCFS services on ALL nodes.

    sudo service o2cb restart
    sudo service ocfs2 restart

![image](https://user-images.githubusercontent.com/74327135/118630930-ecd93e80-b7c6-11eb-80b7-f9a041f76bd5.png)

9.  Create  a directory on ALL nodes.

    sudo mkdir /data-share

![image](https://user-images.githubusercontent.com/74327135/118631025-04182c00-b7c7-11eb-9bee-d9c198d9a53e.png)

10.  On one of the nodes make an OCFS2 file system on the block volume

make a OCFS2 file system - ONLY required on ONE of the nodes.
Note for this worked example the device name allocated when block volume was shared was /dev/sdb. 
This can also be seen at the OS level once the iscsi commands have been run by calling lsblk.

    sudo mkfs.ocfs2 -L data-share /dev/sdb -N 8

![image](https://user-images.githubusercontent.com/74327135/118631093-15613880-b7c7-11eb-9a1d-ae9e0366db0a.png)

11.  On ALL nodes edit fstab for the shared volume

add an entry like the one shown below e.g.

     sudo vi /etc/fstab
     /dev/sdb /data-share ocfs2     _netdev,defaults   0 0

![image](https://user-images.githubusercontent.com/74327135/118631208-2ad66280-b7c7-11eb-8342-41ea00380ee6.png)


12.  Now mount the OCFS2 filesystem on ALL nodes

    sudo mount -a

![image](https://user-images.githubusercontent.com/74327135/118631318-46416d80-b7c7-11eb-80aa-5cd0463e3b19.png)




#### Other References

1.  [Setting fstab options for block volumes using consistent device paths](https://docs.cloud.oracle.com/en-us/iaas/Content/Block/References/fstaboptionsconsistentdevicepaths.htm)
2. [Creating OCI file systems](https://unix.stackexchange.com/questions/395777/how-to-clear-ext4-filesystem-of-partition-in-arch)
3. [Attaching a block volume - end-to-end](https://oracledbwr.com/oracle-gen2-cloud-attaching-a-block-volume-to-an-instance/)
