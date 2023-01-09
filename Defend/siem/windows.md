# Windows

## Sysmon

Download Sysmon from [Microsoft Website](https://learn.microsoft.com/fr-fr/sysinternals/downloads/sysmon).

And now, you can find configurations in the [sysmon-modular github repository](https://github.com/olafhartong/sysmon-modular).

Install with config

```powershell
.\Sysmon64.exe -i config.xml
```

Update config

```powershell
.\Sysmon64.exe -c config.xml
```
