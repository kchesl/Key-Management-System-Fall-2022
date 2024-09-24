# Key-Management-System-Fall-2022
The Key Management System for the Department of Computer Science Fall 2022 version

# Key Management System

The key management system is a website designed to manage and record the owner of keys with Virginia Tech's Dean's Office in the College of Engineering. Ideally, this will create a uniform and automated platform to access all key data.


## Contributors

* Maheer Aeron
* Nikita Patel
* Joel Anglister
* Nahom Atsbeha
* Omar Kalbouneh -- Project Manager

* Second Key Management group:
* Kirsten Chesley -- Project Manager
* Ryan Dyke
* Haylin Kwok
* Pasha Ranakusuma


## Getting Started
### Setting up SSH keys
5. Run `flask run` 
//flask run will only work if there is a app.py or wsgi.py in the same folder. So you may need to run it in the backend directory or other folder which contains that.

## Getting access to the website

* Go to https://keymanagement.discovery.cs.vt.edu/home to see the website
* To see the website locally, use `npm start` as described above (note that only the frontend on your localhost will update, see how to update the backend below)

## Changing roles

* When you first log into the website, your initial role will be `requestor`. You'll want to set your role as `administrator` or `sudo` to see most of the features offered. To do so, follow the following steps:

1. Log in to cloud.cs.vt.edu (Using your CS account credentials)
2. Click on `discovery` and then `Project: keymanagementsystem`
3. Click on `database`
4. Click on the 3 dots in the top right, then click `Execute Shell`
5. From there, use the following commands:
  a. mongosh
  b. use keymanagementdb
  c. show collections (use this to show all the databases)
  d. db.users.find() (use this command to see a list of all users)
  e. db.users.updateOne({pid: '<pid>'}, {$set: {role: '<role>'}}) (pid and role are in quotes)

## Deploying to Cloud

* To deploy to cloud, follow these steps (used to update backend, but can also be used to update the frontend on https://keymanagement.discovery.cs.vt.edu/home)

* Deploying the backend:
1. Install Docker Desktop and have it running in the background (must also install wsl 2)
2. In your terminal, navigate to the `backend` directory
3. Use the following commands
  a. docker login container.cs.vt.edu (If it asks for credentials, use your CS account credentials)
  b. docker build -t <image name> . (For the backend, the image name is container.cs.vt.edu/maheeraeron/keymanagementsystem/flask-api:latest)
  c. docker push <image name>
4. Go to cloud.cs.vt.edu
5. Click on `discovery` and then `Project: keymanagementsystem`
6. Click on `keymanagement-webapi` (note the image name under `Image:`)
7. Click on the 3 dots in the top right, then click `Redeploy`

* Your backend changes should now be reflected when you run local host
* For frontend, use the same steps, navigating to the `frontend` directory and using the image name on the frontend (which can be found under `keymanagement-website`)

## Important notes

* Arguably, for the potential that this project has in becoming a critical service for Virginia Tech, this is not an easy project.

## TODO (ordered by priority -- start from top down)

* Both the frontend and backend docker images are currently hosted on Dockerhub under the user `maheeraeron`. You should contact Chris Arnold to figured out how to host these images on Gitlab instead (contact below)

* Setup a CI platform so that pushes to master can automatically, build, test and deploy to the CS cloud. This will save tremendous time.

* Setup production Dockerfiles for both the front-end and backend. Suggestions are to use a Web Server software like Nginx or Apache for serving the built files on both ends.

* Consider changing the backend framework to a stricter, opinionated, scaleable framework like ASP.NET or Django.

* Automate ledger entries based on returing // reporting key actions.

* Allow keys to be editable in search keys

* Fix date bug when a new record is made but a day is added (known javascript issue)

* Make edit profile page look pretty

* Allow data tables to export to XLSX instead of CSV

* Coordinate with Jeanette and manually add User documents in MongoDB for current key owners. She will not be able to chase down all current key owners to authenticate into the website. You will also have to manually assign keys that they own and mark the corresponding keys as unavailable in the database. This will also take a majority of your time.

* Come up with a plan to have all departments in the COE conform to a uniform schema for representing their key data. This will take a majority of your time.
