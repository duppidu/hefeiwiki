# VBox Xubuntu Image as OVA-File

\\hftm31\tmp\AlainRohr\Robotino64Bit.ova

## 3D-Enabling
export LIBGL_ALWAYS_INDIRECT = 1

or
export LIBGL_ALWAYS_SOFTWARE = 1

http://www.mesa3d.org/envvars.html


## minimizing Image

in guest (linux): dd if=/dev/zero of=/mnt/tmp/big.file bs=102400 

then on host: VBoxManage modifyhd --compact Windows\ XP.vdi 

http://www.schnatterente.net/software/virtualbox-vdi-image-verkleinern