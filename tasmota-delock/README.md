# Tasmota (Delock)

## get-tasmota-delock-firmware-version.yml

Retrieves firmware version data of all Tasmota devices. I'm using Delock 11827 devices.

Sample host file `/etc/ansible/hosts`:

```
[delocks]
192.168.209.[1:5]
192.168.209.8
```

Sample output:

```
TASK [debug] **************************************************************************************************************************************************
Saturday 25 February 2023  21:01:17 +0100 (0:00:00.232)       0:00:10.014 *****
ok: [192.168.209.1] => {
    "firmware_version": "8.5.1(tasmota)"
}
ok: [192.168.209.2] => {
    "firmware_version": "12.4.0(tasmota)"
}
ok: [192.168.209.3] => {
    "firmware_version": "7.2.0(basic)"
}
ok: [192.168.209.4] => {
    "firmware_version": "7.2.0(basic)"
}
ok: [192.168.209.5] => {
    "firmware_version": "7.2.0(basic)"
}
ok: [192.168.209.8] => {
    "firmware_version": "12.2.0(tasmota)"
}
```


## update-tasmota-delock-firmware.yml

Updates the firmware of a tasmota device.

You have to explicitly specify the current version, and the version for the update.

All version combinations in the yml file were tested and worked for me.

Example. To update a device from 8.5.1 to 9.1.0:

```yaml
      previous_version: "8.5.1(tasmota)"
      update_to: "9.1.0"
```
