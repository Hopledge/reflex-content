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

## AD

https://www.it-connect.fr/modules/installation-et-configuration-de-wsus/

### Ajouter utilisateur

- Console `mmc`
- Utilisateurs et ordinateurs AD ~> xxx.xyz ~> Users ~> Logo utilisateur bleu
- Suivre l'assistant

Sinon outil dédié ~> `dsa.msc`

### Créer GPO

- Console `mmc`
- Gestion des stratégies de groupe ~> Forêt ~> Domaines ~> corpxx.local ~> Objets de stratégie de groupe
- Click droit, créer GPO
- Click droit sur la GPO ~> Editer

### Appliquer GPO

Rappel de la hiérarchie d'application des GPO

![](https://s3.hedgedoc.org/demo/uploads/ce30d7ca-fb0d-419e-8825-22c0731fcfc9.png)

- Console `mmc`
- Gestion des stratégies de groupe ~> Forêt ~> Domaines ~> corpxx.local ~> Objets de stratégie de groupe

### Hardening

- Télécharger et lancer ping castle
- Lire le rapport

- Désactiver SMBv1 via la console des fonctionnalités
- Installer LAPS depuis le [site officiel](https://www.microsoft.com/en-us/download/details.aspx?id=46899)
- Désactiver le service Spoiler d'impression dans la console des services
- Désactiver netbios depuis la fonction avancé de l'adapateur ethernet

## Sources

- [Powershell Documentation - Set-Service](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/set-service?view=powershell-7.2)
