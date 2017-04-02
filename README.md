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
- Acl
  - アクセス制御リスト(Access Control List)
- Attr
  - ファイルシステムオブジェクトの拡張属性を管理
- Autoconf
  - テンプレートを元にソースコードを自動作成する
- Automake
  - テンプレートファイルからMakefileを作成
- Bash
  - Bourneシェル
- Bc
  - 任意精度の演算処理言語を提供
- Binutils
  - リンカ、アセンブラ等のオブジェクトファイルを扱うプログラムを提供

## LFSのセットアップ
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
- 作業用ユーザの.bashrcにLFS構築用のocumentRoot用変数LFSを定義
  - export LFS=/mnt/lfs
- マウントポイント作成、マウント
  - mkdir -vp $LFS
  - mount /dev/xxx $LFS
  - df -h

#### 3. LFS構築用パッケージ&パッチの構築
- ソースディレクトリ作成
  - mkdir -vp $LFS/sources
  - chmod -v a+wt $LFS/sources
- パッケージダウンロードを楽にするためにツールwget-listをインストール
  - wget
  - wget --input-file=wget-list --continue --directory-prefix=$LFS/sources

#### 4. 一時的環境の準備
#### 基本パッケージのインストール
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
