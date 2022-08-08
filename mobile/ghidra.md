
https://github.com/HackOvert/GhidraSnippets
```python
from ghidra.app.plugin.core.instructionsearch.model import MaskSettings;
from ghidra.app.plugin.core.instructionsearch import InstructionSearchApi;
from ghidra.program.util import ProgramSelection;
print("Start...")

state = getState()

searcher = InstructionSearchApi();
# Search that masks out all operands.
maskSettings = MaskSettings(False, False, False);
for addr in searcher.search(currentProgram, state.getCurrentSelection().getFirstRange(), maskSettings):
	print(addr)
print("End...")
```
