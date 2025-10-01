# TODO

Suite à un audit effectué en amont, voici les failles et les bugs qui ont été identifés comme prioritaire.

## FAILLES

* Des utilsateurs non admin ont des accès à l'interface de gestion des utilisateurs :
- j'ai rajouté dans config/routes.json : ``"guard": "App\\Guard\\AdminGuard"``

* Les mots de passes ne sont pas chiffrée en base de données... :
- j'ai ajouté ça dans RegisterController.php :
``$user['password'] = password_hash($user['password'], PASSWORD_BCRYPT);``
et j'ai changé la vérification de mot de passe dans SecurityController.php :
`if(password_verify($password, $user->getPassword())) {}`
Les utilisateurs créés avec le script n'auront pas le mot de passe haché mais ceux crées par le site auront leur mot de passe haché

* Des injections de type XSS ont été détéctées sur certains formulaires 

* On nous a signalé des injections SQL lors de la création d'une nouvelles habitudes
  * exemple dans le champs "name" : foo', 'INJECTED-DESC', NOW()); -- :
  pour éviter les injections SQL j'ai fait une requête préparée : 
  ``$sql = "INSERT INTO habits (user_id, name, description, created_at) VALUES (:user_id, :name, :description, NOW())";
        $query = $this->getConnection()->prepare($sql);
        $query->bindParam(':user_id', $data['user_id']);
        $query->bindParam(':name', $name);
        $query->bindParam(':description', $description);
        $query->execute();
        return $this->getConnection()->lastInsertId();``

## BUGS

* Une 404 est détéctée lors de l'accès à l'URL ``/habit/toggle`` : je ne vois pas de template ni de route pour cet URL alors je laisse
* Fatal error: Uncaught Error: Class "App\Controller\Api\HabitsController" lorsque l'on accède à l'URL  ``/api/habits`` :
j'ai rajouté un "s" à ``class HabitsController extends AbstractController`` dans HabitsController.php

**ATTENTION : certains bugs n'ont pas été listé**

Bug non listé : 
Il n'y a pas de template de page pour gérer les habitudes alors j'ai changé ce code pour qu'il affiche juste la page habitude user :
``<a href="/admin/habits" class="btn btn-outline-primary btn-sm">Gérer les habitudes</a>``
j'ai enlevé le /admin :
`` <a href="/habits" class="btn btn-outline-primary btn-sm">Gérer les habitudes</a>``
