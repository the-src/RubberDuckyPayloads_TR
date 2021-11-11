### Bu script chrome başlangıç sayfasını değiştirir.
```
GUI r
DELAY 500
STRING chrome
DELAY 400
ENTER
DELAY 600
REM ---- Chrome Başlangıç sayfasını değiştirir.
STRING chrome://settings/onStartup
ENTER
DELAY 2000
TAB
DELAY 300
TAB
DELAY 300
DOWN
DELAY 300
DOWN
DELAY 300
TAB
DELAY 300
ENTER
DELAY 300
REM ----- Bu kısmı istediğiniz adresle değiştirin.
STRING <YOUR FAKE ADDRESS>
DELAY 300
TAB
DELAY 300
TAB
DELAY 300
ENTER
ALT f4
```
