# cse15l-lab-reports

## Lab Report 2

### ChatServer Webpage

#### Screenshot #1: 
```console
    /add-message?s=Hello&user=jpolitz
```
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-2/Screenshot%202024-04-16%20130724.png?raw=true)

#### Screenshot #2: 
```console
    /add-message?s=How are you&user=yash
```
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-1/Screenshot%202024-04-16%20130743.png?raw=true)

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

#### No Argument
command `ls` without argument gives me all the files and subfolders within current path
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-1/Screenshot%202024-04-02%20102814.png?raw=true)

#### Argument: Path to a Directory
Argument to a path to a directory: `ls` with a certain path gives me the files/subfolders under the given path
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-1/Screenshot%202024-04-02%20102920.png?raw=true)

#### Argument: Specific File
`ls` with a certain path direct to a file makes it to print out the name and its extension
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-1/Screenshot%202024-04-02%20103037.png?raw=true)

### Command: `cat`

#### No Argument
`cat` without argument gives an empty line, to exit this, I can click on ctrl-z to quit from it
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-1/Screenshot%202024-04-02%20103245.png?raw=true)

#### Argument: Path to a Directory
`cat` with an argument to the directory gives the warning that it is not a file but a directory
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-1/Screenshot%202024-04-02%20103348.png?raw=true)

#### Argument: Specific File
`cat` with an argument of specific file prints the content of that file
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-1/Screenshot%202024-04-02%20103424.png?raw=true)
  