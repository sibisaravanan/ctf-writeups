# Photon Lockdown

This is a writeup for the Photon Lockdown box from Hack the Box.

Type: Challenge
Difficulty: Very Easy
HTB Link: [Photon Lockdown](https://app.hackthebox.com/challenges/Photon%2520Lockdown)

## Solution

There were three files given.

```bash
ls -l
fwu_ver
hw_ver
rootfs
```

The `rootfs` file looks like a SquashFS file system.

```bash
file rootfs
rootfs: Squashfs filesystem, little endian, version 4.0, zlib compressed, 10936182 bytes, 910 inodes, blocksize: 131072 bytes, created: Sun Oct  1 07:02:43 2023
```

We will need the `squashfs-tools` package to extract the file system.

```bash
apt-get install squashfs-tools
```

Now we can extract the file system.

```bash
unsquashfs -d squashfs-root rootfs
```

This will extract the files into the directory `squashfs-root`.

```bash
cd rootfs
```

The typical hackthebox flag format was given as `HTB{}`

Hence we can go a `ripgrep` for the flag.

```bash
rg "HTB"
squashfs-root/etc/config_default.xml
244:<Value Name="SUSER_PASSWORD" Value="HTB{N0w_Y0u_C4n_L0g1n}"/>
```

The flag was found in the file `/etc/config_default.xml`

Done!
