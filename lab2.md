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

Do note that this current code is inefficient as adding to a string can involve substantial copying. In this case, it might make more sense to use a StringBuilder.

Screenshot 1:

![image](https://user-images.githubusercontent.com/37094599/214975115-e1a548e9-bd7f-49f8-9704-3e5aa11f763a.png)

In this screenshot, the handleRequest method is called, with a URI that refers to the URL "localhost:1521/add-message?s=how%20are%20y0u". Then, my code verifies that the s= parameter exists and is valid. Finally, it changes the st string from "hi\nhi\nhello\n" to "hi\nhi\nhello\nhow are you\n"

Screenshot 2:

![image](https://user-images.githubusercontent.com/37094599/214975448-6f6dca4a-1c8c-449c-a4c5-c39dd6d273a3.png)

In this screenshot, the handleRequest method is called, with a URI that refers to the URL "localhost:1521/add-message?s=1234567890". Then, my code verifies that the s= parameter exists and is valid. Because URLs are really strings, we don't need to convert the number to a string. Finally, it changes the st string from "hi\nhi\nhello\nhow are you\n" to "hi\nhi\nhello\nhow are you\n1234567890\n"


## Part 2

Failure-inducing input:
```java
    @Test(timeout = 500)
    public void testAppendFail() {
        LinkedList ll = new LinkedList();
        ll.append(5);
        ll.append(6);
        ll.append(7);
        assertEquals("5 6 7 ", ll.toString());
    }
 ```
 
Non failure-inducing output:
```java
    @Test
    public void testAppendPass() {
        LinkedList ll = new LinkedList();
        ll.append(5);
        assertEquals("5 ", ll.toString());
    }
```

Symptom:

![image](https://user-images.githubusercontent.com/37094599/214989027-dfc54f42-9980-4946-a000-57f6146124db.png)

Bug:

Before:

```java
    public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
            n.next = new Node(value, null);
        }
    }
```

After:

```java
    public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        Node n = this.root;

        while(n.next != null) {
            n = n.next;
        }

        n.next = new Node(value, null);
    }
```

The fix addresses the issue because the old code effectively creates an infinite loop, because it ensures that n.next is never null. Because we know this linked list can never contain a cycle, our while loop will eventually reach the end of the linked list (n.next == null). Once we've reached the last node of the linked list, we set its next node to be the node we just added (effectively appending). This is correct behavior.

## Part 3

In lab weeks 2 and 3, I learned how to use junit outside of the context of an IDE (i.e only using javac -cp and java -cp). Prior to this, I mostly used the IDE integration with intellij to run java/junit, but was unaware of the underlying mechanism via which java included other libraries. This could be useful in the future if I ever use Java in industry. One thing I wonder about is how java handles dependencies with libraries, specifically if a junit dependency is not included while junit is.

The end.
