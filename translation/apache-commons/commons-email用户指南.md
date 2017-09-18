## 一个简单的纯文本邮件
第一个例子我们通过Gmail邮箱发送一封纯文本邮件给 "John Doe"。
```
Email email = new SimpleEmail();
email.setHostName("smtp.googlemail.com");
email.setSmtpPort(465);
email.setAuthenticator(new DefaultAuthenticator("username", "password"));
email.setSSLOnConnect(true);
email.setFrom("user@gmail.com");
email.setSubject("TestMail");
email.setMsg("This is a test mail ... :-)");
email.addTo("foo@bar.com");
email.send();
```
调用setHostName方法设置SMTP服务器地址，邮件外发将会使用其发送邮件。如果不设置，系统属性"mail.host" 会无法使用。
## 发送带附件的邮件
发送带附件的邮件需要使用MultiPartEmail类。这个类除了添加了几个可以重载的attach()方法，其他和发送简单邮件的类一样。我们可以通过这个方法添加或者关联多个附件。这些附件会使用MIME编码。  
最简单的添加附件的方式是使用EmailAttachment类来关联附件。  
接下来的例子，让我们创建一封图片附件的邮件。邮件里我们将关联一张图片并发送邮件。
```
import org.apache.commons.mail.*;
...

  // Create the attachment
  EmailAttachment attachment = new EmailAttachment();
  attachment.setPath("mypictures/john.jpg");
  attachment.setDisposition(EmailAttachment.ATTACHMENT);
  attachment.setDescription("Picture of John");
  attachment.setName("John");

  // Create the email message
  MultiPartEmail email = new MultiPartEmail();
  email.setHostName("mail.myserver.com");
  email.addTo("jdoe@somewhere.org", "John Doe");
  email.setFrom("me@apache.org", "Me");
  email.setSubject("The picture");
  email.setMsg("Here is the picture you wanted");

  // add the attachment
  email.attach(attachment);

  // send the email
  email.send();
```
我们也可以引用任何有效的非本地文件URL。邮件发送的时候，文件会被自动下载并添加到邮件附件当中。
```
import org.apache.commons.mail.*;
...

  // Create the attachment
  EmailAttachment attachment = new EmailAttachment();
  attachment.setURL(new URL("http://www.apache.org/images/asf_logo_wide.gif"));
  attachment.setDisposition(EmailAttachment.ATTACHMENT);
  attachment.setDescription("Apache logo");
  attachment.setName("Apache logo");

  // Create the email message
  MultiPartEmail email = new MultiPartEmail();
  email.setHostName("mail.myserver.com");
  email.addTo("jdoe@somewhere.org", "John Doe");
  email.setFrom("me@apache.org", "Me");
  email.setSubject("The logo");
  email.setMsg("Here is Apache's logo");
  
  // add the attachment
  email.attach(attachment);

  // send the email
  email.send();
```
## 发送HTML格式的邮件
可以使用HtmlEmail类完成HTML格式邮件的发送。这个类和MultiPartEmail非常像，也是额外实现了一个方法来设置html内容，但如果邮件接收者不支持HTML邮件，也可以设置成纯文本内容，设置成html邮件的时候也可以在里面添加图片。  
接下来的例子当中，我们会发送一个添加了图片的HTML邮件。
```
import org.apache.commons.mail.HtmlEmail;
...

  // Create the email message
  HtmlEmail email = new HtmlEmail();
  email.setHostName("mail.myserver.com");
  email.addTo("jdoe@somewhere.org", "John Doe");
  email.setFrom("me@apache.org", "Me");
  email.setSubject("Test email with inline image");
  
  // embed the image and get the content id
  URL url = new URL("http://www.apache.org/images/asf_logo_wide.gif");
  String cid = email.embed(url, "Apache logo");
  
  // set the html message
  email.setHtmlMsg("<html>The apache logo - <img src=\"cid:"+cid+"\"></html>");

  // set the alternative message
  email.setTextMsg("Your email client does not support HTML messages");

  // send the email
  email.send();
```
首先，我们注意到调用embed()方法返回一个字符串类型变量，这个字符串是随机产生的唯一标识符，用在image标签中来引用图片。  
接下来例子中并没有调用setMsg()方法，这个方法在HtmlEmail中是仍然可用的，但是当关联了图片时候却不能再使用。而是应该用setHtmlMsg()和setTextMsg()方法来代替。

