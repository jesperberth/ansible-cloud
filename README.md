# Ansible-cloud

Playbooks and guides for enabling a a redundant website in Azure, AWS and Oracle Cloud

All playbooks are for ansible command tools, for Ansible Tower see link

## Oracle Cloud

[OCI Credentials Setup](https://docs.cloud.oracle.com/en-us/iaas/Content/API/SDKDocs/ansiblegetstarted.htm)

[OCI Ansible Module Documentation](https://oracle-cloud-infrastructure-ansible-modules.readthedocs.io/en/latest/index.html)

[OCI Ansible Module index](https://oracle-cloud-infrastructure-ansible-modules.readthedocs.io/en/latest/modules/list_of_cloud_modules.html)

### Todo

Prerequisits

A linux machine, iam using WSL2 Ubuntu
VSCode or other IDE
SSH Client
Webbrowser

Install ansible and prerequisits

```bash
sudo apt-get install python3-venv
python3 -m venv ansible-oci
source ansible-oci/bin/activate
pip install wheel
pip install ansible

ansible --version

pip install oci

git clone https://github.com/oracle/oci-ansible-modules.git

cd oci-ansible-modules

./install.py

```

Create credentials

```bash
mkdir .oci

openssl genrsa -out ~/.oci/oci_api_key.pem 2048

chmod go-rwx ~/.oci/oci_api_key.pem

openssl rsa -pubout -in ~/.oci/oci_api_key.pem -out ~/.oci/oci_api_key_public.pem

openssl rsa -pubout -outform DER -in ~/.oci/oci_api_key.pem | openssl md5 -c
```

[OCI Credentials Setup](https://docs.cloud.oracle.com/en-us/iaas/Content/API/SDKDocs/ansiblegetstarted.htm)

In the web UI create a new user for programatic access, save to ~/.oci/config

```bash
vi ~/.oci/config

[DEFAULT]
user=ocid1.user.oc1..aaaaaaaxxxxxxxxxxxxsxwrtlmxslyi5ob6wup3gjadghctttttttera
fingerprint=06:16:ae:71:98:16:70:56:ef:1f:62:45:fb:b2:56:98
key_file=~/.oci/oci_api_key.pem
tenancy=ocid1.tenancy.oc1..aaaaaaaanaqxxxxxxxxxxxxxxxxnvmeburfq7k43ttttttehta
region=eu-frankfurt-1
```

You can test connection with this command

```bash
ansible localhost -m oci_region_facts
```
