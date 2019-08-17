# Pushdown Automata
👨🏽‍💻👏 Assignments for 'Formal Languages, Automata and Computability' subject about a simulation of pushdown automata.

## More Information
This project is developed using the programming language Python3, however, the speaking language was Portuguese.

### Introduction
The program was developed by [Vitor Camargo](https://github.com/vitorCamargo), [Thaís Zorawski](https://github.com/TZorawski), [Cláudia Sampedro](https://github.com/claudiaps) and [Lucas Ribeiro](https://github.com/lucasvribeiro), students of the Bachelor of Computer Science course at the Federal Technological University of Paraná - *campus* Campo Mourão (UTFPR-CM). This program was developed in the semester 2018/2, for the discipline Formal Languages, Automata and Computability, taught by Professor [Marco Aurélio Graciotto Silva](https://github.com/magsilva), from the Computing Department of UTFPR-CM (DACOM).

### About Pushdown Automata
A *Pushdown Automata* is a theoretical model similar to the functioning of Turing machines. A PA is a machine that manipulates symbols on a tape according to a set of rules and transitions. Like a Turing machine, a Pushdown Automata has an alphabet, which will be the automaton's acceptable set of symbols, a set of possible states, an input word, a stack, and a set of transitions that indicate what will happen to the automaton. automaton and with the stack according to the value that is read on the automaton input.

### How the Program Works
This program follows the same logic as the Turing Machine previously developed by the same students, which is available [at this link](https://github.com/vitorCamargo/turing-machine). Before starting to take the logic approach of the automaton, it is checked whether the entered word contains any invalid characters (outside the input alphabet) and whether the character representing ε is valid (not being used in the input alphabet or the alphabet). of work). After these checks, the initial symbol is added to the stack and the current automaton configuration is created, containing its current state, input word, and stack. This initial configuration is then added to the execution stack and looks in a list of transitions for the paths that can be taken. For each possibility, therefore, is added the result of this possible transition in the queue (searching linearly, and *not* for depth). For a transition to be considered a possible path, 3 requirements must be met:

- the current state of the current configuration must be the same as in the transition (*transitions\[i]\[0]*).
- the first letter of the current configuration input word must be the same symbol as the transition input alphabet (*transitions\[i]\[1]*), \[if there is 1st letter in the word in the current setting] or if the symbol for the transition input alphabet is an ε.
- the top of the current setting should be the same as the alphabet symbol of the transition (*transitions\[i]\[2]*), \[if there is a symbol at the top of the stack in the current setting] or if the transition stack alphabet symbol is an ε.

If a transition is approved as a possible path to take, the current configuration is copied and the following properties are changed:
- If the input alphabet of the transition is different from ε, the first letter of the word is consumed;
- if the symbol of the transition stack alphabet is different from ε, the top of the stack is consumed;
- if the new symbol of the transition stack alphabet is different from ε, add the symbol to the top of the stack;
- we change the current state to the new current state of the transition.

After making the changes it is added to the execution queue and after checking all transitions to the current state, it is taken from the queue, and then the next element of the queue is executed with its own configuration and the process repeats itself.

To check if the computation has been accepted the word size must be 0 and (either an acceptance/final state has been reached or the stack is empty).

### *config = {}* variables
During program execution, the automaton configuration was stored in the variable *config*, where the information is stored as follows:
config\[1]: input alphabet

config\[2]: stack alphabet

config\[3]: symbol to consider to represent epsilon or lambda (must not belong to input alphabet or stack)

config\[4]: initial stack symbol (default: Z)

config\[5]: state set

config\[6]: initial state

config\[7]: set of acceptance states
	
### How to run the program
- The instruction format for program execution is:
	    `python main.py “automata.txt” “input”`
    
  **Example:**  
  `python main.py examples/ww^r.txt aabbaa`

- For testing, in the *"examples"* directory of this repository there are some examples of Pushdown Automata files in the format that should be used as input to the program.

- The program output format is:
  `{'word', 'current_state', 'stack'}`

  Where *‘word’* indicates the final content of the input word, *‘current_state’* indicates the state in which the automaton is at the end of execution and *‘stack’* indicates the final content of the stack.
  
  In addition, at the exit of the program there will be a line indicating the final result of the automaton execution, which can be:
  
  `0: Computing done and accepted.`  
  `-1: Computation terminated and rejected.`  
  `-3: Value entered in word is incorrect.`  
  `-4: Invalid epsilon`

  **Output Example:**  
  `0: Computing done and accepted.`  
  `{'word': '', 'current_state': 'q2', 'stack': []}`
  
- To convert Stack Automata from *.jff* to *.txt* (format supported by the program), use the *jflap-pda2utfpr.py* file as follows:

  `python jflap-pda2utfpr.py pda.jff pda.txt`
