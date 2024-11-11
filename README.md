# ติดตั้ง Oracle Database 21c Enterprise บน Oracle Linux 8

## แก้ไขไฟล์ hosts
```bash
nano /etc/hosts
```

แก้ไขข้อมูลตามด้านล่าง
```bash
[Your IP, 192.168.X.X]  ol8-21.localdomain  ol8-21
```

## ตั้งค่า Hostname
```bash
nano /etc/hostname
```

แก้ไขตั้งค่าตามนี้
```bash
ol8-21.localdomain
```

## Preinstallation

### Automatic installation
```bash
dnf install -y oracle-database-preinstall-21c
dnf update -y
```
หากไม่สามารถติดตั้งได้ลองใช้คำสั่งต่อไปนี้
```bash
curl -o oracle-database-preinstall-21c-1.0-1.el8.x86_64.rpm https://yum.oracle.com/repo/OracleLinux/OL8/appstream/x86_64/getPackage/oracle-database-preinstall-21c-1.0-1.el8.x86_64.rpm
dnf -y localinstall oracle-database-preinstall-21c-1.0-1.el8.x86_64.rpm
```

### Manual installation
```bash
nano /etc/sysctl.conf
```

```bash
/sbin/sysctl -p
```

```bash
nano /etc/security/limits.d/oracle-database-preinstall-21c.conf
```

```bash
oracle   soft   nofile    1024
oracle   hard   nofile    65536
oracle   soft   nproc    16384
oracle   hard   nproc    16384
oracle   soft   stack    10240
oracle   hard   stack    32768
oracle   hard   memlock    134217728
oracle   soft   memlock    134217728
oracle   soft   data    unlimited
oracle   hard   data    unlimited
```

## ติดตั้ง Package
```bash
dnf install -y bc
dnf install -y binutils
dnf install -y compat-openssl10
dnf install -y elfutils-libelf
dnf install -y glibc
dnf install -y glibc-devel
dnf install -y ksh
dnf install -y libaio
dnf install -y libXrender
dnf install -y libX11
dnf install -y libXau
dnf install -y libXi
dnf install -y libXtst
dnf install -y libgcc
dnf install -y libnsl
dnf install -y libstdc++
dnf install -y libxcb
dnf install -y libibverbs
dnf install -y make
dnf install -y policycoreutils
dnf install -y policycoreutils-python-utils
dnf install -y smartmontools
dnf install -y sysstat

# Added by me.
dnf install -y unixODBC
```

## สร้างกลุ่มผู้่ใช้งาน
```bash
groupadd -g 54321 oinstall
groupadd -g 54322 dba
groupadd -g 54323 oper 
groupadd -g 54324 backupdba
groupadd -g 54325 dgdba
groupadd -g 54326 kmdba
groupadd -g 54327 asmdba
groupadd -g 54328 asmoper
groupadd -g 54329 asmadmin
groupadd -g 54330 racdba

useradd -u 54321 -g oinstall -G dba,oper oracle
```


