GLPI — Utilisation quotidienne

Flux d'un ticket (workflow standard)





Déclaration : utilisateur (portail), mail ou téléphone → tu crées le ticket.



Qualification : catégorie, urgence, matériel concerné (lien avec l'inventaire).



N1 : diagnostic et résolution directe.



N2 : escalade (affectation à un groupe niveau 2, tâche d'escalade obligatoire).



Résolution + suivi : décrire la solution (base de connaissances), clôture.



Satisfaction : l'utilisateur évalue — surveiller ce ratio !

Bonnes pratiques





1 incident = 1 ticket (jamais de traitement « de tête » sans traçabilité).



Toujours renseigner : catégorie, description du diagnostic, temps passé.



Statuts à respecter : Nouveau → En cours (attribué à toi) → En attente → Résolu → Clos.

Raccourcis utiles





+ sur un ticket : ajouter une tâche de suivi.



Vue « Mes tickets » pour ne voir que ton affectation.



Recherche globale en haut : nom d'utilisateur, nom de machine, n° de ticket.

Dépannages fréquents







Problème



Solution





Agent FusionInventory ne remonte pas



vérifier http://<serveur>/glpi/front/inventory.php joignable, réinstaller l'agent avec l'URL exacte, pare-feu





Mails non envoyés



configurer le serveur SMTP dans Configuration > Notifications ; vérifier les files d'attente





Page blanche après mise à jour



php bin/console glpi:database:update --force puis vider le cache navigateur