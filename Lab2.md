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


