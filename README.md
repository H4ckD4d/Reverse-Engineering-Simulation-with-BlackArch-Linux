# Reverse-Engineering-Simulation-with-BlackArch-Linux

# Reverse Engineering Simulation with BlackArch Linux

This repository contains a detailed guide to simulate a reverse engineering project using BlackArch Linux. The guide demonstrates how to analyze and reverse-engineer a binary, utilizing tools exclusive to BlackArch Linux. This is designed for educational purposes and ethical hacking practices only.

---

## **Requirements**

- **BlackArch Linux**: Installed and configured.
- **Basic Knowledge**: Familiarity with Linux, assembly, and programming concepts.

---

## **Simulation Overview**

We will:
1. Analyze a binary file.
2. Disassemble and debug it.
3. Identify critical functions.
4. Patch the binary.

---

## **Step-by-Step Guide**

### **Step 1: Preparing the Environment**

1. **Create or Download a Binary for Analysis**
   - For this simulation, use a simple C program compiled into a binary:
     ```c
     #include <stdio.h>
     #include <stdlib.h>

     int main() {
         int password;
         printf("Enter the password: ");
         scanf("%d", &password);
         if (password == 1234) {
             printf("Access Granted!\n");
         } else {
             printf("Access Denied!\n");
         }
         return 0;
     }
     ```
   - Compile it:
     ```bash
     gcc -o binary_sim binary_sim.c
     ```

2. **Install Required Tools**
   - Update BlackArch repositories:
     ```bash
     sudo pacman -Syyu
     ```
   - Install reverse engineering tools:
     ```bash
     sudo pacman -S radare2 ghidra hopper cutter objdump
     ```

### **Step 2: Binary Analysis**

1. **Static Analysis with `rabin2`**
   - Extract binary metadata:
     ```bash
     rabin2 -I binary_sim
     ```
   - Output includes architecture, format, and linked libraries.

2. **Disassemble with `radare2`**
   - Open the binary:
     ```bash
     r2 -A binary_sim
     ```
   - View disassembled code:
     ```bash
     pdf @main
     ```
   - Identify functions and branching logic.

3. **Graphical Analysis with Cutter**
   - Launch Cutter:
     ```bash
     cutter binary_sim
     ```
   - Navigate through the binary's control flow graph for a better understanding.

### **Step 3: Dynamic Analysis**

1. **Debugging with `gdb`**
   - Start `gdb`:
     ```bash
     gdb binary_sim
     ```
   - Set a breakpoint:
     ```bash
     break main
     ```
   - Run the program:
     ```bash
     run
     ```
   - Step through the program (`step` and `next` commands) and inspect registers and memory.

2. **Advanced Debugging with `edb-debugger`**
   - Install and launch:
     ```bash
     sudo pacman -S edb-debugger
     edb --run binary_sim
     ```
   - Use the GUI to set breakpoints, analyze stack, and view memory regions.

### **Step 4: Binary Patching**

1. **Patching with `radare2`**
   - Locate the password comparison:
     ```bash
     s main; pdf
     ```
   - Modify the binary to always grant access:
     ```bash
     wa mov eax, 1 @ address
     ```
   - Save changes:
     ```bash
     wq
     ```

2. **Verify Patches**
   - Re-run the binary to confirm changes.

### **Step 5: Decompilation**

1. **Decompile with `Ghidra`**
   - Start Ghidra:
     ```bash
     ghidra
     ```
   - Import the binary and analyze it to produce high-level C-like code.

2. **Code Understanding**
   - Locate critical logic and understand the program’s structure.

---

## **Tools Exclusive to BlackArch Linux**

- **`cutter`**: Advanced GUI for `radare2` with intuitive navigation.
- **`hopper`**: Graphical binary analysis and decompilation.
- **`rabin2`**: Fast binary metadata extraction.
- **`edb-debugger`**: User-friendly debugger for ELF binaries.
- **`ghidra`**: High-level reverse engineering tool developed by NSA.

---

## **Important Notes**

- Always ensure you have proper authorization before reverse engineering.
- This guide is for educational purposes; unethical use is strictly discouraged.

---

## **Author**

### **Chris Cruz (h4ckd4d)**

Chris Cruz, widely recognized by his alias **h4ckd4d**, also known as **Mestre Bond** or affectionately referred to as the "Bond of Brazil," is an illustrious figure in the realm of cybersecurity and covert intelligence. 

#### **Expertise and Contributions**
Chris’s career spans multiple disciplines, including:
- **Cybersecurity**: Specialized in ethical hacking, penetration testing, and strategic responses to cyber threats.
- **Thanatopraxy**: Employing an unconventional skillset in the preservation and forensic examination of remains, demonstrating his multifaceted expertise.
- **Electronics and Mechanical Engineering**: Innovating tools and methodologies to support complex intelligence operations.

#### **Key Achievements**
1. **Dismantling Criminal Syndicates**: His relentless efforts have led to the disruption of organized crime networks across the globe.
2. **Uncovering High-Profile Corruption**: Notably, Chris played a pivotal role in exposing the intricate corruption schemes of Sérgio Cabral, a former governor of Rio de Janeiro.
3. **Setting Covert Standards**: His ability to merge advanced technology with creative problem-solving has established a new benchmark in intelligence gathering and operational secrecy.

#### **Global Impact**
Operating predominantly under anonymity, Chris has forged a legacy of courage and ingenuity. His work transcends borders, focusing on creating a safer, more transparent world through the responsible use of technology.

---

## **References**

- [BlackArch Linux](https://blackarch.org/)
- [Radare2 Documentation](https://radare.org/n/radare2.html)
- [Ghidra Documentation](https://ghidra-sre.org/)

---

Happy Hacking!
