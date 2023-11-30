https://www.cobalt.io/blog/overflow-vulnerabilities
https://www.cobalt.io/blog/pentester-guide-to-exploiting-buffer-overflow-vulnerabilities

https://www.youtube.com/watch?v=1S0aBV-Waeo
https://www.youtube.com/watch?v=yJF0YPd8lDw&t=2863s

[[Stos (stack) i sterta (heap)]]
# Assembler
* NASM -Netwide Assembler
* MASM - Microsoft Macro Assembler
ISA (Instruction Set Architecture) - set of instructions to understand and use to write a program: memory, registry, instructions, ...
most common ISA: x86 (32 bit), x64 (64 bit) (długość rejestru)
General Purpose Registers (GPRs)

# ASLR (Address space layout randomization)
[Address space layout randomization](https://en.wikipedia.org/wiki/Address_space_layout_randomization)
# DEP (Data Execution Prevention)

# useful registers in assembly 
Rxx - 64-bit Registers - 
Exx - 32-bit Registers: 
- https://www.eecg.toronto.edu/~amza/www.mindsec.com/files/x86regs.html
- https://medium.com/@sharonlin/useful-registers-in-assembly-d9a9da22cdd9
## EIP
instruction pointer for the next address called after an instruction is run. (wherewer next instruction is) 
## ESP
stack pointer - it holds the current address that you’re running
## EBP
base pointer for the current stack frame. When a function is called, some space is reserved on the stack for local variables, which is referenced as EBP.
## ESI
Source index for string operations. Essentially, this stores the start of the string that you’re saving to memory and is also used for string/memory copying.
## RET
kończy wykonanie procedury i nakazuje powrót do program wywołującego

# Programy
## Immunity Debugger - debugging binaries.
mona plugin - https://github.com/corelan/mona
```
# na dole w polu komend Immunity Debugger
!mona config -set workingfolder C:\ImmunityLogs\%p #configure working folder 

# mona create payload
!mona pc 100 # payload ze 100 znakami

# mona find correct offset 
!mona po xxxxx # x wartośc z EIP

# auto generate msf module 
!mona suggest

!mona jmp -r esp 
# -r register we want to target
```
## IDA Pro
## Metasploit
pattern_create
	./pattern_create.rb 100
pattern_offset
	./pattern_offset.rb 22
# Real world BOF
python listener 


# Exploiting Buffer Overflows
Atak buffer overflow na stosie można przeprowadzić w następujący sposób:

1. **Nadmiar danych**: Atakujący wprowadza do bufora więcej danych, niż jest on w stanie pomieścić.
2. **Nadpisanie danych na stosie**: Nadmiarowe dane zaczynają być zapisywane poza zaalokowanym buforem, co może prowadzić do nadpisania zmiennych na stosie, w tym adresu powrotu.
3. **Nadpisanie adresu powrotu**: Atakujący umieszcza w nadmiarowych danych złośliwy kod (zwany exploitem) i zmienia adres powrotu (EIP) na adres, w którym znajduje się ten złośliwy kod.
4. **Wykonanie złośliwego kodu**: Gdy funkcja kończy swoje wykonywanie i próbuje powrócić do miejsca, z którego została wywołana, procesor wykonuje złośliwy kod umieszczony przez atakującego, który jest teraz wskazywany przez adres powrotu (EIP).
Which register value will help us to determine the required bytes of data before overriding the EIP register? - EIP