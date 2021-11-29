# Logic Vulnerability Fuzzing
**Always look at the source - Easy to miss input fields**
- Very large (1000+) string input 
	- Metasploit's pattern_create and pattern_offset is useful
- Negative input
- Strange input (String where number is, etc)
## Workflow Validation
**Test normal flow as template first**
- Skip steps
- Repeat steps again
- Prematurely reset workflow
- Miss input
