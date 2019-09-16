# How to send an E-mail via GMail SMTP Server using PHP

Using GMail SMTP Server you can send E-mails to any domain using your Gmail Credentials.

+ Google limits the number of recipients in a single Email and number of Emails can be sent per day.
+ Current limit is 500 Emails in a day or 500 recipients in a single Email.
+ On reaching threshold limits, You can not send messages for 1 to 24 hours.
+ After Suspension Period counters will get reset automatically and the user can resume sending Emails.
+ For more information on limits refer following links:
  - Link 1: [Email sending limits](https://support.google.com/a/answer/166852)
  - Link 2: [Error messages once limit is crossed](https://support.google.com/mail/answer/22839)

<br>

**++STEP-1: Google Account Security Settings++**
+ Before sending Emails using Gmail SMTP Server, Change the required setting using Google Account Security Settings or [Click Here](https://myaccount.google.com/security)
  - Make sure that **2-Step-Verification** is Disabled
  - Turn ON the **Less Secure App Access** or [Click Here](https://myaccount.google.com/u/0/lesssecureapps)

![Google Account Security Settings](https://i.imgur.com/6Hxmb2G.png))
![Less Secure App Access](https://i.imgur.com/hymkYJ6.png)

<br>

+ If **2-Step-Verification** is Enabled, then you will have to create APP Password for your application or device.
![2-Step Virification Enabled](https://i.imgur.com/vcQYoGo.png)
![Generate App Password](https://i.imgur.com/LHfCxdH.png)

<br>

+ For security precaution, Google may require you to complete this additional step while signing-in. [Click Here](https://accounts.google.com/DisplayUnlockCaptcha) to Allow access to your Google account using new Device/App.

![New Device-App](https://i.imgur.com/mEGa22F.png)

==**Note**: It may take an hour or more to reflect any security changes==

<br>

**++STEP-2: Download PHPMailer Library++**
+ [Click here](https://github.com/PHPMailer/PHPMailer/) for more details about PHP Mailer
+ [Click here](https://github.com/PHPMailer/PHPMailer/archive/master.zip) to download .zip file
+ Unzip the master.zip in your application directory and run following command from your application Directory.

```
composer require phpmailer/phpmailer
```
[Composer](https://getcomposer.org/) is the recommended way to install PHPMailer.

<br>

**++STEP-3: PHP Code++**
+ Using your Gmail Credentials, Connect to Host smtp.gmail.com
  - On port 465, if you’re using SSL
  - On port 587, if you’re using TLS
+ [Click here](https://github.com/PHPMailer/PHPMailer/wiki/Tutorial) for some more Examples and Tutorials of PHPMailer
``` php
<?php
  use PHPMailer\PHPMailer\PHPMailer;
  use PHPMailer\PHPMailer\Exception;
  require 'PHPMailer-master/src/Exception.php';
  require 'PHPMailer-master/src/PHPMailer.php';
  require 'PHPMailer-master/src/SMTP.php';

  $mail = new PHPMailer();
  $mail->IsSMTP();
  $mail->SMTPDebug  = 0;
  
  $mail->SMTPAuth   = TRUE;
  $mail->SMTPSecure = "tls";
  $mail->Host       = "smtp.gmail.com";
  $mail->Port       = 587;
  $mail->Username   = "your-email@gmail.com";
  $mail->Password   = "your-gmail-password";
  
  $mail->Mailer     = "smtp";
  $mail->Subject    = "Test is Test Email sent via Gmail SMTP Server using PHP Mailer";
  
  $mail->SetFrom("your-email@gmail.com", "set-from-name");
  $mail->AddReplyTo("reply-to-email", "reply-to-name");
  $mail->AddAddress("recipient-email", "recipient-name");
  $mail->AddCC("cc-recipient-email", "cc-recipient-name");
  $mail->IsHTML(true);
  
  $content = "<b>This is a Test Email sent via Gmail SMTP Server using PHP mailer class.</b>";
  $mail->MsgHTML($content);
  
  if(!$mail->Send()) {
    echo "Error while sending Email.";
    var_dump($mail);
  } else {
    echo "Email sent successfully";
  }
?>
```
<br>

Other similar options:
+ **G Suite SMTP Relay Service:** Send mail from your organization by authenticating with the IP addresses. You can send messages to anyone inside or outside of your domain.
+ **Restricted Gmail SMTP Server:** Send messages to Gmail or G Suite users only. This option does not require you to authenticate.
+ [Click here](https://support.google.com/a/answer/176600) to see detailed comparison of all 3 services.