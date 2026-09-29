Active Directory — Cheat Sheet Support N1/N2




Concepts clés





AD DS : annuaire central (utilisateurs, ordinateurs, groupes) sur Windows Server.



Domaine : ex. basile.local. Les postes y sont « intégrés » (join domain).



GPO : règles appliquées aux utilisateurs/ordinateurs (mots de passe, mappages, sécurité).



DC : contrôleur de domaine — ne jamais le redémarrer sans prévenir (toujours les autres équipes).

Réinitialiser un mot de passe (tâche n°1 du support)





dsa.msc (Utilisateurs et ordinateurs AD) → retrouver l'utilisateur (Rechercher).



Clic droit → Réinitialiser le mot de passe.



Cocher « L'utilisateur doit changer le mot de passe à la prochaine ouverture ».



Vérifier si le compte est verrouillé (déverrouiller si besoin).



En ligne de commande : Set-ADAccountPassword user1 -Reset -NewPassword (Read-Host -AsSecureString) puis Unlock-ADAccount user1.

Débloquer un compte

Unlock-ADAccount -Identity prenom.nom — cause fréquente : mots de passe tapés après expiration, anciennes sessions Outlook mobiles.

Intégrer un poste au domaine





Paramètres → Système → Renommer ce PC (nom conforme à la convention).



Paramètres → Comptes → Accès professionnel → Se connecter avec un compte de domaine local.



Ou : sysdm.cpl → Nom de l'ordinateur → Modifier → gys.local.



Redémarrer, vérifier dans AD que l'objet ordinateur apparaît.

Créer un utilisateur





dsa.msc → bonne OU (Organizational Unit) → Nouveau → Utilisateur.



Respecter la convention prenom.nom, définir l'UPN (prenom.nom@basile.local).



Mot de passe temporaire + changement forcé.



Ajouter aux groupes (accès partagés, imprimantes) selon le service.



PowerShell : New-ADUser -Name "Prenom Nom" -GivenName "Prenom" -Surname "Nom" -SamAccountName "prenom.nom" -UserPrincipalName "prenom.nom@gys.local" -AccountPassword (Read-Host -AsSecureString) -Enabled $true -ChangePasswordAtLogon $true

Dépannages fréquents







Symptôme



Vérifications





« Le domaine n'est pas disponible »



câble/Wi-Fi, DNS pointe vers le DC (ipconfig /all), ping du DC





Session verrouillée en boucle



compte verrouillé, heure système du poste (Kerakerberos ±5 min)





Lecteurs réseau absents



GPO de mappage, gpupdate /force, redémarrage





Poste sorti du domaine sans raison



conflit de nom, date/heure fausse, ré-intégration nécessaire (compte local admin requis !)





Mot de passe refusé alors qu'il est bon



clavier AZERTY/QWERTY, verrouillage, cache Windows (klist purge)

Commandes essentielles

gpupdate /force                 # réappliquer les GPO
gpresult /r                     # voir quelles GPO s'appliquent
whoami /user                     # SID de l'utilisateur connecté
nltest /dsgetdc:basile.local        # localiser un DC
repadmin /replsummary            # santé de la réplication (N2)