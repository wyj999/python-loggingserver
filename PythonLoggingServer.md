# Introduction #
This project provides a Python Logging Server based on the [Twisted](http://twistedmatrix.com/trac/) framework. This creates a centralized logging server to compliment the logging modules sockethandler client.

## Purpose ##
My reason for creating this is I like the Python logging system, but wasn't crazy about every Python process on every separate server having it's own log file. Plus, I had to know which log file to look in to find a problem that might be occurring. I could have all Python processes point to one log file, but there was nothing to prevent them from trashing the log file by trying to write at the same time. In addition, processes on other servers couldn't do this unless they used some mounted/shared file system. Plus, tailing a log file, while useful, didn't have the immediacy I was looking for.

The logging server resolves these issues by providing the following:
  * It synchronizes access to the one central log file through the network interface
  * Because it is network based, multiple Python processes can send log messages to it
  * Again, because it is network based, multiple Python processes on multiple servers can send log messages to it
  * It provides a centralized status page that provides:
    1. Some statistics on the logging server itself
    1. A color coded, chronological listing of the most recent 300 log messages that is updated every 5 seconds.
    1. A separate user configurable CSS file to control the presentation of the status page

# Requirements #
The logging server requires the [Twisted](http://twistedmatrix.com/trac/) framework be installed on your system in order to run. The easiest way to do this is to use [easy\_install](http://peak.telecommunity.com/DevCenter/EasyInstall) to install the Twisted system.

# Installation #
The logging server isn't a package that is added to a running application, it is a daemon process that runs stand alone. When run it reads its configuration file and begins to listen on two network socket ports for messages. On one port it is listening for log messages that were transmitted by client programs. On the other port it is listening for HTTP requests for the status page. For this reason the project code can be anywhere on the system so long as it can be run by Twisted. The program will need access to it's configuration file. For a production installation the code should be located in some central script location.

## Status Page ##
The loggingserver.css file will need to be accessible to the web based status page, you'll see in the default code it's referenced as http://lcoalhost/loggingserver.css. This means that a web server answering to port 80 will need to have access to the file in order to serve it up. For a production system you'll want to put this on a web server at a URL you can rely on and change the loggingserverwebpage.py file to reflect this.

# Running #
The logging server is run as a daemon process by Twisted, and is invoked as follows:

`twistd --pidfile=loggingserver.pid --logfile=logginserver.log --python=loggingserver.py`

This will tell Twisted to start the logging server by running the loggingserver.py main file. It will save the PID of the process in teh loggingserver.pid file and it will log its own messages to the loggingserver.log file. These are just an example of how to run the logging server, modify as need be for your purposes.

The logging server process can be stopped by this line:

``kill `cat loggingserver.pid```

# Testing #
Once you have the logging server running as described above, you can test the system by running the client test application. This is done as follows:

`python loggingtest.py <module name>`

Where <module name> is just single string value used by the logging system to register a module name for logging. This name will show up in the logged messages. Once the test is running bring up a web server and browse to http://localhost:9021, which will take you to the status page, and should be showing messages as they are coming in from the test application. You can run as many instances of the test application as you'd like, and you'll see log messages from all of them appearing in the status window. To stop the test application hit CTRL-C, which will cause it to exit gracefully.

# References #
I wrote a more complete article about the logging server that appeared in the October issue of Python Magazine.