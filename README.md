Tο παρον repository περιχερει την εργασια του μαθηματος DevOps 2026 

Η εργασία επικεντρώνεται στην εφαρμογή βασικών πρακτικών DevOps, χρησιμοποιώντας Docker ,Ansible και Jekins

Οδηγιες εγκαταστασης :

Docker install:

sudo apt install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
newgrp docker
docker --version
docker compose version

Αν θελουμε να τρεξουμε μονο docker η εντολη ειναι docker compose up  --build

Jenkins install :

Jenkinsfile : Ορίζει τα stages του CI/CD pipeline
jenkins/docker-compose.yml : Εκκίνηση του Jenkins server.
docker-compose.yml : Εκκίνηση της εφαρμογής.
-φτιάχνουμε repository-
/bill/appointments-project$ git init
git remote add origin https://github.com/billkogias/Devops_2026_ergasia
git config --global user.email "billkogias3@gmail.com"
git config --global user.name "billkogias"
git add .
git commit -m "initial commit with jenkins pipeline"
cd ~/bill/appointments-project/jenkins
# Start Jenkins container
docker compose up -d
# Wait for Jenkins to start (30 seconds)
sleep 30
# Check if Jenkins is running
docker ps | grep jenkins
# View logs (wait for "Jenkins is fully up and running")
docker compose logs -f
Ανοίγουμε browser στο http://localhost:8081
1. Manage Jenkins → Plugins → Available plugins
2. Εγκαθηστουμε  τα παρακάτω plugins:
- Docker Pipeline
- Git plugin
- Pipeline
- Maven Integration plugin
3. Κάνε tick: "Restart Jenkins when installation is complete"
4. Περιμένουμε το restart (30-60 δευτερόλεπτα)
5. Refresh browser: http://localhost:8081
Βήμα 4: Δημιουργία Pipeline Job
Create New Item
1. Πατάμε "New Item" (πάνω αριστερά)
2. Item name: `appointments-pipeline`
3. Type: Επιλεγουμε "Pipeline"
4. Πάτα OK
Configure Pipeline
Στην ενότητα Pipeline:
Field | Value |
|-------|-------|
| **Definition** | Pipeline script from SCM |
| **SCM** | Git |
| **Repository URL** | `https://github.com/billkogias/Devops_2026_ergasia` |
| **Branch Specifier** | `*/main` |
| **Script Path** | `Jenkinsfile` |
Πάτα Save
## Εκτέλεση Pipeline
### Manual Trigger (Build Now)
1. Πηγαίνουμε στο job: appointments-pipeline
2. Πατάμε "Build Now" (αριστερά)
3. Στο Build History θα εμφανιστεί #1
Βασίλης Η επιστροφή Σελίδα 23. Στο Build History θα εμφανιστεί #1
4. Πάτα στο #1 → Console Output
docker exec -it jenkins-server bash
apt-get update
apt-get install -y libatomic1
exit
docker exec -it -u root jenkins-server bash
apt-get update
apt-get install -y docker.io
exit
docker exec -it -u root jenkins-server bash
curl -L "https://github.com/docker/compose/releases/download/v2.24.5/docker-
compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
# Έλεγχος
docker-compose --version
exit

