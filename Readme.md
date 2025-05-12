
# Labo 5 - Ryad Bouzourène & Thomas Nguyen

# 1.1 Circuit data_hazard

## Question 1

*Comment savoir si une instruction en cours de décodage est dépendante d’une instruction qui
est pour le moment dans le stage EXECUTE? dans le stage MEMORY_ACCESS? Dans le stage
WRITE_BACK?*

*Réponse:* Grâce aux deux pipelines. En effet les deux pipelines de trois registres en série permettent de stoquer les informations de "si" on va écrire dans la mémoire et "où" ou "dans quel registre" va-t-on écrire l'information. Ce système garde en mémoire les registres qui seront écrit pour les trois dernières instructions. Cela permet de vérifier si une instruction en cours de décodage est dépendante d’une instruction qui est pour le moment dans le stage EXECUTE, MEMORY_ACCESS ou WRITE_BACK. 