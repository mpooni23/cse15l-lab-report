# Lab Report 2 - Servers and SSH Keys (Week 3)

# PART 1

# **1. Code for ChatServer.java**
```
import java.io.IOException;
import java.net.URI;

class Handler2 implements URLHandler {
    String s = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(s);
        } else if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("&");
            String[] message = parameters[0].split("=");
            String[] user = parameters[1].split("=");
            if (message[0].equals("s") && user[0].equals("user")) {
                s += " " + user[1] + " : " + message[1] + "\n";
                return String.format(s);
            }
        }
        return "404 Not Found!";
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler2());
    }
}
```
Which methods in your code are called?
What are the relevant arguments to those methods, and the values of any relevant fields of the class?
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
By values, we mean specific Strings, ints, URIs, and so on. "abc" is a value, 456 is a value, new URI("http://...") is a value, and so on.)

# **2. Two screen shots of /add-message**

![Image](Lab 2 Screenshot 1.png)

**1. Which methods in your code are called?**
    The server is listening for incoming messages at the specified port (4000). When we click http://localhost:4000/add-message?s=Hello&user=jpolitz in the browser, on receiving this message the webserver calls the handlerequest() method of the Handler2 class passing in the provided URI /add-message?s=Hello&user=jpolitz. This method checks if the URL path contains "/add-message". If such is the case, it then extracts the given querystring and parses the querystring to extract the message and the username. For the message it checks to see if the key is equal to "s" and for the username it checks to see the key is "user" and then it adds to the string s which is a declared as a property at the instance level, the string produced by concatenating the ```<username>:<message>```. It then returns the String s as the return value (responds with the entire string so far).


```
   1. handleRequest(URI url)
   2. url.getPath() 
   3. url.getQuery()
   4. String[] parameters = url.getQuery.split("&")
   5. String[] message = parameters[0].split("=");
   6. String[] user = parameters[1].split("=");
   7. s += " " + user[1] + " : " + message[1] + "\n";   
   8. String.Format(s)
```

**2. What are the relevant arguments to those methods, and the values of any relevant fields of the class?**
   
The handlerequest method is provided the URI string as a parameter url /add-message?s=Hello&user=jpolitz. We extract the path from the passed in parameter url by calling the helper method getPath() method on the url -> url.gethPath(). The getPath() method does not take any parameters. If the path contains "/add-messages" we then call the getQuery() helper method on the url to get the query string. The method getQuery() does not take any parameter. We call the split method on the query string based on regex "&". split takes the regex "&" as parameter and splits the string into two parts. The first part is for the message and the second part is for the username. For the message it checks to see if the key is equal to "s" and for the username it checks to see the key is "user" and then it adds to the string s which is a declared as a property at the instance level, the string produced by concatenating the <username>: <message>. It then returns the String s as the return value (responds with the entire string so far).

```
url <- /add-message?s=Hello&user=jpolitz
url.getpath() <- /add-message
url.getQuery() <- s=Hello&user=jpolitz
String[] parameters = url.getQuery.split("&") (parameters[0] = "s=Hello", parameters[1] = "user=jpolitz")
String[] message = parameters[0].split("="); (message[0] = "s", message[1] = "Hello")
String[] user = parameters[1].split("="); (user[0] = "user", user[1] = "jpolitz")
s += " " + user[1] + " : " + message[1] + "\n";  ("jpolitz" : "Hello")
String.Format(s)
```

**3. How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.**

For each specific request, if it is a add-message request the passed in string is appended to the String s. 
String s is the return value  which responds with the entire string so far.

When the path is just "\", the contents of the String s is returned, none of the values get affected.

![Image](Lab 2 Screenshot 2.png)

**1. Which methods in your code are called?**
   
When we click http://localhost:4000/add-message?s=How are you&user=yash in the browser,on receiving this message the webserver calls the handlerequest() method of the Handler2 class passing in the provided URI /add-message?s=Hello&user=jpolitz. This method checks if the URL path contains "/add-message". If such is the case, it then extracts the given querystring and parses the querystring to extract the message and the username. For the message it checks to see if the key is equal to "s" and for the username it checks to see the key is "user" and then it adds to the string s which is a declared as a property at the instance level, the string produced by concatenating the <username>: <message>. It then returns the String s as the return value (responds with the entire string so far).

```
   1. handleRequest(URI url)
   2. url.getPath() 
   3. url.getQuery()
   4. String[] parameters = url.getQuery.split("&")
   5. String[] message = parameters[0].split("=");
   6. String[] user = parameters[1].split("=");
   7. s += " " + user[1] + " : " + message[1] + "\n";   
   8. String.Format(s)
```

**2. What are the relevant arguments to those methods, and the values of any relevant fields of the class?**

The handlerequest method is provided the URI string as a parameter url /add-message?s=How are you&user=yash. We extract the path from the passed in parameter url by calling the helper method getPath() method on the url -> url.gethPath(). The getPath() method does not take any parameters. If the path contains "/add-messages" we then call the getQuery() helper method on the url to get the query string. The method getQuery() does not take any parameter. We call the split method on the query string based on regex "&". split takes the regex "&" as parameter and splits the string into two parts. The first part is for the message and the second part is for the username. For the message it checks to see if the key is equal to "s" and for the username it checks to see the key is "user" and then it adds to the string s which is a declared as a property at the instance level, the string produced by concatenating the <username>: <message>. It then returns the String s as the return value (responds with the entire string so far).

```
url <- /add-message?s=How are you&user=yash
url.getpath() <- /add-message
url.getQuery() <- s=How are you&user=yash
String[] parameters = url.getQuery.split("&") (parameters[0] = "s=How are you", parameters[1] = "user=yash")
String[] message = parameters[0].split("="); (message[0] = "s", message[1] = "How are you")
String[] user = parameters[1].split("="); (user[0] = "user", user[1] = "yash")
s += " " + user[1] + " : " + message[1] + "\n";  ("yash" : "How are you")
String.Format(s)
```

**3. How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.**

For each specific request, if it is a add-message request the passed in String s declared as a property at the class instance level. The index also gets incremented to pointed to next string to be appended. 

Initially String s = "jpolitz" : Hello\n". Then the string s = "jpolitz" : Hello\nyash : How are you\n" on the second invocation.

When the path is just "\", the contents of the String s is returned, none of the values get affected.



