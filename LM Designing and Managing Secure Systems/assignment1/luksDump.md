```shell
# View LUKS header/key information
cryptsetup luksDump encrypted_filesystem.img

LUKS header information
Version:        2
Epoch:          9
Metadata area:  16384 [bytes]
Keyslots area:  16744448 [bytes]
UUID:           0e4d89d2-1ea7-4f47-a3b3-2ff43e5c83dd
Label:          (no label)
Subsystem:      (no subsystem)
Flags:          (no flags)

Data segments:
  0: crypt
        offset: 16777216 [bytes]
        length: (whole device)
        cipher: aes-xts-plain64
        sector: 512 [bytes]

Keyslots:
  3: luks2
        Key:        512 bits
        Priority:   normal
        Cipher:     aes-xts-plain64
        Cipher key: 512 bits
        PBKDF:      argon2i
        Time cost:  720
        Memory:     10240
        Threads:    4
        Salt:       a8 20 95 a7 18 73 67 a9 26 3e ff 4e 15 80 20 c9
                    31 45 65 8f d9 1e 3d 9b 55 b2 cb 2c de e6 b4 fc
        AF stripes: 4000
        AF hash:    sha256
        Area offset:806912 [bytes]
        Area length:258048 [bytes]
        Digest ID:  0
Tokens:
Digests:
  0: pbkdf2
        Hash:       sha256
        Iterations: 251577
        Salt:       f3 41 af 97 bc 6b 01 94 a5 f0 93 cb 89 81 cf dc
                    09 3f 49 bf 7d 15 0f 34 49 e2 78 aa 35 5a 97 f9
        Digest:     74 86 e3 00 34 e8 c7 c5 43 1c 81 ab 2f 04 06 8d
                    33 c3 8c b9 37 30 66 11 dc b4 f6 da d3 72 0d 88
```

```shell
# View configured LUKS header/key information
cryptsetup luksDump encrypted_filesystem.img

LUKS header information
Version:        2
Epoch:          28
Metadata area:  16384 [bytes]
Keyslots area:  16744448 [bytes]
UUID:           0e4d89d2-1ea7-4f47-a3b3-2ff43e5c83dd
Label:          (no label)
Subsystem:      (no subsystem)
Flags:          (no flags)

Data segments:
  0: crypt
        offset: 16777216 [bytes]
        length: (whole device)
        cipher: aes-xts-plain64
        sector: 512 [bytes]

Keyslots:
  0: luks2 # passphrase
        Key:        512 bits
        Priority:   normal
        Cipher:     aes-xts-plain64
        Cipher key: 512 bits
        PBKDF:      pbkdf2
        Hash:       sha256
        Iterations: 2052006
        Salt:       54 b8 74 5b 5d de ab 48 07 32 1e 29 ea d2 89 dd
                    ef 2d 02 35 76 47 97 d9 12 89 7a 87 31 6d 48 79
        AF stripes: 4000
        AF hash:    sha256
        Area offset:290816 [bytes]
        Area length:258048 [bytes]
        Digest ID:  0
  1: luks2 # new.key
        Key:        512 bits
        Priority:   normal
        Cipher:     aes-xts-plain64
        Cipher key: 512 bits
        PBKDF:      pbkdf2
        Hash:       sha256
        Iterations: 2068196
        Salt:       74 cb 36 09 7d ae 70 4f 48 61 06 da 98 85 db 1c
                    ac ec 89 36 00 54 e6 06 be ff d4 4e dd 22 35 bb
        AF stripes: 4000
        AF hash:    sha256
        Area offset:32768 [bytes]
        Area length:258048 [bytes]
        Digest ID:  0
Tokens:
Digests:
  0: pbkdf2
        Hash:       sha256
        Iterations: 251577
        Salt:       f3 41 af 97 bc 6b 01 94 a5 f0 93 cb 89 81 cf dc
                    09 3f 49 bf 7d 15 0f 34 49 e2 78 aa 35 5a 97 f9
        Digest:     74 86 e3 00 34 e8 c7 c5 43 1c 81 ab 2f 04 06 8d
                    33 c3 8c b9 37 30 66 11 dc b4 f6 da d3 72 0d 88
```

earlycon console=ttyAMA0 mem=5G root=/dev/mapper/rootfs rw cryptdevice=/dev/vda:rootfs cryptkey=/dev/vdb1:vfat:new.key

earlycon console=ttyAMA0 mem=5G root=/dev/mapper/rootfs rw cryptdevice=/dev/vda:rootfs cryptkey=rootfs:/mnt/key/new.key

```
mkinitcpio --config /etc/mkinitcpio.conf --generate /boot/initramfs.img
```

