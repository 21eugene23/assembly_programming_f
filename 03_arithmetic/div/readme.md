# Arithmetic Operations: Division (`div`)

## Program 1: `div1.asm`

### 1. Operation Details
- **Source File:** `div1.asm`
- **Instruction Executed:** `div`
- **Observed EFLAGS in GDB:** `[ AF IF ]`

### 2. Flag Status and Explanations

| Flag | Value in GDB | Status | Architectural / Arithmetic Reason |
| :--- | :---: | :---: | :--- |
| **CF (Carry)** | 0 | Cleared | **Undefined**. According to the Intel x86 reference specification, status flags are left officially undefined following integer division (`div`/`idiv`). |
| **OF (Overflow)** | 0 | Cleared | **Undefined**. The CPU does not set the Overflow Flag to indicate signed or unsigned capacity limits after a division instruction. |
| **ZF (Zero)** | 0 | Cleared | **Undefined**. The Zero Flag is undefined and does not reliably indicate whether the quotient or remainder is zero. |
| **SF (Sign)** | 0 | Cleared | **Undefined**. The Sign Flag is undefined and does not reliably reflect the sign bit of the quotient. |
| **PF (Parity)** | 0 | Cleared | **Undefined**. The Parity Flag is not updated to reflect the parity of the result. |
| **AF (Auxiliary)** | 1 | **Set** | **Undefined**. Although GDB shows `AF` as set (`1`), this is a hardware micro-operation artifact left behind by the CPU's internal division circuitry; per the Intel manual, it remains formally undefined. |
| **IF (Interrupt)** | 1 | **Set** | System control flag indicating that maskable hardware interrupts are enabled by the operating system (not an arithmetic status flag). |

>## Program 2: `div3.asm`

### 1. Operation Details
- **Source File:** `div3.asm`
- **Instruction Executed:** `div`
- **Observed EFLAGS in GDB:** `[ AF IF ]`

### 2. Flag Status and Explanations

| Flag | Value in GDB | Status | Architectural / Arithmetic Reason |
| :--- | :---: | :---: | :--- |
| **CF (Carry)** | 0 | Cleared | **Undefined**. Per the Intel x86 reference manual, status flags are officially undefined following an unsigned integer `div` instruction. |
| **OF (Overflow)** | 0 | Cleared | **Undefined**. The processor does not update the Overflow Flag after a division instruction. |
| **ZF (Zero)** | 0 | Cleared | **Undefined**. The Zero Flag is undefined and does not reliably indicate whether the quotient or remainder evaluated to zero. |
| **SF (Sign)** | 0 | Cleared | **Undefined**. The Sign Flag does not reflect the sign or MSB of the quotient. |
| **PF (Parity)** | 0 | Cleared | **Undefined**. Parity is not computed or updated following a division operation. |
| **AF (Auxiliary)** | 1 | **Set** | **Undefined**. Set to `1` as an internal micro-operation relic from the hardware ALU division cycles, but formally classified as undefined by the x86 architecture. |
| **IF (Interrupt)** | 1 | **Set** | System control flag indicating maskable hardware interrupts are enabled by the operating system (not an arithmetic status flag). |

> **Key Architectural Takeaway:** Just like `div1.asm`, `div3.asm` demonstrates that x86 hardware division leaves all condition codes in an undefined state. Software must test registers explicitly (e.g., using `cmp` or `test` on the quotient or remainder) if conditional branching is required.