# cse15l-lab-reports

## Lab Report 2

### Part1: ChatServer Webpage

#### Screenshot #1: 
```console
    /add-message?s=Hello&user=jpolitz
```
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-2/Screenshot%202024-04-16%20130724.png?raw=true)

#### Screenshot #2: 
```console
    /add-message?s=How are you&user=yash
```
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-2/Screenshot%202024-04-16%20130743.png?raw=true)

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

### Part 2

#### Q1: On the command line of your computer, run `ls` with the absolute path to the private key for your SSH key for logging into `ieng6`.

<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-1/Screenshot%202024-04-02%20102814.png?raw=true)

#### Q2: On the command line of the `ieng6` machine, run `ls` with the absolute path to the public key for your SSH key for logging into `ieng6` (this is the one you copied to your account on ieng6 using `ssh-copy-id`, so it should be a path on `ieng6`'s file system).

<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-1/Screenshot%202024-04-02%20102920.png?raw=true)

#### Q3: A terminal interaction where you log into your `ieng6` account without being asked for a password.
`ls` with a certain path direct to a file makes it to print out the name and its extension
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-1/Screenshot%202024-04-02%20103037.png?raw=true)

### Part 3: In 2-3 sentences, describe something you learned from lab in week 2 or 3 that you didn't know before.

I learned that