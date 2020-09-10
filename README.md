# Foundation Mail

The Mail Service  use MailChimp to send a template mail to target contact list

Repo management: $GOPATH//src/wwwin-github.cisco.com/DevNet/Foundation_Mail

### Build the go application
```
export GOPATH=$(cd ../../../..; pwd)
GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go install wwwin-github.cisco.com/DevNet/Foundation_Mail/cmd/mail

mkdir -p bin
cp -fv ../../../../bin/mail bin/mail
```

### Run the mail service locally

[1] CD to cmd/mail folder
```
go build
```

[2] Get MailChimp API key and server address
* Login in [Campaign](https://login.mailchimp.com/) with your MailChimp account.(Here is a account "CiscoDevNet" is ready for couldification team, ask tingxxu@cisco.com for the password)
* [Get your app key](http://kb.mailchimp.com/integrations/api-integrations/about-api-keys)
* Get you MailChimp address. The api address format is: {region}.api.mailchimp.com.
Noticed you app key: ***************-us16, you can use "us16" instead of the region placeholder.
So you MailChimp server address should be: us16.api.mailchimp.com

[3] Start mail Service Server on local
```
MAILCHIMP_ADDR=us16.api.mailchimp.com MAILCHIMP_APIKEY=61596b2c056da0150642e6894e6e23db-us16 \
SMTP_HOST=smtp.gmail.com SMTP_PORT=465 Mail_Password=cisco123 \
REPLYTO_NAME=devnet REPLYTO_MAIL=creationdevnet@gmail.com ./mail serve
```

### Quick Start
#### Send mail to a MailChimp list
* Login in [Campaign](https://login.mailchimp.com/) with you account.(CiscoDevNet is ready for couldification team, ask tingxxu@cisco.com for the password)
* Create a contact list on MailChimp web interface
* Please refer to "MailChimp Template sample" section to  see how to create MailChimp mail template
* Call mail service api [POST]http://localhost:9976/v1/mail with body:
```
{
   "subject":"Go introduction",
   "contact_book_name":"tingxin",                                   #this should be the contact list in your MailChimp
   "template":"devnet_1l",                                          #this should be the tempate name you created in your MailChimp
   "content":{                                                      #this should be  a arbitrary object map to template you selected
      		"name":"tingxin",
      		"project_name":"Cloudification"
      }

}
```

#### Send mail directly
* Call mail service api [POST]http://localhost:9976/v1/mail with body:

```
{
   "subject":"Tingxin's regards",
	"email_address":{
		"to":[
			"tingxxu@cisco.com"
			],
		"cc":[
			"friendship-119@163.com"
			]
	},
   "template":"http://localhost:63344/tests/test.html",             #this should be the template url, if this filed is none or empty, will use default template
   ## "template_token":"template access token",                     #if access template need authorization
   "content":{                                                      #this should be  a arbitrary object map to template you selected
   		"name":"tingxin",
   		"project_name":"Cloudification"
   }
}
```


### Default Template
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office">
<head>
    <!-- This is a simple example template that you can edit to create your own custom templates -->
    <!--[if gte mso 15]>
    <xml>
        <o:OfficeDocumentSettings>
            <o:AllowPNG />
            <o:PixelsPerInch>96</o:PixelsPerInch>
        </o:OfficeDocumentSettings>
    </xml>
    <![endif]-->
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Innovation with DevNet Creations</title>

</head>
<body>
<center>
    <table border="1" cellpadding="0" style="border-spacing:0;border:1pt solid #58A9C6;">
        <tbody>
        <tr>
            <td style="padding:0;border-style:none;">
                <div style="margin:0;"><font face="Times New Roman" size="3"><span style="font-size:12pt;"><a href="https://developer.cisco.com/site/devnetcreations/" target="_blank"><font face="HelveticaNeue-Light"><img src="https://developer.cisco.com/images/dnlabs/email/Devnet_Labs_Email_Header.jpg" width="1033" height="280" border="0"></font></a></span></font></div>
            </td>
        </tr>
        <tr>
            <td style="padding:0.75pt;border-style:none;">
                <table border="0" cellpadding="0">
                    <tbody>
                    <tr>
                        <td width="1017" style="width:610.5pt;padding:30pt;">
                            <div style="margin-right:0;margin-left:0;"><font face="Times New Roman" size="3"><span style="font-size:12pt;"><font face="HelveticaNeue-Light">Hi {{.name}},</font></span></font></div>
                            <div style="margin:14pt 0;"><font face="Times New Roman" size="3"><span style="font-size:12pt;"><font face="HelveticaNeue-Light">Your project named "</font><a href="http://developer.cisco.com/dpCatalogForm/renderFormForUpdate/171051" target="_blank"><font face="HelveticaNeue-Light"><font color="black"><b>{{.project_name}}</b></font></font></a><font face="HelveticaNeue-Light">" has been archived on DevNet Creations!</font></span></font>
                            </div>
                            <div style="margin:14pt 0;"><font face="Times New Roman" size="3"><span style="font-size:12pt;"><font face="HelveticaNeue-Light">We look forward to seeing your next innovation on DevNet Creations!</font></span></font></div>
                            <div style="margin:14pt 0;"><font face="Times New Roman" size="3"><span style="font-size:12pt;"><font face="HelveticaNeue-Light">If you are not a DevNet Creations member, </font><a href="https://tools.cisco.com/IDREG/guestRegistration.do?exit_url=https%3A%2F%2Fdeveloper.cisco.com%2Fsite%2Fdevnet%2Fhome%2Findex.gsp&amp;locale=en_US" target="_blank"><font face="HelveticaNeue-Light"><font color="#46B7D6"><b>sign
                                    up</b></font></font></a><font face="HelveticaNeue-Light"> to view more projects! For any questions, contact us at </font><a href="mailto:devnetlabs@external.cisco.com" target="_blank"><font face="HelveticaNeue-Light"><font color="#46B7D6"><b>devnetlabs@external.cisco.com</b></font></font></a><font face="HelveticaNeue-Light">.</font></span></font>
                            </div>
                            <div style="margin:14pt 0;"><font face="Times New Roman" size="3"><span style="font-size:12pt;"><font face="HelveticaNeue-Light">Cheers, </font><font face="HelveticaNeue-Light"><br>
                                    DevNet Creations Team </font><font face="HelveticaNeue-Light"><br>
                                    </font><a href="https://developer.cisco.com/site/devnetcreaions/" target="_blank"><font face="HelveticaNeue-Light">https://developer.cisco.com/site/devnetcreations/</font></a><font face="HelveticaNeue-Light"> </font></span></font>
                            </div>
                        </td>
                    </tr>
                    </tbody>
                </table>
            </td>
        </tr>
        </tbody>
    </table>
</center>
</body>
</html>
```

### MailChimp Template sample

Here is a MailChimp template sample, please follow those steps to create your own template

- login in MailChimp and click the template tab
- select the "code you own"
- copy follow code to the template editor
- you can use "content manager" to store you resource
- you can update/add new resource just like edit a html
- keep mind keep the container with tag "mc:edit="keyword", that will be changed with your content body when you call api
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office">
  <head>
    <!-- This is a simple example template that you can edit to create your own custom templates -->
    <!--[if gte mso 15]>
    <xml>
      <o:OfficeDocumentSettings>
        <o:AllowPNG />
        <o:PixelsPerInch>96</o:PixelsPerInch>
      </o:OfficeDocumentSettings>
    </xml>
    <![endif]-->
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>*|MC:SUBJECT|*</title>
  </head>
  <body>
    <center>
      <table border="1" cellpadding="0" style="border-spacing:0;border:1pt solid #58A9C6;">
        <tbody>
          <tr>
            <td style="padding:0;border-style:none;">
              <div style="margin:0;">
                <font face="Times New Roman" size="3"><span style="font-size:12pt;"><a href="https://developer.cisco.com/site/devnetcreations/" target="_blank">
                  <font face="HelveticaNeue-Light"><img src="https://developer.cisco.com/images/dnlabs/email/Devnet_Labs_Email_Header.jpg" width="1033" height="280" border="0" alt="Devnet_Labs_Email_Header.jpg">
                    </font></a></span>
                  </font>
                </div>
              </td>
            </tr>
            <tr>
              <td style="padding:.75pt;border-style:none;">
                <table border="0" cellpadding="0">
                  <tbody>
                    <tr>
                      <td width="1017" style="width:610.5pt;padding:30pt;">
                        <div style="margin-right:0;margin-left:0;">
                          <div style="display:inline;">Hi</div>
                          <div mc:edit="name" style="display:inline;">tingxin</div>
                        </div>
                        <div style="margin:14pt 0;">
                          Your project named "<a href="http://developer.cisco.com/dpCatalogForm/renderFormForUpdate/171051" target="_blank" mc:edit="project_name">project name
                        </a>
                        "has been archived on DevNet Creations!
                      </div>
                      <div style="margin:14pt 0;">
                        <font face="Times New Roman" size="3"><span style="font-size:12pt;">
                          <font face="HelveticaNeue-Light">We look forward to seeing your next innovation on DevNet Creations!</font></span>
                        </font>
                      </div>
                      <div style="margin:14pt 0;">
                        <font face="Times New Roman" size="3"><span style="font-size:12pt;">
                          <font face="HelveticaNeue-Light">If you are not a DevNet Creations member, </font><a href="https://tools.cisco.com/IDREG/guestRegistration.do?exit_url=https%3A%2F%2Fdeveloper.cisco.com%2Fsite%2Fdevnet%2Fhome%2Findex.gsp&amp;locale=en_US" target="_blank">
                            <font face="HelveticaNeue-Light">
                              <font color="#46B7D6"><b>sign
                                up</b>
                              </font>
                              </font></a>
                              <font face="HelveticaNeue-Light"> to view more projects! For any questions, contact us at </font><a href="mailto:devnetlabs@external.cisco.com" target="_blank">
                                <font face="HelveticaNeue-Light">
                                  <font color="#46B7D6"><b>devnetlabs@external.cisco.com</b>
                                </font>
                                </font></a>
                                <font face="HelveticaNeue-Light">.</font></span>
                              </font>
                            </div>
                            <div style="margin:14pt 0;">
                              <font face="Times New Roman" size="3"><span style="font-size:12pt;">
                                <font face="HelveticaNeue-Light">Cheers, </font>
                                <font face="HelveticaNeue-Light">
                                  <br>
                                  DevNet Creations Team </font>
                                  <font face="HelveticaNeue-Light">
                                    <br>
                                  </font><a href="https://developer.cisco.com/site/devnetcreaions/" target="_blank">
                                  <font face="HelveticaNeue-Light">https://developer.cisco.com/site/devnetcreations/</font></a>
                                  <font face="HelveticaNeue-Light"> </font></span>
                                </font>
                              </div>
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    </td>
                  </tr>
                </tbody>
              </table>
            </center>
          </body>
</html>
```

### Swagger API Doc
  - Step 1. Open Browser and go to "http://127.0.0.1:9976/apidocs/".
  - Step 2. Put "http://127.0.0.1:9976/apidocs.json" in the text box and explore.