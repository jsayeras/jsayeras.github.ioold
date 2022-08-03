

### GDB custom command
```python
class CustomCommand (gdb.Command):
"""Description of the command"""
    def __init__(self):
        super(CustomCommand, self).__init__("cc", gdb.COMMAND_USER)

    def invoke(self, arg, from_tty):
    """ Custom command implementation """
```
