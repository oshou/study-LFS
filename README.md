# Study - Linux from Scratch

## LFSとは
- = Linux from Scratch
- Linuxシステムの動作の仕組みを勉強するための教材。
- Linuxを1からカーネル等も含めて全て手作業でソースコンパイルする。
- 流れとしては
  - LFS環境構準備用の環境構築
　- LFS環境の構築
  - LFS環境から起動し直す

## LFSの標準
- 以下標準に準拠している
  - POSIX
  - FHS(File Hierarchy System)
  - LSB(Linux Standard Base)
    - LSB Core
    - LSB Desktop
    - LSB Runtime Language
    - LSB Imaging

## 使用するパッケージ
- acl
  - アクセス制御リスト(Access Control List)
- attr
  - ファイルシステムオブジェクトの拡張属性を管理
- autoconf
  - テンプレートを元にソースコードを自動作成する
- automake
  - テンプレートファイルからMakefileを作成
- bash
  - Bourneシェル
- bc
  - 任意精度の演算処理言語を提供
- binutils
  - リンカ、アセンブラ等のオブジェクトファイルを扱うプログラム
- bison
  - yacc(Yet Another Compiler Compiler)のGNUバージョン
- bzip2
  - ファイルの圧縮・拡張を行うプログラム
- check
  - 他プログラムに対するテストハーネス
- coreutils
  - ファイルやディレクトリを参照or操作するための基本プログラム
- dejagnu
  - 他プログラムのテストフレームワーク
- diffutils
  - ファイル、ディレクトリ間の差異を表示するプログラム
- e2fsprogs
  - ext2,ext3,ext4の各ファイルシステムを扱うユーティリティプログラム
- eudev
  - デバイスマネージャ
- expat
  - 比較的小規模のXML解析ライブラリ
- expect
  - 他プログラムと対話型プログラムを通じてやりとりを行うプログラム
- file
  - 指定されたファイルの種類を判別するユーティリティ
- findutils
  - ファイルシステム上のファイル検索を行うプログラム
- flex
  - テキスト内の特定パターンの認識

## LFSのセットアップ

#### 0.必要資料のダウンロード
- 以下サイトから今回導入するLFSのバージョンを選定。手順書PDFファイルをダウンロード
  - http://lfsbookja.osdn.jp/

#### 1. ホストシステムの選定
- Vagrant+VirtualBoxの構成でCentOS6.7を選定

#### 2. Linuxパーティション、ファイルシステムの構築
- 前提ソフトウェアの確認
  - bash lfs_version_check.sh
  - bash lfs_library_check.sh
- 足りないものをインストール
  - yum -y install bison
  - yum -y install byacc
  - yum -y install patch
  - yum -y install xz
  - yum -y install texinfo  #makeinfoはtexinfoパッケージにあるので注意
- パーティション作成
  - 以下を想定
    - / (15GB
    - swap (メモリの2倍)
    - /boot(100MB)
  - まとめは以下
    - http://eng-entrance.com/linux-make-filesystem
  - fdisk -l
  - fdisk /dev/xxx #基本パーティション、番号1、シリング1〜+15Gで作成、最後はw(書込)
- ファイルシステム作成(今回はext4)
  - mkfs.ext4 /dev/sdd1
- 作業用ユーザの.bashrcにLFS構築用のドキュメントルート用変数LFSを定義
  - export LFS=/mnt/lfs
- マウントポイント作成、マウント
  - mkdir -vp $LFS
  - mount /dev/xxx $LFS
  - df -h

#### 3. LFS構築用パッケージ&パッチの構築
- ソースディレクトリ作成
  - mkdir -vp $LFS/sources
  - chmod -v a+wt $LFS/sources
- ダウンロード対象パッケージリストを取得
  - 以下サイトから対象LFSバージョンのwget-listを取得
    - http://lfsbookja.osdn.jp/
  - wget wget-listダウンロードURL
- ダウンロード対象パッケージリストからダウンロード
  - wget --input-file=wget-list --continue --directory-prefix=$LFS/sources
- パッケージ正当性チェック用のチェックサムファイルを配置
  - 以下サイトから対象LFSバージョンのチェックサムファイルを取得
    - http://lfsbookja.osdn.jp/
  - pushed $LFS/sources
  - md5sum -c md5sums

#### 4. 一時的環境の準備
- ビルド済プログラム格納用のディレクトリ作成、トップリンク作成
  - mkdir -v $LFS/tools
  - ln -sv $LFS/tools /
- 作業用ユーザーの追加
  - groupadd lfs
  - useradd -s /bin/bash -g lfs -m -k /dev/null lfs
  - passwd lfs
  - chown -Rv lfs $LFS/tools
  - chown -Rv lfs $LFS/sources
  - su - lfs
- 作業用ユーザーのスタートアップ設定を追加
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

#### 基本パッケージのインストール
- binutilsのインストール
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

#### LFSシステムの構築
#### ベースシステムの設定
#### カーネル&ブートローダーの設定
#### 今後のステップ


## 参考
- Linux from Scratch資料一覧
  - http://lfsbookja.osdn.jp/7.10/
- LFS構築
  - http://note.kurodigi.com/lfs77-part1/
  - http://shain.blog.conextivo.com/2015/01/lfs_on_virtualbox.html#more
