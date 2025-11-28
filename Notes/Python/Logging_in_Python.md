# Logging in Python

- Logging is a crucial aspect of any application, providing a way to track events, errors and operational info.
- Python's built-in logging module offers a flexible framework for emitting log messages from python programs.

```py
import logging

## Configure basic logging settings :
logging.basicConfig(level=logging.DEBUG)

# Log messages 
logging.debug("This is a debug Message")
logging.info("This is a info Message")
logging.warning("This is a warning Message")
logging.error("This is a error Message")
logging.critical("This is a critical Message")
```

## Log Levels :
Python's logging module has several log levels indicating the severity of events. The default levels are :

- `DEBUG` : Detailed info, typically of interest only when diagnosing problems
- `INFO` : Confirmation that things are working as expected.
- `WARNING` : An indication that something unexpected happened or indicative of some problem in the near future (eg. 'Disk space low'). The software is still working as expected.
- `ERROR` : Due to more serious problem, the software has not been able to perform  some function.  
- `CRITICAL` : A very serious error, indicating the program itself may be unable to continue running

### Configure logging :

```py
logging.basicConfig(
    filename='app.log',
    filemode='w',
    level=logging.DEBUG,
    format='%(asctime)s-%(name)s-%(levelname)s-%(message)s',
    datefmt='%Y-%m-%d %H:%M:%S'
)
```

## Multiple loggers in python :
- You can create multiple loggers for different parts of your application.

```py
import logging

# create logger for module1
logger1 = logging.getLogger("module1")
logger1.setLevel(logging.DEBUG)

# create a logger for module2
logger2 = logging.getLogger("module2")
logger2.setLevel(logging.WARNING)

# Configure logging settings
logging.basicConfig(
    level = logging.DEBUG,
    format = '%(asctime)s = %(name)s - %(levelname)s - %(message)s',
    datefmt = '%Y-%m-%d %H:%M:%S'
)

# log message with different loggers 

logger1.debug("This is a debug message")
logger2.warning("This is a warning message")
logger2.error("This is an error message")
```

## Use Case for implementing Logging :

```py
import logging

logging.basicConfig(
    level = logging.DEBUG,
    format = '%(asctime)s = %(name)s - %(levelname)s - %(message)s',
    datefmt = '%Y-%m-%d %H:%M:%S',
    handlers = [
        logging.FileHandler("app.log"),
        logging.StreamHandler()
    ]
)

logger = logging.getLogger("ArithmeticApp") # Name of the logger is "ArithmeticApp"

def add(a, b) :
    result = a + b
    logger.debug(f"adding {a} + {b} = {result}")
    return result

def multiply(a, b) :
    result = a * b
    logger.debug(f"multiplying {a} * {b} = {result}")
    return result

def subtract(a, b) :
    result = a - b
    logger.debug(f"subtracting {a} - {b} = {result}")
    return result

def divide(a, b) :
    try :
        result = a / b
        logger.debug(f"dividing {a} + {b} = {result}")
        return result
    except ZeroDivisionError :
        logger.error("Division by zero error")
        return result
```