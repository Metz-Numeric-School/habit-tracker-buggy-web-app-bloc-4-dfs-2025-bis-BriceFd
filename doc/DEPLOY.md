# Procédure de Déploiement

Décrivez ci-dessous votre procédure de déploiement en détaillant chacune des étapes. De la préparation du VPS à la méthodologie de déploiement continu.

Je commence par me connecter au ssh de la VM avec ssh username@ip
ensuite je colle le script donné sur le site d'aapanel : URL=https://www.aapanel.com/script/install_7.0_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO "$URL" ;else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi;bash install_7.0_en.sh aapanel

Quand le script a fini aapanel nous donne 2 ips qui nous amène au site d'aapanel :!
[Screenshot](<Screenshot 2025-10-01 100018.png>)


## Préparation du VPS

Todo...

## Méthode de déploiement

Todo...
