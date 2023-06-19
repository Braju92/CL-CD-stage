# shared-push 

Tags: 
* local: Necessario per associare un runner locale e il job con lo stesso tag.

Stages:
* deploy: Il job è associato allo stage di deploy e esegue il build di tutte le immagini Docker presenti in una cartella /docker e il push di queste immagini su Dockerhub.

Image:
* docker:latest: Immagine usata per la pipeline che permette di avere l'ultima versione di Docker ufficiale, con ultimi bug fixes e funzionalità. Controllare che gli ultimi aggiornamenti siano compatibili con il progetto.

Services:
* dind: Docker-in-Docker consente di eseguire Docker all'interno di un contenitore Docker, quindi consente di eseguire un'istanza Docker all'interno di un contenitore dedicato durante l'esecuzione delle fasi della pipeline.

Variables:
* IMG_DIR: Directory dentro /docker/IMG_DIR che contiente un Dockerfile.
* IMG: Specifica il nome dell'immagine Docker di cui si deve eseguire il build e il push su DockerHub, è estratta dal Dockerfile.
* TAG: Specifica il tag dell'immagine da caricare su DockerHub, è estratta dal Dockerfile.
* DOCKERHUB_USERNAME: Variabile salvata nei settings di GitLab che contiene l'username di DockerHub con cui autenticarsi.
* DOCKERHUB_PASSWORD: Variabile salvata nei settings di GitLab che contiene un token di accesso per l'autenticazione si DockerHub.

Script:
* echo "Building image...": Stampa un messaggio per indicare l'inizio della fase di costruzione delle immagini.
* docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD: Esegue il login a Docker Hub utilizzando le credenziali fornite tramite le variabili di ambiente $DOCKERHUB_USERNAME e $DOCKERHUB_PASSWORD.
* for IMG_DIR in pwd/docker/*; do: Itera nelle directory sotto pwd/docker.
* if [ -d "\$IMG_DIR" ]; then: Verifica se l'elemento corrente nel loop è una directory.
* cd \$IMG_DIR: Entra nella directory dell'immagine corrente.
* IMG=\$(grep 'IMG=' Dockerfile | cut -d'=' -f2): Estrae il valore della variabile IMG dal file Dockerfile dell'immagine corrente.
* TAG=\$(grep 'TAG=' "\$IMG_DIR/Dockerfile" | cut -d'=' -f2): Estrae il valore della variabile TAG dal file Dockerfile dell'immagine corrente.
* echo "Building image \$IMG:\$TAG": Stampa un messaggio per indicare l'inizio della costruzione dell'immagine corrente.
* docker "build -t \$IMG:\$TAG \$IMG_DIR": Costruisce un'immagine Docker utilizzando il Dockerfile presente nella directory corrente e la tagga con il formato IMG:TAG.
* echo "Pushing image \$IMG:\$TAG": Stampa un messaggio per indicare l'inizio del push dell'immagine corrente.
* docker push "\$IMG:\$TAG": Esegue il push dell'immagine Docker nel repository remoto (in questo caso, Docker Hub).
* echo "Image \$IMG:\$TAG pushed successfully": Stampa un messaggio per indicare il successo del push dell'immagine corrente.
* cd ..: Torna alla directory precedente.
* La pipeline ripete i passaggi 4-13 per ogni directory trovata sotto pwd/docker.
