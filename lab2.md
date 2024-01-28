# Lab Report 2

# Part 1

## ChatServer
```
import java.io.IOException;
import java.net.URI;
import java.util.*;

class SearchHandler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    ArrayList<String> strings = new ArrayList<>();

    public String handleRequest(URI url) {
        if(url.getPath().equals("/")) {
            return this.toString(strings);
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("&");
                String message = parameters[0].split("=")[1];
                String user = parameters[1].split("=")[1];
                strings.add(user + ": " + message);
                return String.format("%s and %s added!", message, user);
            } 
        }   
        return "404 Not Found!";
    }

    public String toString(ArrayList<String> strs) {
        String string = "";
        for(String str:strings) {
            string += str + "\n";
        }
        return string;
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new SearchHandler());
    }
}
```

## Using /add-message?s=Hello&user=jpolitz
![](/Screenshots/first_command.png)
- Me/thods Called: handleRequest(URI url), toString(ArrayList<String> strs)
- Relevant Arguments: URI url - the url that is entered and to be processed
- Relevant Fields: ArrayList<String> strings - String ArrayList that stores all inputs into the url
- Changed Values in Fields: jpolitz: Hello was added to ArrayList<String> strings

## Using /add-message?s=How are you&user=yash
![](/Screenshots/second_command.png)
- Methods Called: handleRequest(URI url), toString(ArrayList<String> strs)
- Relevant Arguments: URI url - the url that is entered and to be processed
- Relevant Fields: ArrayList<String> strings - String ArrayList that stores all inputs into the url
- Changed Values in Fields: yash: How are you was added to ArrayList<String> strings

# Part 2

## The absolute path to the private key for your SSH key for logging into ieng6 (on your computer, an EdStem workspace, or on the home directory of the lab computer)
![](/Screenshots/private_key.png)
## The absolute path to the public key for your SSH key for logging into ieng6 (this is the one you copied to your account on ieng6, so it should be a path on ieng6's file system)
![](/Screenshots/public_key.png)
## A terminal interaction where you log into your ieng6 account without being asked for a password.
![](/Screenshots/login_wo_pw.png)

# Part 3

I learnt that I can create a simple web server just by processing urls through code. 



