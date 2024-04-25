# cse15l-lab-reports

## Lab Report 2

### Part1: ChatServer Webpage

#### Screenshot #1: 
```console
    /add-message?s=Hello&user=jpolitz
```
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-2/Screenshot%202024-04-16%20130724.png?raw=true)

##### Q1: Which methods in your code are called?

1. handle(HttpExchange exchange):
This is the entry point for handling HTTP requests in your ChatHandler class. It's triggered automatically by the HTTP server when a request comes in.

2. handleRequest(URI url):
This method processes the URI to determine the action to be taken based on the URL path and query parameters.

3. displayChat():
This method is called to concatenate and return all chat messages stored in the chat history.

##### Q2: What are the relevant arguments to those methods, and the values of any relevant fields of the class?

1. HttpExchange exchange: This argument carries all details of the HTTP request and response. It's used to extract the request URI and send back the HTTP response.
2. URI url: Derived from exchange.getRequestURI(), it contains the path and the query part of the request URL.
3. List<String> chatHistory: A field in the ChatHandler class that stores all chat messages. Initially, this list is empty.


##### Q3: How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
1. Before the Request:
<br>chatHistory is empty (i.e., chatHistory = []).
2. Processing the Request:
<br>The handleRequest method parses the URI to get the path and query.
<br>It recognizes the path /add-message and proceeds to parse the query s=Hello&user=jpolitz.
<br>The method extracts the message "Hello" and the user "jpolitz".
<br>A new chat message is constructed in the format "jpolitz: Hello" and added to chatHistory.
3. After the Request:
<br>chatHistory now contains one element: ["jpolitz: Hello"].


#### Screenshot #2: 
```console
    /add-message?s=How are you&user=yash
```
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-2/Screenshot%202024-04-16%20130743.png?raw=true)

##### Q1: Which methods in your code are called?

1. handle(HttpExchange exchange): 
Extracts the URI from the exchange object.
Calls handleRequest to process the URI based on the path and query.
Sends the HTTP response headers and body using the output from handleRequest.
2. handleRequest(URI url)
Parses the query string to extract message and user information since the path matches /add-message.
Constructs a formatted string from the user and message and adds it to chatHistory.
Calls displayChat to compile and return the full chat history for the response.
3. displayChat()
Joins all elements of chatHistory with newline characters to form the complete chat log.

##### Q2: What are the relevant arguments to those methods, and the values of any relevant fields of the class?

1. HttpExchange exchange: Carries the HTTP request and response details. It is used to obtain the request URI and to send back the compiled chat history.
2. URI url: Derived from exchange.getRequestURI(), it contains the URL path and query, which in this case is /add-message?s=How are you&user=yash.
3. List<String> chatHistory (Field in ChatHandler):
<br>Value Before the Request: ["jpolitz: Hello"]
<br>Value After the Request: ["jpolitz: Hello", "yash: How are you"]

##### Q3: How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
<br>chatHistory:
1. Before the Request: Contains the message ["jpolitz: Hello"].
2. After Processing the Request:
<br>The handleRequest method parses the new query string, extracting "How are you" as the message and "yash" as the user.
<br>Constructs the new string "yash: How are you" and adds it to the chatHistory.
3. End of Request: chatHistory now contains two items: ["jpolitz: Hello", "yash: How are you"].



#### Code for ChatServer
```java
    import java.io.IOException;
    import java.net.URI;
    import java.util.Vector;

    class Handler implements URLHandler {
        // The one bit of state on the server: a number that will be manipulated by
        // various requests.
        Vector<String> chathistory = new Vector<String>();

        public String displayChat(){
            String str="";

            for(String s:chathistory)
                str+=(s+"\n");

            return str;
        }

        public String handleRequest(URI url) {
            String path=url.getPath();
            if (path.equals("/")) {
                return displayChat();
            }else {
                if (path.contains("/add-message")) {
                    String[] actions = url.getQuery().split("&");
                    if(actions.length==2){    
                        //action 0: "s=How are you"
                        String[] words=actions[0].split("=");

                        //action 1: "user=yash"
                        String[] user=actions[1].split("=");
                        
                        chat ct=new chat(user[1], words[1]);

                        chathistory.add(ct.toString());

                        return displayChat();
                    }
                }
                return "404 Not Found!";
            }
        }
    }

    class chat{
        private String username, comment;
        public chat(String username, String comment){
            this.username=username;
            this.comment=comment;
        }

        public String toString(){
            return username+": "+comment;
        }
    }

    public class ChatServer {
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

### Part 2: Use of private key and public key into server

#### Q1: On the command line of your computer, run `ls` with the absolute path to the private key for your SSH key for logging into `ieng6`.

<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-2/Screenshot%202024-04-16%20143153.png?raw=true)

#### Q2: On the command line of the `ieng6` machine, run `ls` with the absolute path to the public key for your SSH key for logging into `ieng6` (this is the one you copied to your account on ieng6 using `ssh-copy-id`, so it should be a path on `ieng6`'s file system).

<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-2/Screenshot%202024-04-16%20143200.png?raw=true)

#### Q3: A terminal interaction where you log into your `ieng6` account without being asked for a password.
`ls` with a certain path direct to a file makes it to print out the name and its extension
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-2/Screenshot%202024-04-16%20143225.png?raw=true)

### Part 3: In 2-3 sentences, describe something you learned from lab in week 2 or 3 that you didn't know before.

I learned how to operate with the commandline, including how to utilize ls, cat, and echo. Meanwhile, I had never work with the server before, week 2 and 3's content surprised me.