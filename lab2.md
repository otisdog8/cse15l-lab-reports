# Lab report 2

## Part 1
Code for my StringServer
```java
import java.net.URI;

class StringHandler implements URLHandler {
    StringBuilder sb = new StringBuilder();

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
            sb.append(s);
            sb.append('\n');
            return sb.toString();

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
Here, i chose not to use 
Screenshot 1:
![image](https://user-images.githubusercontent.com/37094599/214975115-e1a548e9-bd7f-49f8-9704-3e5aa11f763a.png)
Screenshot 2:
![image](https://user-images.githubusercontent.com/37094599/214975448-6f6dca4a-1c8c-449c-a4c5-c39dd6d273a3.png)

## Part 2

## Part 3

The end.
