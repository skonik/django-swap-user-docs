Example of settings is shown below.

In your django `settings.py` file put variable called `SWAP_USER` and configure the package as you wish.
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
## 🦺 Services
Services are classes used to implement some logic.
For example, one time password generation logic.

### `OTP_SENDER_CLASS`
`type: str`

Dotted path to to an implementation of one time password sender class.
You can implement your own OTP sender class to send passwords by email/sms/push and put the path here.


### `GET_OTP_SERVICE_CLASS`
`type: str`

Dotted path to to an implementation of a class to get/generate one time password.

This  class manages generation and storing code in redis. Uses `OTP_SENDER_CLASS` implementation to send  OTP.

### `CHECK_OTP_SERVICE_CLASS`
`type: str`

Dotted path to to an implementation of one time password checker class.

Checks how much wrong login attempts a user did and authenticates the user.


### `VALIDATION_SERVICE_CLASS`
`type: str`

Dotted path to to an implementation of one time password validation class.

Checks if user is banned/password is wrong.

## 🏁 Patterns
Patterns are used as keys/values templates for storing information inside redis.

Use `{user_id}` as user id template tag.

### `INVALID_LOGIN_COUNTER_PATTERN`
`type: str`

Pattern for storing invalid logins count in redis.

Settings value example: `swap-user:invalid:login:{user_id}`

How is stored in redis: `swap-user:invalid:login:3:5` (a user with id 3 has failed to login 5 times)


### `SENT_OTP_COUNTER_PATTERN`
`type: str`

Pattern for storing sent otp count.

Settings value example: `swap-user:sent:otp:{user_id}`

How is stored in redis: `swap-user:sent:otp:3:5` (5 one time passwords have been sent to a user with id 3)


### `USER_BANNED_FOR_INVALID_LOGIN`
`type: str`

Cache key for tracking if a user is banned for reaching maximum count of invalid logins(wrong OTP entered).

Settings value example: `swap-user:banned:invalid:login:{user_id}`

How is stored in redis: `swap-user:banned:invalid:login:3:true` (a user with id 3 is banned for invalid logins - true)

### `USER_BANNED_FOR_OTP_RATE_LIMIT_PATTERN`
`type: str`

Cache key for tracking if a user is banned for reaching maximum count of OTP sent.

Settings value example: `swap-user:banned:rate:limit:{user_id}`

How is stored in redis: `swap-user:banned:rate:limit:3:true` (a user with id 3 is banned for too many OTP sent - true)


### `OTP_PATTERN`
`type`: str

Settings value example: `swap-user:otp:{user_id}`

How is stored in redis: `swap-user:otp:3:1234ABC`(for a user with id 3 OTP is `1234ABC`)

## ⏱️ Constant values
Values that adjust bans, timeouts and alphabet.

### `BAN_FOR_INVALID_LOGIN_TIMEOUT`
`type: int`

TTL in seconds for time within we track invalid login attempts.


### `BAN_FOR_OTP_RATE_LIMIT_TIMEOUT`
`type: int`

TTL in seconds for time within we track count of otp sent.

### `OTP_TIMEOUT`
`type: int`

TTL in seconds for time we store one time passwords until they expire.

### `MAX_ATTEMPTS_OF_INVALID_LOGIN`
`type: int`

Maximum number of invalid login attempts before banning a user.

### `MAX_NUMBER_OF_OTP_SENT`
`type: int`

Maximum number of OTP sent before banning a user.


### `OTP_ALPHABET`
`type: str`

Characters included to generate a one time password.

### `OTP_LENGTH`
`type: int`

Length of a one time password to generate.








