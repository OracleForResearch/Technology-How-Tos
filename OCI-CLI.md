## Setting up OCI Command line interface (CLI) for Researchers

By Rajib Ghosh, Senior Solutions Architect, Oracle for Research

This document outlines the basic and the necessary steps to set up the OCI command line interface for Oracle for Research. Since most researchers need basic automation steps I,e starting and stopping instances, standing up and terminating clusters, the document focusses on to get them started and show the learning path required for advanced options. This requires a researcher be familiar with spinning up a compute instance and logging in to the VM as opc account with SSH credentials. Key steps are illustrated below

### Pre-requisites
* Oracle Linux 7.8 / Oracle Linux 8 platform image
* Successful SSH to the compute instance

1.	Spin up a compute instance with Oracle 7.8 / Oracle 8 Linux image with an Always Free Tier shape
2.	Follow the link to perform a yum install of OCI CLI as shown below based on the image you selected
https://docs.cloud.oracle.com/en-us/iaas/Content/API/SDKDocs/cliinstall.htm 
3.	After successful install, go ahead and generate the API signing key as shown below from the opc account or whichever account you would be working
<pre><code>mkdir ~/.oci
openssl genrsa -out ~/.oci/oci_api_key.pem 2048  # passphrase (recommended) 
chmod go-rwx ~/.oci/oci_api_key.pem               # Change permission on the key
openssl rsa -pubout -in ~/.oci/oci_api_key.pem -out ~/.oci/oci_api_key_public.pem             # Create a public key
cat ~/.oci/oci_api_key_public.pem     # cat the public key and copy it to clipboard 
</code></pre>

4.	Get the key fingerprint 
<pre><code>openssl rsa -pubout -outform DER -in ~/.oci/oci_api_key.pem | openssl md5 -c</code></pre>
5.	Get the Tenancy OCID and User’s OCID (following the link) and upload the public key
https://docs.cloud.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm 
6.	Create the python virtual environment based on the python environment
<pre><code>python3.6 -m venv oracle-cli
source oracle-cli/bin/activate
pip install --upgrade pip</code></pre>
7.	Download OCI CLI from github
<pre><code>wget https://github.com/oracle/oci-cli/releases/download/v2.14.1/oci-cli-2.14.1.zip</code></pre>
8.	Install OCI CLI 
(Refer - https://docs.cloud.oracle.com/en-us/iaas/Content/API/SDKDocs/climanualinst.htm)
<pre><code>pip install oci-cli</code></pre>
9.	Setup OCI CLI Resource files 
<pre><code>oci setup oci-cli-rc --file ~/.oci/oci-cli-rc</code></pre>
10.	Set up the OCI CLI config file in vi ~/.oci/config and populate with the following 
<pre><code>[DEFAULT]
user=ocid1.user.oc1..<unique_ID>
fingerprint=<your_fingerprint>
key_file=~/.oci/oci_api_key.pem
tenancy=ocid1.tenancy.oc1..<unique_ID>
region=us-ashburn-1

[ADMIN_USER]
user=ocid1.user.oc1..<unique_ID>
fingerprint=<your_fingerprint>
key_file=keys/admin_key.pem
pass_phrase=<your_passphrase></code></pre> 
11.	Set up permissions for the OCI CLI config file 
<pre><code>oci setup repair-file-permissions --file /home/opc/.oci/config</code></pre>
12.	Test OCI CLI 
<pre><code>oci os ns get</code></pre>
13.	Refer to CLI environment variables setup 
https://docs.cloud.oracle.com/en-us/iaas/Content/API/SDKDocs/clienvironmentvariables.htm#CLI_Environment_Variables
14.	For OCI CLI command reference 
https://docs.cloud.oracle.com/en-us/iaas/tools/oci-cli/2.14.1/oci_cli_docs/ 

### Using the Research Gateway custom image

You may be able to use an Oracle for Research custom image to standup a gateway VM. The image is pre-installed with OCI CLI on OracleLinux7.8 and you would only need it to configure with your tenancy ocid, compartment ocid and user ocid in ~/.oci/config file 

1.	Import the image to your tenancy as a custom image using the following URL – 
2.	Create the Always Free Tier compute instance with this custom image in the public subnet
3.	SSH to the instance ( ssh -i <pvt key> opc@<public IP> )
4.	Run – oci os ns get 
5.	You should receive a json output of the OCI namespaces in your tenancy
6.	This concludes a successful installation of OCI CLI

### What’s next? 

1.	If you are familiar with Linux bash scripts or if not learn the basics of Linux bash shell script
2.	You may use any Linux tutorial to learn shell scripting
3.	Refer to the OCI CLI command line documentation to try and test out OCI CLI 
4.	Use OCI CLI from the Research-Gatway VM to start / stop your instances / cluster
5.	Use operating system tools or OCI telemetry to remotely monitor cluster usage
6.	Shutdown VM / instance pool based on usage characteristics

NOTE : Oracle for research would have an enhanced version of the image with start / stop scripts and instructions. However, OCI generic direction being with Terraform scripting is encouraged.
