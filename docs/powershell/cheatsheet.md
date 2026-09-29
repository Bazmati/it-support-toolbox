PowerShell — Les commandes du support

Inventaire / parc

Get-ADComputer -Filter * -Properties OperatingSystem | Select Name,OperatingSystem | Export-Csv postes.csv
Get-ADUser -Filter {Enabled -eq $true} -Properties LastLogonDate | Where LastLogonDate -lt (Get-Date).AddDays(-90)

Utilisateurs (module ActiveDirectory)

Get-ADUser prenom.nom                    # infos utilisateur
Disable-ADAccount prenom.nom             # désactiver (départ de collaborateur)
Search-ADAccount -LockedOut              # comptes verrouillés
Get-ADGroupMember "GG-Support-IT"        # membres d'un groupe

Système / réseau

Get-ComputerInfo                          # fiche complète du poste
Get-Service | Where Status -eq 'Stopped'  # services arrêtés
Get-NetIPAddress                          # configuration IP
Test-NetConnection serveur -Port 3389     # tester RDP sur un serveur
Get-EventLog -LogName System -Newest 20 -EntryType Error   # erreurs récentes

A distance (WinRM activé)

Invoke-Command -ComputerName POSTE-123 { gpupdate /force }
Restart-Computer POSTE-123 -Force

Bon réflexe

Chaque résolution récurrente → en faire un script dans scripts/ versionné dans ce repo :
.\scripts\reset-user.ps1 prenom.nom fait mot de passe + déblocage + notification en une commande.