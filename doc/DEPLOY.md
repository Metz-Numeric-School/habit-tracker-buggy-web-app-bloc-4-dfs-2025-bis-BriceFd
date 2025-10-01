# Procédure de Déploiement

Décrivez ci-dessous votre procédure de déploiement en détaillant chacune des étapes. De la préparation du VPS à la méthodologie de déploiement continu.

Je commence par me connecter au ssh de la VM avec ssh username@ip
ensuite je colle le script donné sur le site d'aapanel : URL=https://www.aapanel.com/script/install_7.0_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO "$URL" ;else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi;bash install_7.0_en.sh aapanel

Quand le script a fini aapanel nous donne 2 ips qui nous amène au site d'aapanel, et je peux ajouter l'ip de la VM sur le site :!
[Screenshot](<Screenshot 2025-10-01 100018.png>)


## Préparation du VPS

Pour le VPS, j'ai fait en local après avoir cloné mon repo github :
git add .
git commit -m "initial commit"
git push -u vps main

Puis sur la VM :
mkdir /var/deploy
git init --bare
git --work-tree=/www/wwwroot/172.17.4.9 --git-dir=/var/deploy checkout -f main
composer install



## Méthode de déploiement

Todo...
