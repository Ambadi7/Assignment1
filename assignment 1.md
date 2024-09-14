```python
import time
from django.db.models.signals import post_save
from django.dispatch import receiver
from django.contrib.auth.models import User
from django.utils.timezone import now


@receiver(post_save, sender=User)
def user_saved_handler(sender, instance, **kwargs):
    print(f"Signal received for user: {instance.username} at {now()}")
    print("Handler started processing...")
    time.sleep(5)  
    print(f"Handler finished processing at {now()}")


def create_user():
    print(f"Creating user at {now()}")
    user = User.objects.create_user(username='test_user', password='password')
    print(f"User creation finished at {now()}")


create_user()
