# Lab Report 2
#### Part 1
```java
import java.io.IOException;
import java.net.URI;
import java.util.List;
import java.util.ArrayList;


class Handler implements URLHandler {
    List < String > wordlist = new ArrayList < String > ();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return toListS();
        } else if (url.getPath().equals("/add-message")) {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    wordlist.add(parameters[1]);
                    return toListS();
                }
            }
        }

        return "404 Not Found!";
    }

    public String toListS() {
        String result = "";
        for (int i = 0; i < wordlist.size(); i++) {
            result = result + wordlist.get(i) + "\n";
        }
        return result;
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
##### Image 1 Using `add-message`
![Image](UsingAdd1.png)

When we use anything after the /, aka giving the url a path, the Hnadler class looks at the input. It looks the given url path and compares it to "/add-message". If the url path is not the same then it will return an error message. If the url path is the same, then it will enter the next stage. The next step is to separate the equal sign from the message. Then it checks to see whether there is a "s" before the equal sign. This is basically the query check step. If it is equal to s then it will add the given word/paramater to `wordlist`. Word list is a string type arraylist, created to contain all of the given strings. Thereafter, the given paramaters are sent to a `toListS` function which basically turns them into a returnable string value. We do have to mention that there is a **handleRequest** method that takes care of all of that within the handler class. The `handleRequest` method takes it `URI` type. <br>
Although the type of `wordlist` is string, it can take int values as displayed in the next image. That is because it is an ArrayList which is dynamic. One thing that was interesting was when I used spaces in the URI. In the actual URL section on google, the spaces were replaced by "%20", however, the spaces are replaced by plus signs on the return statement of the website.  

##### Image 2 Using `add-message`
![Image](UsingAdd2.png)

I mirror the answer for the first image. This is the example where the URI includes a number. Basically what happens is that it assumes that the URI is going to be a type string and converts all of it to a string. Once you add the given URI to the ArrayList, it converts to String type. 

#### Part 2

##### Public Key
![Image](PublicKey.png)


##### Private Key
![Image](SshKey.png)



