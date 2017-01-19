# delve_on_mac
How to get delve debugger running on Mac OSX 10.12.1+

Mac OSX 10.12.1+ introduced some caveats that may prevent the delve debugger from running. Here are the steps I used to get delve working on OSX 10.12.2 (Sierra).

All of the following commands are to be run from a terminal window as an unprivledged user. You may get prompted for sudo credentials; this is expected.

# Install Brew and Go  
1. Install brew: http://brew.sh/

$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

2. Install golang  
$ brew install go

3. Set the go environment up in ~/.bash_profile
export GOPATH=$HOME/go  
export PATH=$GOPATH/bin:$PATH

4.Then, open a new terminal window and install delve and the delve patch:  
$ brew install go-delve/delve/delve

5. Install the delve source code and patch (replace user.name with your username)  
$ mkdir -p ~/go/src/github.com/derekparker/  
$ cd ~/go/src/github.com/derekparker/  
$ git clone https://github.com/derekparker/delve.git  
$ cd delve  
$ git fetch origin pull/665/head  
$ git checkout FETCH_HEAD  
$ CERT=dlv-cert make install  

6. Open a new terminal window and clone this project, if you have not already  
$ mkdir -p ~/go/src/github.com/aaronhackney  
$ cd ~/go/src/github.com/aaronhackney  
$ git clone https://github.com/aaronhackney/delve_on_mac.git  
$ cd delve_on_mac.git  

7. Test by debugging an application  
If delve is working, you should see:  

 Type 'help' for list of commands.  
 (dlv)

#Tips and Tricks
- Some end point protection software like CrowdStrike Falcon host will see delve's attempts to control threads for debugging purposes as a threat and will prevent it from running. Before you spend too much time fighting an issue like "timeout waiting for thread", disable end point protection software and work with your end point protection software vendor to come up with a solution.

- If it delve does not work, you will see something about waiting for a thread to stop or a thread error of some kind.
