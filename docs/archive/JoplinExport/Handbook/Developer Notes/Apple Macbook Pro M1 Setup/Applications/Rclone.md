---
title: Rclone
updated: 2021-03-14 13:36:32Z
created: 2021-03-14 13:36:32Z
source: https://rclone.org/
---

[<img width="154" height="36" src="../../../../_resources/logo_on_dark__horizontal_color_e5261b4d2843464bad3.svg"/>](https://rclone.org/)

- [Downloads](https://rclone.org/downloads/)
- <a id="navbarDropdown"></a>[Docs](#)
- <a id="navbarDropdown"></a>[Commands](#)
- <a id="navbarDropdown"></a>[Storage Systems](#)
- [Contact](https://rclone.org/contact/)
- [Donate](https://rclone.org/donate/)

# Rclone syncs your files to cloud storage

<img width="450" height="104" src="../../../../_resources/logo_on_light__horizontal_color_8e134f066d734f3b8c.svg"/>

- [About rclone](#about)
- [What can rclone do for you?](#what)
- [What features does rclone have?](#features)
- [What providers does rclone support?](#providers)
- [Download](https://rclone.org/downloads/)
- [Install](https://rclone.org/install/)

## [](#about)About rclone

Rclone is a command line program to manage files on cloud storage. It is a feature rich alternative to cloud vendors' web storage interfaces. [Over 40 cloud storage products](#providers) support rclone including S3 object stores, business & consumer file storage services, as well as standard transfer protocols.

Rclone has powerful cloud equivalents to the unix commands rsync, cp, mv, mount, ls, ncdu, tree, rm, and cat. Rclone's familiar syntax includes shell pipeline support, and `--dry-run` protection. It is used at the command line, in scripts or via its [API](https://rclone.org/rc).

Users call rclone *"The Swiss army knife of cloud storage"*, and *"Technology indistinguishable from magic"*.

Rclone really looks after your data. It preserves timestamps and verifies checksums at all times. Transfers over limited bandwidth; intermittent connections, or subject to quota can be restarted, from the last good file transferred. You can [check](https://rclone.org/commands/rclone_check/) the integrity of your files. Where possible, rclone employs server-side transfers to minimise local bandwidth use and transfers from one provider to another without using local disk.

Virtual backends wrap local and cloud file systems to apply [encryption](https://rclone.org/crypt/), [caching](https://rclone.org/cache/), [compression](https://rclone.org/compress/) [chunking](https://rclone.org/chunker/) and [joining](https://rclone.org/union/).

Rclone [mounts](https://rclone.org/commands/rclone_mount/) any local, cloud or virtual filesystem as a disk on Windows, macOS, linux and FreeBSD, and also serves these over [SFTP](https://rclone.org/commands/rclone_serve_sftp/), [HTTP](https://rclone.org/commands/rclone_serve_http/), [WebDAV](https://rclone.org/commands/rclone_serve_webdav/), [FTP](https://rclone.org/commands/rclone_serve_ftp/) and [DLNA](https://rclone.org/commands/rclone_serve_dlna/).

Rclone is mature, open source software originally inspired by rsync and written in [Go](https://golang.org). The friendly support community are familiar with varied use cases. Official Ubuntu, Debian, Fedora, Brew and Chocolatey repos. include rclone. For the latest version [downloading from rclone.org](https://rclone.org/downloads/) is recommended.

Rclone is widely used on Linux, Windows and Mac. Third party developers create innovative backup, restore, GUI and business process solutions using the rclone command line or API.

Rclone does the heavy lifting of communicating with cloud storage.

## [](#what)What can rclone do for you?

Rclone helps you:

- Backup (and encrypt) files to cloud storage
- Restore (and decrypt) files from cloud storage
- Mirror cloud data to other cloud services or locally
- Migrate data to cloud, or between cloud storage vendors
- Mount multiple, encrypted, cached or diverse cloud storage as a disk
- Analyse and account for data held on cloud storage using [lsf](https://rclone.org/commands/rclone_lsf/), [ljson](https://rclone.org/commands/rclone_lsjson/), [size](https://rclone.org/commands/rclone_size/), [ncdu](https://rclone.org/commands/rclone_ncdu/)
- [Union](https://rclone.org/union/) file systems together to present multiple local and/or cloud file systems as one

## [](#features)Features

- Transfers
    - MD5, SHA1 hashes are checked at all times for file integrity
    - Timestamps are preserved on files
    - Operations can be restarted at any time
    - Can be to and from network, e.g. two different cloud providers
    - Can use multi-threaded downloads to local disk
- [Copy](https://rclone.org/commands/rclone_copy/) new or changed files to cloud storage
- [Sync](https://rclone.org/commands/rclone_sync/) (one way) to make a directory identical
- [Move](https://rclone.org/commands/rclone_move/) files to cloud storage deleting the local after verification
- [Check](https://rclone.org/commands/rclone_check/) hashes and for missing/extra files
- [Mount](https://rclone.org/commands/rclone_mount/) your cloud storage as a network disk
- [Serve](https://rclone.org/commands/rclone_serve/) local or remote files over [HTTP](https://rclone.org/commands/rclone_serve_http/)/[WebDav](https://rclone.org/commands/rclone_serve_webdav/)/[FTP](https://rclone.org/commands/rclone_serve_ftp/)/[SFTP](https://rclone.org/commands/rclone_serve_sftp/)/[dlna](https://rclone.org/commands/rclone_serve_dlna/)
- Experimental [Web based GUI](https://rclone.org/gui/)

## [](#providers)Supported providers

(There are many others, built on standard protocols such as WebDAV or S3, that work out of the box.)

- 1Fichier [Home](https://1fichier.com/) [Config](https://rclone.org/fichier/)
- Alibaba Cloud (Aliyun) Object Storage System (OSS) [Home](https://www.alibabacloud.com/product/oss/) [Config](https://rclone.org/s3/#alibaba-oss)
- Amazon Drive ([See note](https://rclone.org/amazonclouddrive/#status)) [Home](https://www.amazon.com/clouddrive) [Config](https://rclone.org/amazonclouddrive/)
- Amazon S3 [Home](https://aws.amazon.com/s3/) [Config](https://rclone.org/s3/)
- Backblaze B2 [Home](https://www.backblaze.com/b2/cloud-storage.html) [Config](https://rclone.org/b2/)
- Box [Home](https://www.box.com/) [Config](https://rclone.org/box/)
- Ceph [Home](http://ceph.com/) [Config](https://rclone.org/s3/#ceph)
- Citrix ShareFile [Home](http://sharefile.com/) [Config](https://rclone.org/sharefile/)
- C14 [Home](https://www.online.net/en/storage/c14-cold-storage) [Config](https://rclone.org/sftp/#c14)
- DigitalOcean Spaces [Home](https://www.digitalocean.com/products/object-storage/) [Config](https://rclone.org/s3/#digitalocean-spaces)
- Dreamhost [Home](https://www.dreamhost.com/cloud/storage/) [Config](https://rclone.org/s3/#dreamhost)
- Dropbox [Home](https://www.dropbox.com/) [Config](https://rclone.org/dropbox/)
- Enterprise File Fabric [Home](https://storagemadeeasy.com/about/) [Config](https://rclone.org/filefabric/)
- FTP [Home](https://en.wikipedia.org/wiki/File_Transfer_Protocol) [Config](https://rclone.org/ftp/)
- Google Cloud Storage [Home](https://cloud.google.com/storage/) [Config](https://rclone.org/googlecloudstorage/)
- Google Drive [Home](https://www.google.com/drive/) [Config](https://rclone.org/drive/)
- Google Photos [Home](https://www.google.com/photos/about/) [Config](https://rclone.org/googlephotos/)
- HDFS [Home](https://hadoop.apache.org/) [Config](https://rclone.org/hdfs/)
- HTTP [Home](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) [Config](https://rclone.org/http/)
- Hubic [Home](https://hubic.com/) [Config](https://rclone.org/hubic/)
- Jottacloud [Home](https://www.jottacloud.com/en/) [Config](https://rclone.org/jottacloud/)
- IBM COS S3 [Home](http://www.ibm.com/cloud/object-storage) [Config](https://rclone.org/s3/#ibm-cos-s3)
- Koofr [Home](https://koofr.eu/) [Config](https://rclone.org/koofr/)
- Mail.ru Cloud [Home](https://cloud.mail.ru/) [Config](https://rclone.org/mailru/)
- Memset Memstore [Home](https://www.memset.com/cloud/storage/) [Config](https://rclone.org/swift/)
- Mega [Home](https://mega.nz/) [Config](https://rclone.org/mega/)
- Memory [Home](https://rclone.org/memory/) [Config](https://rclone.org/memory/)
- Microsoft Azure Blob Storage [Home](https://azure.microsoft.com/en-us/services/storage/blobs/) [Config](https://rclone.org/azureblob/)
- Microsoft OneDrive [Home](https://onedrive.live.com/) [Config](https://rclone.org/onedrive/)
- Minio [Home](https://www.minio.io/) [Config](https://rclone.org/s3/#minio)
- Nextcloud [Home](https://nextcloud.com/) [Config](https://rclone.org/webdav/#nextcloud)
- OVH [Home](https://www.ovh.co.uk/public-cloud/storage/object-storage/) [Config](https://rclone.org/swift/)
- OpenDrive [Home](https://www.opendrive.com/) [Config](https://rclone.org/opendrive/)
- OpenStack Swift [Home](https://docs.openstack.org/swift/latest/) [Config](https://rclone.org/swift/)
- Oracle Cloud Storage [Home](https://cloud.oracle.com/storage-opc) [Config](https://rclone.org/swift/)
- ownCloud [Home](https://owncloud.org/) [Config](https://rclone.org/webdav/#owncloud)
- pCloud [Home](https://www.pcloud.com/) [Config](https://rclone.org/pcloud/)
- premiumize.me [Home](https://premiumize.me/) [Config](https://rclone.org/premiumizeme/)
- put.io [Home](https://put.io/) [Config](https://rclone.org/putio/)
- QingStor [Home](https://www.qingcloud.com/products/storage) [Config](https://rclone.org/qingstor/)
- Rackspace Cloud Files [Home](https://www.rackspace.com/cloud/files) [Config](https://rclone.org/swift/)
- rsync.net [Home](https://rsync.net/products/rclone.html) [Config](https://rclone.org/sftp/#rsync-net)
- Scaleway [Home](https://www.scaleway.com/object-storage/) [Config](https://rclone.org/s3/#scaleway)
- Seafile [Home](https://www.seafile.com/) [Config](https://rclone.org/seafile/)
- SFTP [Home](https://en.wikipedia.org/wiki/SSH_File_Transfer_Protocol) [Config](https://rclone.org/sftp/)
- StackPath [Home](https://www.stackpath.com/products/object-storage/) [Config](https://rclone.org/s3/#stackpath)
- SugarSync [Home](https://sugarsync.com/) [Config](https://rclone.org/sugarsync/)
- Tardigrade [Home](https://tardigrade.io/) [Config](https://rclone.org/tardigrade/)
- Tencent Cloud Object Storage (COS) [Home](https://intl.cloud.tencent.com/product/cos) [Config](https://rclone.org/s3/#tencent-cos)
- Wasabi [Home](https://wasabi.com/) [Config](https://rclone.org/s3/#wasabi)
- WebDAV [Home](https://en.wikipedia.org/wiki/WebDAV) [Config](https://rclone.org/webdav/)
- Yandex Disk [Home](https://disk.yandex.com/) [Config](https://rclone.org/yandex/)
- Zoho WorkDrive [Home](https://www.zoho.com/workdrive/) [Config](https://rclone.org/zoho/)
- The local filesystem [Home](https://rclone.org/local/) [Config](https://rclone.org/local/)

Links

- [Home page](https://rclone.org/)
- [GitHub project page for source and bug tracker](https://github.com/rclone/rclone)
- [Rclone Forum](https://forum.rclone.org)
- [Downloads](https://rclone.org/downloads/)

Share and Enjoy

[Twitter](https://twitter.com/intent/tweet/?text=rclone%20-%20rsync%20for%20cloud%20storage%20from%20%40njcw&url=https%3A%2F%2Frclone.org)
[Facebook](https://facebook.com/sharer/sharer.php?u=https%3A%2F%2Frclone.org)
[Reddit](https://reddit.com/submit/?url=https%3A%2F%2Frclone.org&resubmit=true&title=rclone%20-%20rsync%20for%20cloud%20storage)

Links

[Rclone forum](https://forum.rclone.org)
[GitHub project](https://github.com/rclone/rclone)
[Rclone slack](https://slack-invite.rclone.org/)
[Rclone Wiki](https://github.com/rclone/rclone/wiki)
[Donate](https://rclone.org/donate/)
[@njcw](https://twitter.com/njcw)

© [Nick Craig-Wood](https://www.craig-wood.com/nick/) 2014-2021
Source file [_index.md](https://github.com/rclone/rclone/blob/master/docs/content/_index.md) last updated [2020-09-28](https://github.com/rclone/rclone/commit/71edc75ca651add7613e64ed41b1af3e082f3e7c)
Website hosted on a [MEMSET CLOUD VPS](https://www.memset.com/dedicated-servers/vps/), uploaded with [rclone](https://rclone.org) and built with [Hugo](https://github.com/spf13/hugo). Logo by [@andy23](https://twitter.com/andy23).