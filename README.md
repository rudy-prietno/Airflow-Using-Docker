# Airflow-Using-Docker
This repo use for setup airflow using Dockerfile and Docker Compose.

Speksification:
- 1 webserver
- 1 scheduler
- 1 monitoring
- 8 workers

after you run start.sh, docker-compose semi automatic running Dockerfile to build images and running containers.
and also, you can see in your folder you have "ciput_airflow" with 2 folder dags and plugins, and 1 file "airflow.cfg".

So, you can put your code DAG's into folder dags and you can put code custom operator in folder plugins.
and also, you edit airflow configuration in file "airflow.cfg".

and then, if you do something in 3 of component, if you don't show changes you must do comment "docker restart webserver scheduler workers" together in the same time.

for the last, in this configuration I put login admin
if you don't have account, you can create with this way:
- go to access you webserver container:
   - docker exec -ti --user root webserver
   
     after that call the python:
     
      - python3
      
        and the put this:
        
            import airflow
            from airflow import models, settings
            from airflow.contrib.auth.backends.password_auth import PasswordUser
            user = PasswordUser(models.User())
            user.username = 'username'
            user.email = 'your email address'
            user.password = 'your password'
            user.superuser = True ---- if you give the permission like a root, if false user just can see like a user read only
            session = settings.Session()
            session.add(user)
            session.commit()
            session.close()
            exit()
            
            
