# Structure-d-un-projet-Django
Projet Django


# Dans settings.py du projet 

      STATIC_URL = '/static/'
      MEDIA_URL = '/media/'
      STATICFILES_DIRS = [
          os.path.join(BASE_DIR,'static')
      ]
      STATIC_ROOT= os.path.join(BASE_DIR, '../static_cdn')
      MEDIA_ROOT= os.path.join(BASE_DIR, '../media_cdn')
 
 # Dans le urls.py du projet 
 
      from django.conf import settings
      from django.conf.urls.static import static
      
      
      
      
      
      
      if settings.DEBUG :
          urlpatterns += static(settings.MEDIA_URL, document_root = settings.MEDIA_ROOT)
          urlpatterns += static(settings.STATIC_URL, document_root = settings.STATIC_ROOT)

          
 # Exemple admin.py 
      from django.contrib import admin
      from . import models
      from tinymce import HTMLField
      from django.utils.safestring import mark_safe
      # Register your models here.


      @admin.register(models.Categorie)
      class CategorieAdmin(admin.ModelAdmin):
          list_display = ('nom', 'date_add', 'date_upd', 'statut',)
          list_filter = ('date_add', 'date_upd', 'statut',)
          list_search = ('nom')
          ordering = ('nom',)
          list_per_page = 5
          actions = ('active', 'desactive',) 
          def active(self, request, queryset):
              queryset.update(statut=True)
              self.message_user(request, 'Activer une categorie')
          active.short_description = 'active categorie'

          def desactive(self, request, queryset):
              queryset.update(statut = False)
              self.message_user(request, 'Desactiver une categorie')
          desactive.short_description = 'desactive categorie'



      @admin.register(models.Article)
      class ArticleAdmin(admin.ModelAdmin):
          list_display = ('titre', 'date', 'description', 'content', 'date_add', 'date_upd', 'statut', 'categorie',   'auteur','view_image',)
          list_filter = ('date_add', 'date', 'date_upd', 'statut',)
          list_search = ('titre')
          ordering = ('titre',)
          list_per_page = 5
          readonly_fields = ['detail_image']
          filter_horizontal = ('tag',)
          actions = ('active', 'desactive',)

          def active(self, request, queryset):
              queryset.update(statut=True)
              self.message_user(request, 'Activer une Article')
          active.short_description = 'active Article'

          def desactive(self, queryset, request):
              queryset.update(statut = False)
              self.message_user(request, 'Desactiver une Article')
          desactive.short_description = 'desactive Article'

          def view_image(self, obj):
              return mark_safe('<img src = "{url}" width ="100px" height ="100px" />'.format(url = obj.image.url))

          def detail_image(self, obj):
              return mark_safe('<img src = "{url}" width ="100px" height ="100px" />'.format(url = obj.image.url))



      @admin.register(models.Commentaire)
      class CommentaireAdmin(admin.ModelAdmin):
          list_display = ('date', 'message', 'date_add', 'date_upd', 'statut', 'article', 'nom', 'view_image',)
          list_filter = ('date_add', 'date', 'date_upd', 'statut',)
          list_search = ('nom',)
          ordering = ('nom',)
          list_per_page = 5

          readonly_fields = ['detail_image']
          actions = ('active', 'desactive',) 
          def active(self, request, queryset):
              queryset.update(statut=True)
              self.message_user(request, 'Activer une Commentaire')
          active.short_description = 'active Commentaire'

          def desactive(self, request, queryset):
              queryset.update(statut = False)
              self.message_user(request, 'Desactiver une Commentaire')
          desactive.short_description = 'desactive Commentaire'
          def view_image(self, obj):
              return mark_safe('<img src = "{url}" width ="100px" height ="100px" />'.format(url = obj.image.url))

          def detail_image(self, obj):
              return mark_safe('<img src = "{url}" width ="100px" height ="100px" />'.format(url = obj.image.url))



      @admin.register(models.Comment)
      class CommentAdmin(admin.ModelAdmin):
          list_display = ('nom', 'email', 'web', 'message', 'date_add',)
          list_filter = ('date_add',)
          list_serach = ('nom',)
          list_per_page = 5
          ordering = ('nom',)



      @admin.register(models.Tag)
      class TagAdmin(admin.ModelAdmin):
          list_display = ('nom', 'date_add', 'date_upd', 'statut',)
          list_filter = ('date_add', 'date_upd', 'statut',)
          list_serach = ('nom')
          list_per_page = 5
          ordering = ('nom',)



## creation d'environnement virtuel sur linux
# Installer virtualenv
      pip install virtualenv

# Acceder au dossier du projet
     cd my_folder

# Créer l'environnement virtuel  `venv`
      virtualenv venv


# Indiquer l'interpreteur (2.7) à utiliser pour notre environnement 'venv'
      virtualenv -p /usr/bin/python2.7 venv

# Activer `venv`
      source venv/bin/activate

# Désactiver `venv`
       deactivate

# Générer les bibliothéques utilisées
      venv/bin/pip freeze > requirements.txt

# Installer les bibliothèques automatiquement depuis le fichier 'requirements.txt' 
      venv2/bin/pip install -r requirements.txt



## creation d'environnement virtuel sur windows

# Installer virtualenv
       pip install virtualenv

# Acceder au dossier du projet
       cd my_folder

# Créer l'environnement virtuel  `venv`
       virtualenv venv

# Indiquer l'interpreteur (2.7) à utiliser pour notre environnement 'venv'
       virtualenv -p /usr/bin/python2.7 venv

# Activer `venv`
       venv\Scripts\activate

# Désactiver `venv`
       venv\Scripts\deactivate

# Générer les bibliothéques utilisées
      venv/bin/pip freeze > requirements.txt

#Installer les bibliothèques automatiquement depuis le fichier 'requirements.txt' 
      venv2/bin/pip install -r requirements.txt
      
# Revision projet Django
https://learndjango.com/tutorials/django-slug-tutorial

# Installer autoSulgField
https://pypi.org/project/django-autoslug/

