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

You have to explicitly specify the current version, and the target version for the update.

All version combinations in the yml file were tested and worked for me(TM). These are pre-defined as a dict (`update_sets`).

Example. To update a device from 8.5.1 to 9.1.0 set `use_update_set` to `1`:

```yaml
    use_update_set: 1
    update_sets:
      0:
        current_version: "7.2.0(basic)"
        update_to: "8.5.1"
      1:
        current_version: "8.5.1(tasmota)"
        update_to: "9.1.0"
```

Sample output:

```
(...)

TASK [debug] *********************************************************************************************************************************************************
Saturday 25 February 2023  22:32:46 +0100 (0:00:00.245)       0:00:07.624 *****
ok: [192.168.209.1] => {
    "firmware_version": "9.1.0(tasmota)"
}
ok: [192.168.209.2] => {
    "firmware_version": "12.4.0(tasmota)"
}
ok: [192.168.209.3] => {
    "firmware_version": "9.1.0(tasmota)"
}
ok: [192.168.209.4] => {
    "firmware_version": "9.1.0(tasmota)"
}
ok: [192.168.209.5] => {
    "firmware_version": "9.1.0(tasmota)"
}
ok: [192.168.209.8] => {
    "firmware_version": "12.2.0(tasmota)"
}

(...)

TASK [Start firmware update] *****************************************************************************************************************************************
Saturday 25 February 2023  22:32:46 +0100 (0:00:00.024)       0:00:07.939 *****
skipping: [192.168.209.2]
skipping: [192.168.209.8]
changed: [192.168.209.1 -> localhost]
changed: [192.168.209.3 -> localhost]
changed: [192.168.209.5 -> localhost]
changed: [192.168.209.4 -> localhost]

(...)

TASK [Retrieve JSON] *************************************************************************************************************************************************
Saturday 25 February 2023  22:33:00 +0100 (0:00:10.048)       0:00:21.782 *****
skipping: [192.168.209.2]
skipping: [192.168.209.8]
FAILED - RETRYING: [192.168.209.3 -> localhost]: Retrieve JSON (6 retries left).
FAILED - RETRYING: [192.168.209.4 -> localhost]: Retrieve JSON (6 retries left).
(...)
ok: [192.168.209.4 -> localhost]
ok: [192.168.209.5 -> localhost]
ok: [192.168.209.1 -> localhost]
ok: [192.168.209.3 -> localhost]

(...)

PLAY RECAP ***********************************************************************************************************************************************************
192.168.209.1              : ok=9    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.209.2              : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0
192.168.209.3              : ok=8    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.209.4              : ok=8    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.209.5              : ok=8    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.209.8              : ok=4    changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0
```
