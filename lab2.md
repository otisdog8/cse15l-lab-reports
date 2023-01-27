# Lab report 2

## Part 1
Code for my StringServer
```java
import java.io.IOException;
import java.net.URI;

class StringHandler implements URLHandler {
    String st = "";

    public String handleRequest(URI url) {
        if (url == null) {
            return "Error";
        }
        String quString = url.getQuery();
        if (quString == null) {
            return "Error";
        }
        String[] quArr = quString.split("=");

        String s = null;

        for (int i = 0; i < quArr.length-1; i += 2) {
            if (quArr[i].equals("s")) {
                s = quArr[i+1];
            }
        }

        if (s == null) {
            return "Invalid querystring";
        }
        if (url.getPath().endsWith("/add-message")) {
            st = st + s + "\n";
            return st;

        }
        else {
            return "404";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new StringHandler());
    }
}
```


Screenshot 1:

![image](https://user-images.githubusercontent.com/37094599/214975115-e1a548e9-bd7f-49f8-9704-3e5aa11f763a.png)

In this screenshot, the handleRequest method is called, with a URI that refers to the URL "localhost:1521/add-message?s=how%20are%20y0u". Then, my code verifies that the s= parameter exists and is valid. Finally, it changes the st string from "hi\nhi\nhello\n" to "hi\nhi\nhello\nhow are you\n"

Screenshot 2:

![image](https://user-images.githubusercontent.com/37094599/214975448-6f6dca4a-1c8c-449c-a4c5-c39dd6d273a3.png)

In this screenshot, the handleRequest method is called, with a URI that refers to the URL "localhost:1521/add-message?s=1234567890". Then, my code verifies that the s= parameter exists and is valid. Because URLs are really strings, we don't need to convert the number to a string. Finally, it changes the st string from "hi\nhi\nhello\nhow are you\n" to "hi\nhi\nhello\nhow are you\n1234567890\n"


## Part 2

## Part 3

The end.
