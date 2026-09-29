VMware vSphere — Notions de base

Vocabulaire





ESXi : hyperviseur installé « bare metal » sur le serveur physique.



vCenter : console centrale qui gère plusieurs ESXi (clusters, migration à chaud).



VM : machine virtuelle ; datastore : stockage des fichiers disque (.vmdk).



vMotion : déplacement d'une VM en marche. Snapshot : point de restauration (à supprimer < 72 h).

Opérations de base (vSphere Client)





Créer une VM : Nouvelle machine virtuelle → nom (convention) → guest OS → 1 vCPU/4 Go pour un poste → finir l'installation puis installer VMware Tools (indispensable).



Snapshot : clic droit VM → Snapshots → Prendre un instantané. Un snapshot n'est pas une sauvegarde.



Monter une ISO : Modifier les paramètres → CD/DVD → fichier ISO du datastore.



Console : onglet Console / Web Console pour accéder à l'écran de la VM.

Dépannages fréquents







Symptôme



Cause classique





VM lente



snapshot oublié, provisioning thin plein, CPU Ready élevé





Plusieurs VM à la même IP



clonage sans changer l'adresse MAC / pas de renouvellement DHCP





« VMware Tools not running »



réinstaller les tools après mise à jour du guest





Datastore plein



consolider les snapshots, nettoyer les ISO et VM orphelines