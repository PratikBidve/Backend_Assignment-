Starting Structure:

myproject/
  docker-compose.yml
  docker-compose.prod.yml
  Dockerfile
  requirements.txt
  manage.py
  myproject/
    __init__.py
    settings.py
    celery.py
    urls.py
    wsgi.py
  apps/
    core/
      __init__.py
      models.py
      tasks.py
      views.py
  nginx/
    nginx.conf

Application Startup commands:

# Build and start all services
docker compose up --build -d

# Run database migrations
docker compose exec web python manage.py migrate

# Create a superuser for the admin panel
docker compose exec web python manage.py createsuperuser

# Check that all services are running
docker compose ps


System Design Questions:
● How do you handle cache stampede when 10,000 users' caches expire
simultaneously?
Ans:  I would use extra redis instaces to avoid the expiration cache stampede

● How would your cache strategy change if messages could be edited after being
sent?
Ans:  So I can only cache the data of chats when the user asks a new question or I would use redis push command without nx so it would just update the existing message 

● What would you cache differently if the platform had 1 million users?
Ans: I will do the horrizontal scalling of django app, add read replicas for database.