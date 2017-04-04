# Study - Linux from Scratch

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

## ���Ѥ���ѥå�����
- acl
  - ������������ꥹ��(Access Control List)
- attr
  - �ե����륷���ƥ४�֥������Ȥγ�ĥ°�������
- autoconf
  - �ƥ�ץ졼�Ȥ򸵤˥����������ɤ�ư��������
- automake
  - �ƥ�ץ졼�ȥե����뤫��Makefile�����
- bash
  - Bourne������
- bc
  - Ǥ�����٤α黻�����������
- binutils
  - ��󥫡�������֥����Υ��֥������ȥե�����򰷤��ץ����
- bison
  - yacc(Yet Another Compiler Compiler)��GNU�С������
- bzip2
  - �ե�����ΰ��̡���ĥ��Ԥ��ץ����
- check
  - ¾�ץ������Ф���ƥ��ȥϡ��ͥ�
- coreutils
  - �ե������ǥ��쥯�ȥ�򻲾�or���뤿��δ��ܥץ����
- dejagnu
  - ¾�ץ����Υƥ��ȥե졼����
- diffutils
  - �ե����롢�ǥ��쥯�ȥ�֤κ��ۤ�ɽ������ץ����
- e2fsprogs
  - ext2,ext3,ext4�γƥե����륷���ƥ�򰷤��桼�ƥ���ƥ��ץ����
- eudev
  - �ǥХ����ޥ͡�����
- expat
  - ���Ū�����Ϥ�XML���ϥ饤�֥��
- expect
  - ¾�ץ��������÷��ץ������̤��Ƥ��Ȥ��Ԥ��ץ����
- file
  - ���ꤵ�줿�ե�����μ����Ƚ�̤���桼�ƥ���ƥ�
- findutils
  - �ե����륷���ƥ��Υե����븡����Ԥ��ץ����
- flex
  - �ƥ������������ѥ������ǧ��

## LFS�Υ��åȥ��å�

#### 0.ɬ�׻����Υ��������
- �ʲ������Ȥ��麣��Ƴ������LFS�ΥС����������ꡣ����PDF�ե��������������
  - http://lfsbookja.osdn.jp/

#### 1. �ۥ��ȥ����ƥ������
- Vagrant+VirtualBox�ι�����CentOS6.7������

#### 2. Linux�ѡ��ƥ�����󡢥ե����륷���ƥ�ι���
- ���󥽥եȥ������γ�ǧ
  - bash lfs_version_check.sh
  - bash lfs_library_check.sh
- ­��ʤ���Τ򥤥󥹥ȡ���
  - yum -y install bison
  - yum -y install byacc
  - yum -y install patch
  - yum -y install xz
  - yum -y install texinfo  #makeinfo��texinfo�ѥå������ˤ���Τ����
- �ѡ��ƥ���������
  - �ʲ�������
    - / (15GB
    - swap (�����2��)
    - /boot(100MB)
  - �ޤȤ�ϰʲ�
    - http://eng-entrance.com/linux-make-filesystem
  - fdisk -l
  - fdisk /dev/xxx #���ܥѡ��ƥ�������ֹ�1�������1��+15G�Ǻ������Ǹ��w(���)
- �ե����륷���ƥ����(�����ext4)
  - mkfs.ext4 /dev/sdd1
- ����ѥ桼����.bashrc��LFS�����ѤΥɥ�����ȥ롼�����ѿ�LFS�����
  - export LFS=/mnt/lfs
- �ޥ���ȥݥ���Ⱥ������ޥ����
  - mkdir -vp $LFS
  - mount /dev/xxx $LFS
  - df -h

#### 3. LFS�����ѥѥå�����&�ѥå��ι���
- �������ǥ��쥯�ȥ����
  - mkdir -vp $LFS/sources
  - chmod -v a+wt $LFS/sources
- ����������оݥѥå������ꥹ�Ȥ����
  - �ʲ������Ȥ����о�LFS�С�������wget-list�����
    - http://lfsbookja.osdn.jp/
  - wget wget-list���������URL
- ����������оݥѥå������ꥹ�Ȥ�����������
  - wget --input-file=wget-list --continue --directory-prefix=$LFS/sources
- �ѥå����������������å��ѤΥ����å�����ե����������
  - �ʲ������Ȥ����о�LFS�С������Υ����å�����ե���������
    - http://lfsbookja.osdn.jp/
  - pushed $LFS/sources
  - md5sum -c md5sums

#### 4. ���Ū�Ķ��ν���
- �ӥ�ɺѥץ�����Ǽ�ѤΥǥ��쥯�ȥ�������ȥåץ�󥯺���
  - mkdir -v $LFS/tools
  - ln -sv $LFS/tools /
- ����ѥ桼�������ɲ�
  - groupadd lfs
  - useradd -s /bin/bash -g lfs -m -k /dev/null lfs
  - passwd lfs
  - chown -Rv lfs $LFS/tools
  - chown -Rv lfs $LFS/sources
  - su - lfs
- ����ѥ桼�����Υ������ȥ��å�������ɲ�
  - cat ~/.bash_profile << "EOF"
exec env -i HOME=$HOME TERM=$TERM PS1='\u:\w\$ ' /bin/bash
EOF
  - cat ~/.bashrc << "EOF"
set +h
umask 022
LFS=/mnt/lfs
LC_ALL=POSIX
LFS_TGT=$(uname -m)-lfs-linux-gnu
PATH=/tools/bin:/bin:/usr/bin
export LFS LC_ALL LFS_TGT PATH
EOF
  - source ~/.bash_profile
  - source ~/.bashrc

#### ���ܥѥå������Υ��󥹥ȡ���
- binutils�Υ��󥹥ȡ���
  - su - lfs
  - cd $LFS/sources
  - tar xf binutils-xxxx.tar.bz2
  - mkdir -v build
  - cd build
  - ../binutils-xxxx/configure  --prefix=tools        \
                                --with-sysroot=$LFS   \
                                --with-lib-path=/tools/lib  \
                                --target=$LFS_TGT   \
                                --disable-nls \
                                --disable-werror

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
