Example of settings is shown below.

```python
# settings.py
SWAP_USER = {
    # services
    "OTP_SENDER_CLASS": "swap_user.otp.senders.StdOutOTPSender",
    "GET_OTP_SERVICE_CLASS": "swap_user.otp.services.GetOTPService",
    "CHECK_OTP_SERVICE_CLASS": "swap_user.otp.services.CheckOTPService",
    "VALIDATION_SERVICE_CLASS": "swap_user.otp.services.ValidationService",
    # patterns
    "INVALID_LOGIN_COUNTER_PATTERN": "swap-user:invalid:login:{user_id}",
    "SENT_OTP_COUNTER_PATTERN": "swap-user:sent:otp:{user_id}",
    "USER_BANNED_FOR_INVALID_LOGIN": "swap-user:banned:invalid:login:{user_id}",
    "USER_BANNED_FOR_OTP_RATE_LIMIT_PATTERN": "swap-user:banned:rate:limit:{user_id}",
    "OTP_PATTERN": "swap-user:otp:{user_id}",
    # constant values
    "BAN_FOR_INVALID_LOGIN_TIMEOUT": 60 * 60 * 24,  # 24 hours
    "BAN_FOR_OTP_RATE_LIMIT_TIMEOUT": 60 * 60 * 2,  # 2 hours
    "OTP_TIMEOUT": 60,  # 60 seconds
    "MAX_ATTEMPTS_OF_INVALID_LOGIN": 3,
    "MAX_NUMBER_OF_OTP_SENT": 5,
    "OTP_ALPHABET": "0123456789",
    "OTP_LENGTH": 5,
}

```