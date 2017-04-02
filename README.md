# Study_Linux from Scratch

## LFS�Ȥ�
- = Linux from Scratch
- Linux�����ƥ��ư��λ��Ȥߤ��ٶ����뤿��ζ��ࡣ
- Linux��1���饫���ͥ�����ޤ�����Ƽ��Ȥǥ���������ѥ��뤹�롣
- ή��Ȥ��Ƥ�
  - LFS�Ķ��������ѤδĶ�����
��- LFS�Ķ��ι���
  - LFS�Ķ����鵯ư��ľ��

## LFS��ɸ��
- �ʲ�ɸ��˽�򤷤Ƥ���
  - POSIX
  - FHS(File Hierarchy System)
  - LSB(Linux Standard Base)
    - LSB Core
    - LSB Desktop
    - LSB Runtime Language
    - LSB Imaging


## LFS�Υ��åȥ��å�
#### 1. �ۥ��ȥ����ƥ������
- Vagrant+VirtualBox�ι�����CentOS6.7������

#### 2. Linux�ѡ��ƥ�����󡢥ե����륷���ƥ�ι���
- ���󥽥եȥ������γ�ǧ
  - lfs_version_check.sh
  - lfs_library_check.sh
- ­��ʤ���Τ򥤥󥹥ȡ���
  - yum -y install bison
  - yum -y install byacc
  - yum -y install patch
  - yum -y install xz
  - yum -y install texinfo  ��makeinfo��texinfo�ѥå������ˤ���Τ����
- �ѡ��ƥ����������
  - / (15GB)
  - swap (�����2��)
  - /boot(100MB)
- VirtualBox���HDD�ǥ����������
- �ѡ��ƥ���������
  - �ʲ�������
    - / (15GB
    - swap (�����2��)
    - /boot(100MB)
  - �ޤȤ�ϰʲ�
    - http://eng-entrance.com/linux-make-filesystem
  - fdisk -l
  - fdisk /dev/xxx �����ܥѡ��ƥ�������ֹ�1�������1��+15G�Ǻ������Ǹ��w(���)
- �ե����륷���ƥ����(�����ext4)
  - mkfs.ext4 /dev/sdd1
- ����ѥ桼����.bashrc�˺��DocumentRoot���ѿ�LFS�����
  - export LFS=/mnt/lfs
- �ޥ���ȥݥ���Ⱥ������ޥ����
  - mkdir -vp $LFS
  - mount /dev/sdd1 $LFS
  - df -h

#### 3. LFS�����ѥѥå�����&�ѥå��ι���
- �������ǥ��쥯�ȥ����
  - mkdir -vp $LFS/sources
  - chmod -v a+wt $LFS/sources
- �ѥå�������������ɤ�ڤˤ��뤿��˥ġ���wget-list�򥤥󥹥ȡ���
  - wget --input-file=wget-list --continue

#### 4. ���Ū�Ķ��ν���
#### ���ܥѥå������Υ��󥹥ȡ���
#### LFS�����ƥ�ι���
#### �١��������ƥ������
#### �����ͥ�&�֡��ȥ�����������
#### ����Υ��ƥå�


## ����
- Linux from Scratch��������
  - http://lfsbookja.osdn.jp/7.10/
- LFS����
  - http://note.kurodigi.com/lfs77-part1/
  - http://shain.blog.conextivo.com/2015/01/lfs_on_virtualbox.html#more
