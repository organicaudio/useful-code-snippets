# python tool template

[A template for a new tool](https://gist.github.com/CrowdSalat/064b62c15315d4f65e9b44bb2ea7d972)

## create executable

You can create a standalone executable with all needed dependencies with [pipi PyInstaller](https://pypi.org/project/PyInstaller/).

## shebang

In order to be directly executable via file manager or terminal in linux add a shebang to the script: `#!/usr/bin/env python3`

## arguments

Options:

1. native `sys.argv`
2. getopt
3. optparse (Deprecated since version 3.2)
4. [**argparse**](https://docs.python.org/3/library/argparse.html) (New in version 3.2)

 [Here](https://pymotw.com/2/argparse/) is a nice overview of argparse.


```python
import argparse

parser = argparse.ArgumentParser(
    description='This script allows to serach for files in a list of archive files.')

# adds positional arguments
parser.add_argument('filenames', metavar='F', type=str, nargs='+',
                    help='filesnames of archive files.')

# adds a optinal argument (bool flag)
parser.add_argument('--verbose', '-v',
                    action='store_true', default=False,
                    dest='log_to_console',
                    help='activate verbose mode.')

# adds a optinal argument (value)
parser.add_argument('--timeout', '-t',
                    action='store',
                    dest='timeout_seconds',
                    type=int,
                    help='seconds when the script stops searching')


args = parser.parse_args()
archive_files = args.filenames
activate_logging = args.log_to_console
timeout = args.timeout_seconds
```

##  logging

```python
import logging

logging.basicConfig(format='%(asctime)s %(levelname)-8s %(message)s',
                    level=logging.INFO,
                    handlers=[
                        logging.FileHandler("file_name.log"),
                        logging.StreamHandler()
                    ]
                    )
logging.info("info log.")
```