## 发送内嵌了图片的HTML邮件
先前的例子我们展示如何创建一个嵌入了图片的HTML邮件，但是这需要提前知道所有的图片信息，这在使用一个HTML邮件模板的时候是非常不方便的。ImageHtmlEmail就帮我们解决了这个问题，通过转换所有的外部图片成为关联图片的方式。
```
import org.apache.commons.mail.HtmlEmail;
...

  // load your HTML email template
  String htmlEmailTemplate = ".... <img src=\"http://www.apache.org/images/feather.gif\"> ....";

  // define you base URL to resolve relative resource locations
  URL url = new URL("http://www.apache.org");

  // create the email message
  ImageHtmlEmail email = new ImageHtmlEmail();
  email.setDataSourceResolver(new DataSourceUrlResolver(url));
  email.setHostName("mail.myserver.com");
  email.addTo("jdoe@somewhere.org", "John Doe");
  email.setFrom("me@apache.org", "Me");
  email.setSubject("Test email with inline image");
  
  // set the html message
  email.setHtmlMsg(htmlEmailTemplate);

  // set the alternative message
  email.setTextMsg("Your email client does not support HTML messages");

  // send the email
  email.send();
```
首先，我们创建一个HTML邮件模板来引用所有的图片。所有的引用图片会通过特殊的DataSourceResolver自动转换成关联图片。
## 调试
JavaMail API支持调试，这在出现问题的时候是非常有用的。我们可以通过邮件类的setDebug(true)来开启调试模式。调试结果将会被输出到System.out当中。  
我们想试试不同的安全设置或者commons-email的其他特性的时候，可以从EmailLiveTest和EmailConfiguration着手，这两个类被用来测试commons-email，当然，都需要是SMTP服务器。

## 授权
如果需要授权使用SMTP服务器（发送邮件），在发送邮件前我们可以调用setAuthentication(userName,password)方法。调用该方法时会创建一个DefaultAuthenticator实例，邮件发送的时候JavaMail API会调用这个实例。当然，前提是SMTP必须支持RFC2554。  

我们也可以使用更复杂的授权方法，像通过创建javax.mail.Authenticator的子类对象给一个用户显示对话框。子类在处理收集用户信息的时候需要重写getPasswordAuthentication()方法。使用创建的子类，通过Email.setAuthenticator来给Email赋值。  
## 安全
现如今，使用SMTP服务器发送邮件时候很少使用纯SMTP协议，而是使用一些更加复杂的协议。  
最常用的有两个：
* 使用25端口的STARTTLS协议
* 使用465端口的SSL协议。

下面是从维基百科上摘录下来的关于两个协议的定义：
* STARTTLS是纯文本的通信协议的扩展，它提供了一种方式升级纯文本协议，使其能直接连接到加密连接，而不是使用独立的端口来进行加密通信。
*  TLS和旧的SSL是加密协议，为网络访问提供安全的通信机制。TLS和SSL加密传输层的网络连接数据，使用非对称加密算法来进行秘钥的交换，使用对称秘钥对隐私数据和消息完整性验证信息进行加密。  
  
另外，我们也可以强制启用安全检查（默认是关闭的）：
* 在使用SSL时，我们可以通过调用设置Email.setSSLCheckServerIdentity(true)方法来强制检查服务端证书。
* 使用STARTTLS则调用Email.setStartTLSRequired(true)方法。

## 处理退回邮件
通常情况，邮件在无法发送给接收者时会退回给发送者（通过From属性指定）。然后，有些场景我们并不想原路退回，而是想发送到别的邮件地址。我们可以在发送邮件前通过简单的调用setBounceAddress(emailAddressString)来实现这种情况。  

技术说明：SMTP在发送邮件时不会根据邮件内容中的发送者判断发生错误时候邮件应该发送给谁。而是通过SMTP的"envelope sender"值来判断。JavaMail默认会根据JavaMail Session中的mail.smtp.from值来设置该值（Commons Email通过使用System.getProperties()来初始化JavaMail Session）。也就是说，如果"envelope sender"的值没有被设定，JavaMail将使用“from”中的值。在Commons Email中，如果bounceAddress被设置了，Commons Email在初始化session时候将会使用bounceAddress值来设定mail.smtp.from属性，同时覆盖其他可以被设置的值。  

注意：这是唯一一个控制处理返回邮件的方式。SMTP头的 "Errors-to:"属性已经废弃不用，在处理退回邮件时是不可信的。另外注意，除非你设置了退回地址，否则，使用一个不受信的地址当做发件地址是个不好的做法。如果应用允许用户发送邮件时设置发送地址，那么我们就应该确保设置的退回地址是一个可用的地址。

**原文地址：** https://commons.apache.org/proper/commons-email/userguide.html