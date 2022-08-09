[Ghidra snippets](https://github.com/HackOvert/GhidraSnippets)

### Search instruction patterns like in YARA

```python
from ghidra.app.plugin.core.instructionsearch.model import MaskSettings;
from ghidra.app.plugin.core.instructionsearch import InstructionSearchApi;
from ghidra.program.util import ProgramSelection;

state = getState()
searcher = InstructionSearchApi();
# Search that masks out all operands. Used in YARA plugin
maskSettings = MaskSettings(False, False, False);
for addr in searcher.search(currentProgram, state.getCurrentSelection().getFirstRange(), maskSettings):
	print(addr)
```
