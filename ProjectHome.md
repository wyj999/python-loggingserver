# Python logging Server #
This projects provides a Python Logging Server based on the [Twisted](http://twistedmatrix.com/trac/) framework. It provides the server side compliment to the Python logging.handlers.SocketHandler client module. The logging server itself is a centralized service to which any and all Python code/processes/servers can log messages to. This means that multiple processes can log messages to the same log file without conflict. This concept extends across servers that are running Python processes so long as there is a network connection between those servers. The server also provides a web based status page that shows some statistics and a color coded, chronological listing of the last 300 log messages. The look and feel of this web page is user configurable through a Cascading Style Sheet.
# Provides #
  * Centralized logging for Python log messages
  * Centralized logging for multiple Python processes
  * Centralized logging for multiple Python processes across multiple servers
  * A web based status page:
    1. Statistics about the logging server itself
    1. A color coded, chronological listing of the last 300 log messages

# Wiki #
http://code.google.com/p/python-loggingserver/wiki/PythonLoggingServer