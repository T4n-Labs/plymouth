# plymouth
Plymouth Setup For T4n OS

## 1. Install Plymouth

Pastikan sudah ada:

```bash
sudo xbps-install -S plymouth
```

## 2. Pilih / Install Theme

Cek theme yang ada:

```bash
plymouth-set-default-theme -l
```

Set theme:

```bash
sudo plymouth-set-default-theme -R spinner
```

> `-R` otomatis rebuild initramfs (kalau dracut tersedia)

Kalau mau manual theme custom:

```bash
/usr/share/plymouth/themes/
```

## 3. Konfigurasi Dracut (PENTING)

Buat config:

```bash
sudo nano /etc/dracut.conf.d/plymouth.conf
```

Isi:

```conf
add_dracutmodules+=" plymouth "
```

Kalau mau lebih clean:

```conf
omit_dracutmodules+=" splash "
add_dracutmodules+=" plymouth "
```

## 4. Enable Kernel Parameters

Edit bootloader (biasanya GRUB):

```bash
sudo nano /etc/default/grub
```

Tambahkan ke:

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash rd.udev.log_level=3 vt.global_cursor_default=0 plymouth.use-simpledrm"
```

## 5. Rebuild GRUB + Initramfs

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
sudo dracut -f
```

## 6. Enable Service (Void Linux)

Kalau pakai Void:

```bash
sudo ln -s /etc/sv/plymouthd /var/service/
```

## 7. Reboot

```bash
reboot
```
