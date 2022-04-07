#Éditeur de formulaire OCA

#Image de marque d'une attestation (branding)
Un des objetifs de la preuve de concept était de vérifier la possibilité d'afficher une image de marque (branding) pour une attestation. 
Par exemple, pouvoir afficher l'équivalent visuelle d'une carte (assurance maladie, permis de conduire, etc.) Pour ce faire, la tecnologie OCA offre
la couche (overlay) CredentialLayoutOverlay. Elle permet de définir la structure d'un affichage en HTML sous forme de YAML et de css. Il est possible de 
définir des lignes, des colonnes, des images des libéllés et des champs textes bindés sur des données d'entrées.

##Construction de la mise en page via le YAML
La mise en page de l'image de marque d'une attestation s'effectue via une document YAML. Il y a peu de commande à connaître mais l'expérience
développeur n'est pas très bonne. Cela se fait pas essaie erreur et le processus est relativement long. Il serait bon d'envisager le développement
d'un éditeur pour aider les éventuels émetteurs d'attestation.

##Performance
Pour effectuer le rendu HTML d'une attestation, la composante WebView a été utilisée. Pour accélérer l'affichage des images, la librairie OCA utilisée a
du être patché afin de supporter les images encodées en base64 (embedded). Originalement, la librairie supporte uniquement des références SAI vers 
les images. Le téléchargement à partir du dépôt OCA est lent. Malgré cette optimisation, l'affichage reste peu performant (perceptible par l'utilisateur).
Il faudra fort probablement effectuer des travaux pour l'améliorer. Dans l'état actuel, il ne serait pas envisageable d'utiliser cette méthode
pour afficher une liste d'attestation avec image de marque. Le rendu de cette liste serait trop lent.
