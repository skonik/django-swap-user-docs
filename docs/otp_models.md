One time password(OTP) functionality allows you not to store passwords in your databases.
It lets to generate passwords valid for a certain amount of time and usable only once.

![Email and Phone OTP](./media/images/django_user_swap_02.jpeg)

To use specified model with OTP functionality follow the steps below.
### Step 1 - change `INSTALLED_APPS`
Add the following apps below to `INSTALLED_APPS` in order to swap to the specified OTP model.

=== ":material-email-lock: to_email_otp"

    ``` python
    "swap_user",
    "swap_user.to_email_otp",
    ```

=== ":material-phone-lock: to_phone_otp"

    ``` python
    "swap_user",
    "swap_user.to_phone_otp",
    ```

---

### Step 2 - set `AUTH_USER_MODEL`
=== ":material-email-lock: to_email_otp"

    ``` python
    AUTH_USER_MODEL = "swap_to_email_otp.EmailOTPUser"
    ```

=== ":material-phone-lock: to_phone_otp"

    ``` python
    AUTH_USER_MODEL = "swap_to_phone_otp.PhoneOTPUser"
    ```

---

### Step 3 - replace `django.contrib.admin`
In order to render django admin pages properly with one time password login enabled you should replace `django.contrib.admin` in
your `INSTALLED_APPS` to the one below:

=== ":material-email-lock: to_email_otp"

    ``` python
    AUTH_USER_MODEL = "swap_user.to_email_otp.apps.SiteConfig"
    ```

=== ":material-phone-lock: to_phone_otp"

    ``` python
    AUTH_USER_MODEL = "swap_user.to_phone_otp.apps.SiteConfig"
    ```

---

### Step 4 - apply migrations
=== ":material-email-lock: to_email"

    ``` sh
    python manage.py migrate swap_to_email
    ```

=== ":material-phone-lock: to_phone"

    ``` sh
    python manage.py migrate swap_to_phone
    ```

---