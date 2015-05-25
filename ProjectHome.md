A simple library for recognizing capcha images with the antigate.com service.
Usage is very simple, just see the example below.
```
import j.antigate.*;
public class TypicalAntigate{
	 static String answer;
    public static void main (String[] args){
	try {
/** Just get an InputStream of your image in any way you want. In the example I use a local File **/
	File f = new File("C:\\capcha.png");
    	FileInputStream is = new FileInputStream(f);
    	//** You may check your antigate.com balance first **/
    	String balance = CapchaUtils.getBalance("YOURAPIKEY");
    	/** Use CapchaAnswer() method to get the capcha text, returns error message if any **/
		answer = CapchaBypass.CapchaAnswer(is, "YOURAPIKEY", null, null, null);
	} catch (IOException | InterruptedException e) {
		e.printStackTrace();
	}
    System.out.println(answer);
}
}
```
Method parameters are:

```
CapchaAnswer(InputStream, "YOURAPIKEY", "YES/NO for multiple words", "YES/NO for reg sensivity", "YES/NO for russian lang");
```
You can just write `null` for these optional parameters.
If any error aperas, the CapchaAnswer() returns the error code. Here is what it means:
```
ERROR_WRONG_USER_KEY|user authorization key is invalid (its length is not 32 bytes as it should be)
ERROR_KEY_DOES_NOT_EXIST|you have set wrong user authorization key in request
ERROR_ZERO_BALANCE|account has zero or negative balance
ERROR_NO_SLOT_AVAILABLE|no idle captcha workers are available at the moment, please try a bit later or try increasing your bid here
ERROR_ZERO_CAPTCHA_FILESIZE|the size of the captcha you are uploading or pointing to is zero
ERROR_TOO_BIG_CAPTCHA_FILESIZE|your captcha size is exceeding 100kb limit
ERROR_WRONG_FILE_EXTENSION|your captcha file has wrong extension, the only allowed extensions are gif,jpg,jpeg,png
ERROR_IMAGE_TYPE_NOT_SUPPORTED|Could not determine captcha file type, only allowed formats are JPG, GIF, PNG
ERROR_IP_NOT_ALLOWED|Request with current account key is not allowed from your IP. Please refer to IP list section located here
```