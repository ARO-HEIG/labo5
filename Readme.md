
# Labo 5 - Ryad Bouzourène & Thomas Nguyen

# 1.1 Circuit data_hazard

## Question 1

*Comment savoir si une instruction en cours de décodage est dépendante d’une instruction qui
est pour le moment dans le stage EXECUTE? dans le stage MEMORY_ACCESS? Dans le stage
WRITE_BACK?*

*Réponse:* Grâce aux deux pipelines. En effet les deux pipelines de trois registres en série permettent de stoquer les informations de "si" on va écrire dans la mémoire et "où" ou "dans quel registre" va-t-on écrire l'information. Ce système garde en mémoire les registres qui seront écrit pour les trois dernières instructions. Cela permet de vérifier si une instruction en cours de décodage est dépendante d’une instruction qui est pour le moment dans le stage EXECUTE, MEMORY_ACCESS ou WRITE_BACK. 

## Question 2 

*Est-ce que cela pose un problème si une instruction en cours de décodage dépend du résultat
d’une instruction qui est au stage WRITE_BACK?*

*Réponse:* Oui celà peut causer problème, on appelle ce genre de dépendance des RAW (Read after Write). Après avoir fetch l'instruction on la "lit", on la décode. Cette étape va aller lire dans les registres concernée par cette instruction. Comme cette istruction dépend du résultat d’une instruction qui est au stage WRITE_BACK, alors le décode sera faussé vu que les registres concernés n'auront pas encore été mis à jour.

## Question 3 

*Quels informations doivent être mémorisées pour chaque instruction ?* 

*Réponse:* "Si" on écrit dans un registre ou non, celà correspond à l'entrée "reg_bank_write_en_i". Et le registre à écrire, celà correspond à l'entrée "adr_reg_d_i".

## Question 4 

*Quelles informations permettent de savoir si le registre D est utilisé ?*

*Réponse:* Le signal "reg_bank_write_en_s" pipeliné et enregistré sur 3 coups de cloches nous permet de savoir si le regsitre à écrire est utilisé.
