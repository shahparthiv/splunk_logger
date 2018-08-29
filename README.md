# splunk_logger

How to setup the logger in splunk?
After reading so many blongs I found the following snippet to setup the logger.

```
import logging
import logging.handlers

def setup_logger(level):
    logger = logging.getLogger('my_search_command')
    logger.propagate = False # Prevent the log messages from being duplicated in the python.log file
    logger.setLevel(level)
 
    file_handler = logging.handlers.RotatingFileHandler(os.environ['SPLUNK_HOME'] + '/var/log/splunk/my_search_command1.log', maxBytes=25000000, backupCount=5)
    formatter = logging.Formatter('%(asctime)s %(levelname)s %(message)s')
    file_handler.setFormatter(formatter)
    
    logger.addHandler(file_handler)
    
    return logger
    
logger = setup_logger(logging.INFO)
logger.info("Hello World !!!")
```
This is the best way to set up the logger.
Here you also setup the format of your logger. Also you can create and the setup your log file name and location of your log file. 
