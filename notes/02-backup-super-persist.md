# Backup `super.img` and `persist.img`

## Note
- `super.img` may be around 14–15 GB.
- `persist.img` may be around 30–40 MB.
- `persist.img` contains device-specific data such as fingerprint-related data.
- Keep `persist.img` safe; losing it may result in fingerprint or VoLTE problems.
- Keep backups of newer `super.img` files after major stock updates.

## Steps
1. With root access:
```shell
adb shell
su
dd if=/dev/block/by-name/super of=/sdcard/super.img
dd if=/dev/block/by-name/persist of=/sdcard/persist.img
```
2 files will be saved to internal storage. Keep them safe