# Windows

## Windows Update

Manage **W**indows **U**pdate **S**ervice (WSUS).

???+ tip "Manage WSUS state"
    | Command                                                   | Description |
    | --------------------------------------------------------- | ----------- |
    | `Set-Service -Name wsusservice -Status Running -PassThru` | Enable WSUS |
    | `Start-Service wsusservice  -PassThru`                    | Start WSUS  |

## Sources

- [Powershell Documentation - Set-Service](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/set-service?view=powershell-7.2)
