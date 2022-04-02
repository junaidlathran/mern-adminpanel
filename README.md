# Deployment Guide
# Pull Docker images from my personal Gitlab Public Container Registry 
 * docker pull registry.gitlab.com/junaidlathransoft/mern-frontend:latest
 * docker pull registry.gitlab.com/junaidlathransoft/mern-backend:latest
 * docker pull registry.gitlab.com/junaidlathransoft/mern-db:latest

# Clone App's Repo 
 * git clone https://github.com/junaidlathran/mern-adminpanel.git 

# Deploy the compose file through Docker Swarm
 * docker swarm init
 * docker stack deploy --compose-file docker-compose.yaml mern

# Access Application's Frontend
 * Application will be running on "<b>http://localhost:3000</b>"

# Cron Job
 * Cron is scheduled in the Mongodb container. 
 * Enter mongodb container -> docker exec -it mern_mongo.1.(press-tab to autofill the nameid) /bin/bash
 * After logging in to container enter crontab -> crontab -e .The script for cron is stored at <b>/root</b> inside the container
  
# Delete Data on Insert after Specific Amount Of Days
 * The Script for doing this task is placed at <b>/root</b> inside mongodb container with the name of <b>scheduledDelete.sh</b>.
 * Run the Script and Pass an argument of number of days and the data will be deleted. -> "<b> ./scheduledDelete.sh 5 </b>"
 
 * Another way of Scheduling Deletion of Data after insertion is through javascript
 * Enter App's backend container -> docker exec -it mern_api.1.(press-tab to autofill the nameid) /bin/bash
 * Redirect to /usr/src/app/models and open users.js and check line 10 
 * On Schema level I added that after insertion data will be deleted after 10 days.
 * Reference of this approach: reference:https://stackoverflow.com/questions/38472125/delete-mongodb-document-at-specific-time

# Database Backup & Restore
 * Scheduled Backups will be saved at <b>/root/backups/(Date Of Backup)/userlist</b> inside mongodb continer
 * To Restore DB execute this command -> mongorestore --db userlist --drop /root/backups/(Date Of Backup)/userlist
  
# Technoligies Used
  * React v18.0.0
  * Node v16.14.2
  * Mongo v5.0.6
  
