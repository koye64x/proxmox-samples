# proxmox-samples

## Создание шаблона cloud-init

<pre>
qm create 1000 --memory 4096 --core 4 --name ubuntu-cloud --net0 virtio,bridge=vmbr0
cd /var/lib/vz/template/iso
qm importdisk 1000 ubuntu-24.04-server-cloudimg-amd64.img local-lvm
qm set 1000 --scsihw virtio-scsi-pci --scsi0 local-lvm:vm-1000-disk-0
qm set 1000 --ide2 local-lvm:cloudinit
qm set 1000 --boot c --bootdisk scsi0
qm set 1000 --serial0 socket --vga serial0
</pre>

1000 - ID ВМ

/var/lib/vz/template/iso - папка образов дистрибутивов

ubuntu-24.04-server-cloudimg-amd64.img - имя файла дистрибутива с cloud-init

local-lvm - имя диска Proxmox для хранения ВМ

Источники:

https://www.youtube.com/watch?v=Kv6-_--y5CM

https://www.youtube.com/watch?v=shiIi38cJe4&ab_channel=TechnoTim

https://technotim.live/posts/cloud-init-cloud-image/
