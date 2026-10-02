# Arithmetic Operations: Multiplication (`mul`)

## Program 1: `mul1.asm`

### 1. Operation Details
- **Source File:** `mul1.asm`
- **Instruction Executed:** `mul`
- **Observed EFLAGS in GDB:** `[ IF ]`

### 2. Flag Status and Explanations

| Flag | Value in GDB | Status | Arithmetic & Architectural Explanation |
| :--- | :---: | :---: | :--- |
| **CF (Carry)** | 0 | Cleared | In x86 unsigned multiplication, CF is cleared to 0 because the upper half of the product register (e.g., `AH` or `DX`) is `0`. The entire product fits within the lower register alone. |
| **OF (Overflow)** | 0 | Cleared | In unsigned `mul`, the Overflow Flag mirrors the Carry Flag. It is cleared to 0 because the upper half of the product is `0` (no overflow beyond the lower register). |
| **ZF (Zero)** | 0 | Cleared | **Undefined**. Per the Intel x86 architecture manual, the Zero Flag is left undefined following a `mul` instruction. |
| **SF (Sign)** | 0 | Cleared | **Undefined**. The Sign Flag is left undefined after multiplication. |
| **PF (Parity)** | 0 | Cleared | **Undefined**. Parity is not reliably calculated or updated by `mul`. |
| **AF (Auxiliary)** | 0 | Cleared | **Undefined**. Left undefined after `mul`. |
| **IF (Interrupt)** | 1 | Set | System control flag indicating maskable hardware interrupts are enabled by the operating system (not an arithmetic status flag). |

> **Key Architectural Takeaway:** For unsigned multiplication (`mul`), the x86 CPU only defines CF and OF. Both flags evaluate whether the upper half of the double-width product register contains non-zero data. Since both are cleared, the product did not exceed the capacity of the primary accumulator.


# Arithmetic Operations: Multiplication (`mul`)

## Program 1: `mul1.asm`

### 1. Operation Details
- **Source File:** `mul1.asm`
- **Instruction Executed:** `mul`
- **Observed EFLAGS in GDB:** `[ IF ]`

### 2. Flag Status and Explanations

| Flag | Value in GDB | Status | Arithmetic & Architectural Explanation |
| :--- | :---: | :---: | :--- |
| **CF (Carry)** | 0 | Cleared | In x86 unsigned multiplication, CF is cleared to 0 because the upper half of the product register (e.g., `AH` or `DX`) is `0`. The entire product fits within the lower register alone. |
| **OF (Overflow)** | 0 | Cleared | In unsigned `mul`, the Overflow Flag mirrors the Carry Flag. It is cleared to 0 because the upper half of the product is `0` (no overflow beyond the lower register). |
| **ZF (Zero)** | 0 | Cleared | **Undefined**. Per the Intel x86 architecture manual, the Zero Flag is left undefined following a `mul` instruction. |
| **SF (Sign)** | 0 | Cleared | **Undefined**. The Sign Flag is left undefined after multiplication. |
| **PF (Parity)** | 0 | Cleared | **Undefined**. Parity is not reliably calculated or updated by `mul`. |
| **AF (Auxiliary)** | 0 | Cleared | **Undefined**. Left undefined after `mul`. |
| **IF (Interrupt)** | 1 | Set | System control flag indicating maskable hardware interrupts are enabled by the operating system (not an arithmetic status flag). |

> **Key Architectural Takeaway:** For unsigned multiplication (`mul`), the x86 CPU only defines CF and OF. Both flags evaluate whether the upper half of the double-width product register contains non-zero data. Since both are cleared, the product did not exceed the capacity of the primary accumulator.