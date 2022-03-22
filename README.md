Step 1
----------
個人gmail帳號就可以發信測試，設定gmail允許呼叫
![mailconfig](https://user-images.githubusercontent.com/24542187/159418113-3c9a8c86-3c32-45ef-8b8d-f58466997509.jpg)


Step 2
----------
安裝套件
```
composer require phpmailer/phpmailer
```


Step 3
----------
```
<?php
//Import PHPMailer classes into the global namespace
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\Exception;
 
require_once 'vendor/autoload.php';
 
$mail = new PHPMailer(true);
try{
    $mail->isSMTP();
    $mail->Host = 'smtp.googlemail.com';  //gmail SMTP server
    $mail->SMTPAuth = true;
    $mail->Username = 'GMAIL_USERNAME';   // gmail account
    $mail->Password = 'GMAIL_PASSWORD';   // gmail password
    $mail->SMTPSecure = 'ssl';
    $mail->Port = 465;                    //SMTP port

    $mail->setFrom('FROM_EMAIL_ADDRESS', 'FROM_NAME');
    $mail->addAddress('RECEPIENT_EMAIL_ADDRESS', 'RECEPIENT_NAME');
    
    $mail->isHTML(true);
    
    $mail->Subject = 'Email subject';
    $mail->Body    = '<b>Hello World</b>';
    
    $mail->send();
}catch(Exception $e){
    echo $e->errorMessage();
}

echo 'Message has been sent';

```

* 注意 gmail server SSL是465 port，TLS是 587 port。一般SMPT server default port是25

參考: https://artisansweb.net/send-email-using-gmail-smtp-server-php-script/
