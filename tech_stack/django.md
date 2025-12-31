# DJANGO FORMAL SPECIFICATION 

## 12 PRIMARY DJANGO KEYWORDS

### 1. **MODEL** - ORM & Database Models
```python
from django.db import models
from django.core.validators import EmailValidator

class User(models.Model):
    """User model with validation."""
    
    class Status(models.TextChoices):
        ACTIVE = 'active', 'Active'
        INACTIVE = 'inactive', 'Inactive'
    
    name = models.CharField(max_length=100)
    email = models.EmailField(unique=True, validators=[EmailValidator()])
    status = models.CharField(choices=Status.choices, default=Status.ACTIVE)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    class Meta:
        db_table = 'users'
        ordering = ['-created_at']
        indexes = [
            models.Index(fields=['email']),
            models.Index(fields=['status', '-created_at']),
        ]
    
    def __str__(self):
        return self.name
```

### 2. **MIGRATION** - Schema Migrations
```bash
# Create migrations
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Create migration with custom operations
python manage.py makemigrations --empty --name add_custom_field
```

### 3. **VIEW** - Request Handlers
```python
from django.views import View
from django.views.generic import ListView, CreateView
from django.http import JsonResponse
from django.views.decorators.http import require_http_methods

# Function-based view
@require_http_methods(["GET", "POST"])
def user_list(request):
    if request.method == 'GET':
        users = User.objects.all()
        return render(request, 'users/list.html', {'users': users})

# Class-based view
class UserListView(ListView):
    model = User
    template_name = 'users/list.html'
    context_object_name = 'users'
    paginate_by = 20

# API view with JSON response
class UserAPIView(View):
    def get(self, request, user_id):
        user = User.objects.get(id=user_id)
        return JsonResponse({
            'id': user.id,
            'name': user.name,
            'email': user.email
        })
```

### 4. **URL** - URL Routing
```python
# urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('users/', views.UserListView.as_view(), name='user-list'),
    path('users/<int:pk>/', views.UserDetailView.as_view(), name='user-detail'),
    path('users/create/', views.UserCreateView.as_view(), name='user-create'),
]
```

### 5. **FORM** - Form Handling
```python
from django import forms
from django.core.exceptions import ValidationError

class UserForm(forms.ModelForm):
    """User creation form."""
    
    class Meta:
        model = User
        fields = ['name', 'email']
    
    def clean_email(self):
        email = self.cleaned_data['email']
        if User.objects.filter(email=email).exists():
            raise ValidationError('Email already registered')
        return email
```

### 6. **QUERY** - ORM Query Operations
```python
# Basic queries
User.objects.all()
User.objects.get(id=1)
User.objects.filter(status='active')
User.objects.filter(status='active').count()

# Advanced queries
User.objects.filter(
    status='active'
).exclude(
    email__endswith='test.com'
).order_by('-created_at')

# Aggregation
from django.db.models import Count, Sum
User.objects.annotate(
    post_count=Count('posts'),
    total_views=Sum('posts__views')
).filter(post_count__gt=0)

# Raw SQL
User.objects.raw('SELECT * FROM users WHERE status = %s', ['active'])
```

### 7. **AUTHENTICATION** - User Auth & Permissions
```python
from django.contrib.auth.models import User, Permission
from django.contrib.auth.decorators import login_required

# User creation
user = User.objects.create_user(
    username='john',
    email='john@example.com',
    password='secure_password'
)

# Permissions
@login_required
def protected_view(request):
    if request.user.has_perm('app.delete_user'):
        # Permission granted
        pass
```

### 8. **MIDDLEWARE** - Request/Response Processing
```python
class LoggingMiddleware:
    """Log all requests."""
    
    def __init__(self, get_response):
        self.get_response = get_response
    
    def __call__(self, request):
        logger.info(f"{request.method} {request.path}")
        response = self.get_response(request)
        logger.info(f"Status: {response.status_code}")
        return response
```

### 9. **SIGNAL** - Event Handling
```python
from django.db.models.signals import post_save
from django.dispatch import receiver

@receiver(post_save, sender=User)
def user_created(sender, instance, created, **kwargs):
    """Send welcome email on user creation."""
    if created:
        send_welcome_email(instance.email)
```

### 10. **TEMPLATE** - Template Rendering
```html
{% extends 'base.html' %}

{% block content %}
<div class="user-list">
  {% for user in users %}
    <div class="user-card">
      <h3>{{ user.name }}</h3>
      <p>{{ user.email }}</p>
      {% if user.status == 'active' %}
        <span class="badge">Active</span>
      {% endif %}
    </div>
  {% endfor %}
</div>
{% endblock %}
```

### 11. **CELERY** - Asynchronous Tasks
```python
from celery import shared_task

@shared_task
def send_email(user_id):
    """Send email asynchronously."""
    user = User.objects.get(id=user_id)
    send_email_to(user.email)

# Trigger task
send_email.delay(user_id=1)
```

### 12. **TESTING** - Unit & Integration Tests
```python
from django.test import TestCase, Client
from django.urls import reverse

class UserTestCase(TestCase):
    def setUp(self):
        self.user = User.objects.create_user(
            username='testuser',
            email='test@example.com',
            password='testpass'
        )
    
    def test_user_creation(self):
        self.assertEqual(User.objects.count(), 1)
        self.assertEqual(self.user.username, 'testuser')
    
    def test_user_list_view(self):
        response = self.client.get(reverse('user-list'))
        self.assertEqual(response.status_code, 200)
        self.assertContains(response, 'testuser')
```

## BEST PRACTICES
1. Use ORM for queries
2. Leverage migrations
3. Implement proper authentication
4. Use class-based views
5. Cache strategically
6. Test thoroughly
7. Use signals sparingly
8. Optimize database queries
9. Implement proper error handling
10. Document API endpoints

