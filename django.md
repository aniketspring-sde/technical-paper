create new app in django (project is different than app)
create entity class in modals.py
entity-> managment-> commands -> create class

class Command(BaseCommand):
  entiityName.objects.create()
  it will save in db

add entity in setting.py installed app section
command to migrate data to db
python manage.py makemigrations entity
python manage.py migrate
python manage.py import_ipl
