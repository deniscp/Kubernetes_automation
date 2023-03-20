Requirements
============

The playbook "kvm_provision.yaml" requires a KVM/QEMU image, a public/private SSH key pairs and an xml KVM/QEMU VM provisionig j2 template tailored to your system.
The latter can be obtained starting from an already provisioned KVM/QEMU VM by using the libvirt command:

```
virsh dumpxml <linux_domain_name> > vm-template.xml
```

The following instructions show how to obtain the "default/main.yml" requirements but they can be overrided by providing to "kvm_provision.yaml" the path to a different VM Linux server image and the path to a different SSH public key.

#### Download the latest base image from https://alt.fedoraproject.org/cloud/ , e.g. "Fedora-Cloud-Base-37-1.7.x86_64.qcow2":

```
mkdir -p $HOME/Download/kvm_provision && cd $HOME/Download/kvm_provision/
```
```
curl https://download.fedoraproject.org/pub/fedora/linux/releases/37/Cloud/x86_64/images/Fedora-Cloud-Base-37-1.7.x86_64.qcow2 -o Fedora-Cloud-Base-37-1.7.x86_64.qcow2
```

#### Verify the authenticity and integrity of the the downloaded image ( refer to https://alt.fedoraproject.org/en/verify.html ) :
```
curl https://getfedora.org/static/fedora.gpg > fedora.gpg
```
```
curl https://getfedora.org/static/checksums/37/images/Fedora-Cloud-37-1.7-x86_64-CHECKSUM > Fedora-Cloud-37-1.7-x86_64-CHECKSUM
```

```
gpg --no-default-keyring --keyring fedora.gpg --verify Fedora-Cloud-37-1.7-x86_64-CHECKSUM
```
```
cat Fedora-Cloud-37-1.7-x86_64-CHECKSUM | grep .qcow2 | sha256sum -c --ignore-missing
```

 - **make sure "Fedora-Cloud-Base-37-1.7.x86_64.qcow2: OK" appears in the output**

#### Generate the public/private SSH key pair:
```
mkdir -p $HOME/Download/kvm_provision/ssh_keys && $HOME/Download/kvm_provision/ssh_keys
```
```
ssh-keygen -t rsa -b 3072 -f id_rsa -C "kvm_provision"
```
