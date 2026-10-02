## Program 2: `sub2.asm`

### 1. Operation Details
- **Source File:** `sub2.asm`
- **Instruction Executed:** `sub`
- **Observed EFLAGS in GDB:** `[ CF PF SF IF ]`

### 2. Flag Status and Explanations

| Flag | Value in GDB | Status | Arithmetic Reason |
| :--- | :---: | :---: | :--- |
| **CF (Carry/Borrow)** | 1 | **Set** | An unsigned borrow occurred. The value being subtracted (subtrahend) was larger than the starting value (minuend), forcing an unsigned wrap-around past zero. |
| **PF (Parity)** | 1 | **Set** | The least significant byte of the result contains an even number of set bits (`1`s). In x86 architecture, an even bit count sets the Parity Flag to 1. |
| **SF (Sign)** | 1 | **Set** | The most significant bit (MSB) of the result is `1`, indicating that the result is negative in signed two's complement representation. |
| **OF (Overflow)** | 0 | Cleared | No signed overflow occurred. The mathematical result fits within the valid signed boundaries of the destination register width (e.g., within $-128$ to $+127$ for an 8-bit register or $-32,768$ to $+32,767$ for a 16-bit register). |
| **ZF (Zero)** | 0 | Cleared | The result of the subtraction is non-zero (the two operands were not equal). |
| **AF (Auxiliary)** | 0 | Cleared | No borrow was required from bit 4 into bit 3 during the low-nibble calculation. |
| **IF (Interrupt)** | 1 | Set | System control flag indicating maskable hardware interrupts are enabled by the operating system (not an arithmetic status flag). |

> **Key Arithmetic Takeaway:** The combination of `CF = 1` and `SF = 1` with `OF = 0` demonstrates a classic case of subtracting a larger positive unsigned number from a smaller positive unsigned number. Unsigned logic interprets this as an underflow/borrow (`CF = 1`), while signed logic interprets this correctly as a valid negative number without signed overflow (`SF = 1`, `OF = 0`).


## Program 3: `sub3.asm`

### 1. Operation Details
- **Source File:** `sub3.asm`
- **Instruction Executed:** `sub` (or multi-precision `sbb`)
- **Observed EFLAGS in GDB:** `[ SF IF ]`

### 2. Flag Status and Explanations

| Flag | Value in GDB | Status | Arithmetic Reason |
| :--- | :---: | :---: | :--- |
| **SF (Sign)** | 1 | **Set** | The most significant bit (MSB) of the result register is `1`, indicating that the result is negative when evaluated as a signed two's complement integer. |
| **CF (Carry/Borrow)** | 0 | Cleared | No unsigned borrow occurred. Either the minuend was greater than or equal to the subtrahend in an unsigned context, or no borrow was carried out of the highest bit. |
| **OF (Overflow)** | 0 | Cleared | No signed two's complement overflow occurred. The signed mathematical result fits properly within the register bounds without corrupting the sign bit. |
| **ZF (Zero)** | 0 | Cleared | The final result is non-zero. |
| **PF (Parity)** | 0 | Cleared | The least significant byte (lowest 8 bits) of the result contains an odd count of `1` bits (odd parity), keeping PF cleared to 0. |
| **AF (Auxiliary)** | 0 | Cleared | No borrow was propagated across the nibble boundary (from bit 4 to bit 3). |
| **IF (Interrupt)** | 1 | Set | Standard operating system flag indicating hardware interrupts are enabled (system control flag, not an arithmetic status flag). |

> **Key Arithmetic Takeaway:** Having `SF = 1` while `CF = 0` and `OF = 0` confirms that the operation resulted in a valid signed negative number without causing signed arithmetic overflow or unsigned underflow/borrow wrap-around.