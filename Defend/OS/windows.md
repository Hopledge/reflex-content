# Windows

## User management

???+ tip "Manage WSUS state"
    | Command                                                   | Description |
    |-----------------------------------------------------------|-------------|
    | `Set-Service -Name wsusservice -Status Running -PassThru` | Enable WSUS |
    | `Start-Service wsusservice  -PassThru`                    | Start WSUS  |

## Windows Update

Manage **W**indows **S**erver **U**pdate **S**ervice (WSUS).

???+ tip "Manage WSUS state"
    | Command                                                   | Description |
    |-----------------------------------------------------------|-------------|
    | `Set-Service -Name wsusservice -Status Running -PassThru` | Enable WSUS |
    | `Start-Service wsusservice  -PassThru`                    | Start WSUS  |

???+ faq "Time management"
    | Command                                    | Description                                         |
    |--------------------------------------------|-----------------------------------------------------|
    | `Get-TimeZone`                             | Get time configuration                              |
    | `Get-TimeZone -ListAvailable`              | List all timezone (Romance Standard Time" for :fr:) |
    | `Set-TimeZone -Id "Romance Standard Time"` | Set timezone for Europe                             |

## Sources

- [Powershell Documentation - Set-Service](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/set-service?view=powershell-7.2)
