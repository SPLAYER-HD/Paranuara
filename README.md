# Paranuara
=============
# Steps to test API

### 1 Build docker (estimated time building image 8 minutes)
```bash
sudo docker-compose -f local.yml build
```

### 2 Load models on database
```bash
sudo docker-compose -f local.yml run --rm django python manage.py makemigrations
sudo docker-compose -f local.yml run --rm django python manage.py migrate
```

### 3 UP docker
```bash
sudo docker-compose -f local.yml up
```

### 4 Load data from json (if you are going to change the json files please keep the same format and let them in the same folder)
```bash
sudo docker-compose -f local.yml run --rm django python manage.py populate  companies.json company
sudo docker-compose -f local.yml run --rm django python manage.py populate  people.json person
```
### 5 Use API
- Given a company, the API needs to return all their employees. 

    http://localhost:8000/companies/STRALUM/employees

    - Provide the appropriate solution if the company does not have any employees.

        First of all you have to know who company has employees, for suppliyed data is NETBOOK.

        http://localhost:8000/companies/NETBOOK/employees

        This service returns an URL to associate the citizens who do not have an associated company. Similar to this: 

        http://localhost:8000/companies/NETBOOK/add_free_employees/ 

- Given 2 people, provide their information (Age, Name, Address, phone) and the list of their friends in common which have brown eyes and are still alive.

    http://localhost:8000/citizens/friends_in_common?users=XXX,XXX

    Where XXX and XXX has to be the IDs of the citizens, (possible values 1000,988) to search their IDs use this url:

    http://localhost:8000/citizens

- Given 1 people, provide a list of fruits and vegetables they like (possible value 1000).

    http://localhost:8000/citizens/XXX/get_food

    Where XXX is the citizen ID who you want to find.

If you want in the project root there is a Postman export with the End Points. (called: paranuara.postman_collection.json)

### 6 Validate unit test and API Test
```bash
sudo docker-compose -f local.yml run --rm django pytest
```

# Additional Information

### Celery Flower (the process to asociate citizens free to an empty company is released by celery)
Server: http://localhost:5555/

User: paranuara

Password: P4r4nu4r4

### PostgreSql Credentials
POSTGRES_HOST=localhost

POSTGRES_PORT=5432

POSTGRES_DB=paranuara

POSTGRES_USER=sBLRWyyPsInwHftmHAWmYJURGWBGFpLs

POSTGRES_PASSWORD=tuXL3XSF8O7tsGrcGHoMos4tVNtL3tnrRshSCZokGnIfk4ArDyzaa297k2WgQPSL

# TO DO
Only get friends service has tests. Load unit test and integration test to others services

Adapt json files to use fixtures instead of use BaseCommand 
