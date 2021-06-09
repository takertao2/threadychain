# threadychain
<h3>Private Blockchain for Discord server incubator</h3>


Setting up a node and connecting to the server's private Blockchain.


About the command-line:


For Mac you have the native command-line, if you are in windows you will want to setup WSL. Please refer to [this guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10) on how to install WSL on windows. WSL allows you to natively run Linux kernel inside of windows and have all the same features.
If you already have a WSL or command-line in MacOS, you need to install Geth, with Geth you can run ETH nodes, develop, and create your own private network. In this case we will be connecting our nodes to create our private Blockchain capable of running Dapps and Web3 applications on the web, for free.


More about how to Install Geth on your command-line [here](https://geth.ethereum.org/docs/install-and-build/installing-geth).


The benefits of running our own private network as developers are many, we can test any new features on the network and do not need to pay to deploy smart contracts. All our smart contracts and tokens will work just as any other cryptocurrency. Even being able to share coins on Metamask or other wallets that allow custom RPC. This also means we can have free cryptocurrency for development of real applications. The cons are simply that our network is small and may have bugs, be slow, and drop. But this will also give us experience to fix the issues.
It's also good if you have [Visual Code](https://code.visualstudio.com/) installed for this tutorial, or other IDE.
After installing Geth, follow along:


Create a new folder.


On Linux/wsl:

      mkdir foldername
      
      
      cd foldername
      
      
      code . 
     
If you are on windows this command (code .) will open the Visual Code editor inside the folder and enable you to perform changes if necessary, you can use this for the next step, if you want to do everything in the command-line you can use Nano.


eg. 

    nano genesis.json

Create or download the file *Genesis.json* found in this git.


run:

            geth --identity “YOUR_NODE_NAME” init /YOUR_DIRECTORY/Genesis.json --datadir /YOUR_DIRECTORY/data/YOUR_NODE_NAME
  
  
The above commands will setup the genesis block in your node.

To start your node run:

            geth --http --http.port "8085" --datadir /YOUR_DIRECTORY/data/YOUR_NODE_NAME --networkid 1337 --nodiscover

This code will run the node and start the blockchain.

Once started the Blockchain will run indefinitely until stopped. Open a new terminal and run this:

            geth attach /YOUR_DIRECTORY/data/YOUR_NODE_NAME/geth.ipc

A javascript prompt will appear where we can now perform any Blockchain tasks.
run:

            personal.newAccount()

A wallet will be generate, with a password prompt, save this wallet and remember your password. Open another terminal as you will need to do a bit more configuration.

Now you need to install Tor in your command-line so you won't expose your real IP.

on linux/WSL do:

            sudo apt-get install tor
            
You need to edit the torrc file.

depending on your configuration you will find the torrc file here:

            /etc/tor/torrc
            
If you can't find the file please refer to us.

you will need to uncomment the lines: 

            HiddenServiceDir /var/lib/tor/hidden_service/
            HiddenServicePort 80 127.0.0.1:80 
            
by removing the "#" from both lines.
A way to easily access this files is using nano

eg.

            sudo nano /etc/tor/torrc
 
Restart Tor and you should be safe. 

            service tor restart
            
Additionally setup a router/firewall on linux to make sure your IP won't leak:
Go back to your root folder with "cd". And do:

            git clone https://github.com/ruped24/toriptables2.git
            cd toriptables2
            sudo ./toriptables2.py -l
            # use ‘-f’ to deactivate
            
Now test your connection:

            curl --socks5 localhost:9050 --socks5-hostname localhost:9050 -s https://check.torproject.org/ | cat | grep -m 1 Congratulations | xargs
            
You should receive the following reply: "Congratulations. This browser is configured to use Tor".

Find the .onion link at this directory inside the file 'hostname':

                  /var/lib/tor/hidden_service
                  
This hostname will like somethine like ijiqkas001koksjd.onion, it will be used to share your node safely. 
                  

Use this command to get your enode:// address in the javascript prompt. 

             admin.nodeInfo
             
And 

             curl --socks5 127.0.0.1:9050 http://checkip.amazonaws.com/
             
will give you your Tor ip address to make sure you are connected to Tor.


Now connect your node to our private network with in the javascript prompt

            admin.addPeer("OUR NODES"):


I need to add mode details on how to connect the nodes between each other upon testing.

To mine use:

            miner.start()
            
In the javascript prompt.
And to limit your CPU usage (you will want to do this) use:

            apt-get install cpulimit
            cpulimit -e geth -l 30
            
This will limit geth to 30% cpu usage, feel free to make it however you fee like. This command will be running continually so you will need to open another terminal window if need. I might find a way to run it on background later.
            
  
To get our private nodes address list please refer to the discord server.
To run the nodes in other systems please join us in the discord for enquires. 

contact on twitter @kinuhero for more info.


  
 
