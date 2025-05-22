
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

*Réponse:* Le signal "reg_bank_write_en_s" pipeliné et enregistré sur 3 coups de clock nous permet de savoir si le regsitre à écrire est utilisé.


## Question 5 

*Quelles informations permettent de savoir si le registre S, N ou MEM sont utilisés ?*

*Réponse:* Pour déterminer si les registres S, N ou MEM sont utilisés, il faut examiner les instructions de la porte OR :

- Le registre S est utilisé si la 1ère opérande est lue.
- Le registre N est utilisé si la 2ème opérande est lue.
- Le registre MEM est utilisé si l'opérande source est lue.

## Question 6

*Une détection d’aléa de donnée va influencer quel(s) enable(s) d’étage du pipeline ? A quel
moment? Pourquoi ?*

*Réponse:* Lorsqu’un aléa de donnée est détecté dans le pipeline, cela impacte principalement les signaux "fetch_en_o" et "decode_en_o". Ces deux signaux sont désactivés au cycle où l’instruction en phase DECODE dépend d’une donnée qui n’est pas encore disponible, ce qui permet de geler les étages FETCH et DECODE. Ce gel empêche l’introduction de nouvelles instructions et maintient l’instruction fautive en DECODE jusqu’à ce que la donnée nécessaire soit prête, évitant ainsi toute propagation d’erreur dans les étapes suivantes du pipeline.

## Question 7

*Quel est l’IPC du programme (01_main.S) dans votre circuit logisim?*

-20 cycles   
-16 instructions  

IPC = 16/20 = 4/5 = 0.8

*Quel est l’IPC du programme (02_main.S) dans votre circuit logisim?*

-16 cycles  
-12 instructions   

IPC = 12/16 = 3/4 = 0.75

*Quel est le rôle des intructions NOP placées à la fin des programmes ?*

Les instructions NOP placées à la fin du programme permettent de vidanger correctement le pipeline. Dans un pipeline à 5 étages, même après le fetch de la dernière instruction utile, plusieurs cycles sont encore nécessaires pour que cette instruction atteigne l’étage de write-back. Les NOP assurent donc que le pipeline continue à fonctionner jusqu’à ce que toutes les instructions en cours soient entièrement exécutées. Sans ces NOP, le programme pourrait se terminer prématurément, interrompant certaines instructions avant qu'elles n’aient eu le temps de produire leurs résultats. Tester avec et sans NOP montre que, sans eux, certaines valeurs attendues dans les registres peuvent ne pas être écrites correctement.



