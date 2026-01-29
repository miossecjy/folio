StockFolio
Documentation d’installation complète
Environnement
•	Système : Debian Linux
•	Frontend : React (Yarn v1)
•	Backend : FastAPI (Python)
•	Base de données : MongoDB
•	Serveur web : Nginx
•	Déploiement : sans Docker
________________________________________
1. Préparation du serveur
Installer les dépendances système :
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl git nginx python3 python3-venv python3-pip build-essential
________________________________________
2. Installation de Node.js 20 et Yarn
Installer Node.js 20 :
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
Vérifier :
node -v
Installer Yarn (v1 obligatoire) :
npm install -g yarn
yarn -v
________________________________________
3. Installation du frontend (Yarn uniquement)
⚠️ Ne jamais utiliser npm sur ce projet.
Se placer dans le dossier frontend :
cd /var/www/Folio/frontend
Installer les dépendances :
yarn install --ignore-engines
Compiler le projet :
yarn build
Vérification locale du build :
npx serve build
Accès navigateur :
http://localhost:3000
Arrêter avec CTRL + C.
________________________________________
4. Configuration Nginx (Frontend + API)
Créer le fichier de configuration :
sudo nano /etc/nginx/sites-available/stockfolio
Contenu du fichier :
server {
    listen 80;

    root /var/www/Folio/frontend/build;
    index index.html;

    location / {
        try_files $uri /index.html;
    }

    location /api/ {
        proxy_pass http://127.0.0.1:3000/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
Activer la configuration :
sudo ln -s /etc/nginx/sites-available/stockfolio /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
________________________________________
5. Installation de MongoDB
Installer MongoDB :
sudo apt install -y mongodb
Démarrer et activer le service :
sudo systemctl enable mongodb
sudo systemctl start mongodb
Créer la base :
mongosh
use StockFolio
exit
________________________________________
6. Installation du backend FastAPI
Se placer dans le dossier backend :
cd /var/www/Folio/backend
Créer l’environnement virtuel :
python3 -m venv venv
source venv/bin/activate
Installer les dépendances :
pip install --upgrade pip
pip install -r requirements.txt
________________________________________
7. Test du backend (manuel)
Lancer l’API :
uvicorn server:app --host 127.0.0.1 --port 3000
Tester :
curl http://127.0.0.1:3000
Réponse attendue :
{"detail":"Not Found"}
➡️ Cela signifie que le backend fonctionne.
Arrêter avec CTRL + C.
________________________________________
8. Création du service systemd (backend.service)
Créer le service :
sudo nano /etc/systemd/system/backend.service
Contenu :
[Unit]
Description=StockFolio Backend (FastAPI)
After=network.target mongodb.service

[Service]
User=www-data
WorkingDirectory=/var/www/Folio/backend
Environment="MONGO_URL=mongodb://localhost:27017"
Environment="DB_NAME=StockFolio"
ExecStart=/var/www/Folio/backend/venv/bin/python -m uvicorn server:app --host 127.0.0.1 --port 3000
Restart=always

[Install]
WantedBy=multi-user.target
Activer le service :
sudo systemctl daemon-reload
sudo systemctl enable backend
sudo systemctl start backend
________________________________________
9. Vérifications finales
Statut du backend :
sudo systemctl status backend
Port utilisé :
sudo ss -tulpn | grep 3000
Test via Nginx :
curl http://127.0.0.1/api
________________________________________
Encadré — Problèmes connus Yarn / Node.js 20
Erreur
The engine "node" is incompatible
Solution
yarn install --ignore-engines
🚫 Ne jamais utiliser npm install.
________________________________________
Encadré — Erreurs backend FastAPI
KeyError: MONGO_URL ou DB_NAME
Cause : variables d’environnement absentes
Solution : vérifier backend.service.
________________________________________
{"detail":"Not Found"}
➡️ Comportement normal : backend actif, route inexistante.
________________________________________
Backend ne démarre pas
Logs :
sudo journalctl -u backend -n 50 --no-pager
________________________________________
Statut final attendu
Composant	État
Frontend	Nginx
Backend	FastAPI (port 3000)
MongoDB	Actif
Accès	http://IP


