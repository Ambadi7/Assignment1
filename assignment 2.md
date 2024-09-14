
```python
import threading
from django.db.models.signals import post_save
from django.dispatch import receiver
from django.contrib.auth.models import User
from django.utils.timezone import now


@receiver(post_save, sender=User)
def user_saved_handler(sender, instance, **kwargs):
    print(f"Signal received for user: {instance.username} at {now()}")
    print(f"Signal handler is running in thread: {threading.current_thread().name}")


def create_user():
    print(f"Creating user at {now()}")
    print(f"User creation is running in thread: {threading.current_thread().name}")
    user = User.objects.create_user(username='test_user', password='password')
    print(f"User creation finished at {now()}")


create_user()
