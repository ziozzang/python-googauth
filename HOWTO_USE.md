Sample Generate
===============

You can use Google Auth App as OTP.

Sample Secret Key Generation Code
```
import googauth
secret_key = googauth.generate_secret_key()
print googauth.generate_code(secret_key)
```


This is the URL of OTP Scan code.

```
http://www.google.com/chart?chs=200x200&chld=M|0&cht=qr&chl=otpauth://totp/app_name@domain?secret=SECRET_KEY
```

This URL is can acuire using API

```
import googauth
secret_key = googauth.generate_secret_key()
print googauth.get_barcode_url('user', 'domain.com', secret_key)
```


Time Based Check
================

```
import googauth
secret_key = googauth.generate_secret_key()
print googauth.verify_time_based(secret_key, '123456')
```

Check Valid Time Area
=====================

```
import googauth
curr_pos = googauth.verify_time_based(secret_key,googauth.generate_code(secret_key))
value = googauth.verify_time_based(secret_key, code, window=3)
if (value is not None):
  print "OK"
```

MITM attack issue
=================

Each code should first be check against previously used codes to prevent a code from being reused by an attacker in a MITM attack.

Time Sync on Server
===================

You can syncronize your server with this crontab.

```
cat > /etc/cron.d/timesync << EOF
# For Every *:24 / KST time Sync Server
24 * * * * root rdate -s time.bora.net
EOF
```
