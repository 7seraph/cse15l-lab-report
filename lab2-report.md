# Lab 2 - Servers and SSH Keys
---
## Part 1: Creating a web server
`ChatServer` Implementation: The code will separate the url into `user` and `message` separated by a `:`. You can change the `user` and message. As you reload the page, the server will update the chat. Note that all previous messages and user will still be on the server (as long as the server is still running).
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    //int num = 0;
    ArrayList<String> strMessage = new ArrayList<String>();
    public String handleRequest(URI url) {
        String user;
        String message;
        if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("&");
            String[] userParameter = parameters[1].split("=");
            String[] messageParameter = parameters[0].split("=");

            if (userParameter.length > 1) {
                user = userParameter[1];
            }
            else {
                user = " ";
            }

            if (messageParameter.length > 1) {
                message = messageParameter[1];
            }
            else {
                message = " ";
            }

            if (!user.isEmpty() && !message.isEmpty()) {
                String newMessage = user + ": " + message;
                strMessage.add(newMessage);
                return String.join("\n", strMessage);
            }
        }

            
           
        
        return "This is the beginning of your chat!";
    }
}


class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
- The `String` arrays are used to as parameters to identify where in the url we want `user`and `message` to be. In this case, we are following the format: `/add-message?s=<string>&user=<string>`. We also need to create a `String` such that the message we see on the server follows the format: `user: message`. Note: we also want to add `\n` such that the next message will be printed on a new line.
- If there are more users, then it will be concatenated (ie. `user1+user2`). The same goes for the message too!
> If there is no input, then server will return a nice message (`This is the beginning of your chat!`). As of now, any path that is not in the format: `/add-message?s=<string>&user=<string>` will return the `This is the beginning of your chat!` message. You can also view the chat history as long as the server is still running and you send a message using the path `/add-message?s=<string>&user=<string>`.
---
### Examples
![img]()
