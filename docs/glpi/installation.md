GLPI — Installation (Debian + Apache)

Prérequis





VM Debian 12, 2 vCPU / 4 Go RAM / 20 Go disque.



Accès sudo, ouverture des ports 80/443.

Installation rapide

# 1. Paquets
sudo apt update && sudo apt install -y apache2 mariadb-server php php-mysql php-mbstring php-curl php-gd php-intl php-xml php-zip php-bz2 php-imap

# 2. Base de données
sudo mysql_secure_installation
sudo mysql -e "CREATE DATABASE glpidb; CREATE USER 'glpi'@'localhost' IDENTIFIED BY 'MotDePasseFort!'; GRANT ALL ON glpidb.* TO 'glpi'@'localhost'; FLUSH PRIVILEGES;"

# 3. GLPI
wget https://github.com/glpi-project/glpi/releases/download/10.0.x/glpi-10.0.x.tgz
sudo tar -xvzf glpi-10.0.x.tgz -C /var/www/html/
sudo chown -R www-data:www-data /var/www/html/glpi
sudo chmod -R 755 /var/www/html/glpi

# 4. Terminer via le navigateur
# http://<ip-serveur>/glpi → assistant d'installation
# Identifiants par défaut : glpi / glpi (À CHANGER immédiatement)

Post-installation





Supprimer le fichier d'installation : sudo rm /var/www/html/glpi/install/install.php



Activer HTTPS (Let's Encrypt) : sudo apt install certbot python3-certbot-apache && sudo certbot --apache



Planifier les sauvegardes de glpidb : mysqldump glpidb | gzip > /backup/glpi_$(date +%F).sql.gz