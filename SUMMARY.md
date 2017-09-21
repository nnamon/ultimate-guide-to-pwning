# Summary

### Getting Started

* [Introduction to the Guide](README.md)
* [Overview](overview.md)
* [Quick Start](quickstart.md)

### Scripting for CTFs

* [Overview](combatscripting/overview.md)
* [Basic File Operations](combatscripting/fileoperations.md)
* [Network Operations](combatscripting/network.md)
* [Cryptography](combatscripting/cryptography.md)
* [Starting Processes](combatscripting/processes.md)

### Pwntools

* [Overview](pwntools/overview.md)
* [Workflow](pwntools/workflow.md)

### Linux Basics

* [Environment Setup](linux/environment.md)
* [Basic Commands](linux/commands.md)
* [procfs](linux/procfs.md)

### Linux (x86-64) Exploitation

* [Environment Setup](linuxexp/environment.md)
* [Basic Concepts](linuxexp/basics.md)
* [Defenses and Mitigations](linuxexp/defenses.md)
    * [Address Space Layout Randomisation](linuxexp/aslr.md)
    * [No eXecute](linuxexp/nx.md)
    * [Stack Canary](linuxexp/canary.md)
    * [Fortify Source](linuxexp/fortify.md)
    * [Position Independent Executable](linuxexp/pie.md)
    * [Control Flow Integrity](linuxexp/cfi.md)
* [Stack Based Corruption](linuxexp/stackoverflow.md)
    * [Jump to Shellcode](linuxexp/jumptoshellcode.md)
    * [Return Oriented Programming](linuxexp/rop.md)
    * [SigReturn Oriented Programming](linuxexp/sigreturn.md)
    * [Stack Pivoting](linuxexp/stackpivot.md)
    * [Uninitialised Local Variables](linuxexp/uninitalised.md)
* [Format String Attacks](linuxexp/formatstring.md)
* [Heap Based Corruption](linuxexp/heapoverflow.md)
    * [Use After Free](linuxexp/useafterfree.md)
    * [Double Free](linuxexp/doublefree.md)
    * [House of Spirit](linuxexp/houseofspirit.md)
* [Techniques and Tricks](linuxexp/techniques.md)
    * [Return to Procedure Linkage Table (PLT)](linuxexp/plt.md)
    * [Global Offset Table Overwrite](linuxexp/got.md)
    * [vsyscall Page](linuxexp/vsyscall.md)
    * [linux.gate.so.1](linuxexp/linuxgate.md)
    * [Stack Protect Information Leak](linuxexp/stackprotectil.md)
    * [Return to libc](linuxexp/ret2libc.md)
    * [Overwrite .dtors Section](linuxexp/dtors.md)
    * [Magic libc Gadgets](linuxexp/magiclibc.md)
    * [File Stream Structure Corruption](linuxexp/filestream.md)

### Linux Privilege Escalation

* Overview

### Memory Allocators

* jemalloc
* dlmalloc

### Miscellaneous Exploitation

* Overview
* Bash
    * General Tricks
    * Shellshock
* Python
    * Sandbox Escapes
    * Unsafe Deserialisation

### Web

* [Cross-Site Scripting](web/xss.md)
* [PHP](web/php.md)
    * Loose Comparisons
    * Local File Inclusion
    * Deserialisation

### Cryptography

* [Hashing](cryptography/hashing.md)
* [Public Key Cryptography](cryptography/publickey.md)

### Tools

* [Reverse Engineering and Exploitation](tools/re.md)
    * [IDA Pro](tools/idapro.md)
    * [Binary Ninja](tools/binaryninja.md)
    * [Pwntools](tools/pwntools.md)

#### Further Reading

* [References](furtherreading/references.md)
