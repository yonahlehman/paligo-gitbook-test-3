# scan

The `scan` command is used to **run and** **manage scans** in Checkmarx One.

## Usage

```
./cx scan [command] [flags]
```

{% hint style="info" %}
**--scan-timeout** flag can't be used with the **--async** flag.

When a scan is initiated in *asynchronous* mode using **--async** flag, Checkmarx One CLI does not wait for the result and completes the scan.
{% endhint %}

## Scan Commands

`scan` can be used with the following commands:

## In this section

- [scan cancel](scan-cancel.md)
- [scan create](scan-create.md)
- [scan delete](scan-delete.md)
- [scan list](scan-list.md)
- [scan show](scan-show.md)
- [scan tags](scan-tags.md)
- [scan workflow](scan-workflow.md)
- [scan logs](scan-logs.md)
- [sca-realtime](sca-realtime.md)
- [kics-realtime](kics-realtime.md)
