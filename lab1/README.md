# Lab 1: Introduction to VHDL Programming and Open-Source Simulation Tools

## Objective

- Install and familiarize with the open-source VHDL development environment:
  - VS Code
  - GHDL
  - GTKWave
- Understand the fundamental components of a VHDL design:
  - Libraries and Packages
  - Entity
  - Architecture
- Create, compile, simulate, and verify a simple digital circuit using VHDL.

---

## Theory

**VHDL (VHSIC Hardware Description Language)** is a standardized hardware description language used for modeling and designing digital systems. VHSIC stands for **Very High-Speed Integrated Circuit**.

Unlike traditional programming languages such as C or Python, which execute instructions sequentially, VHDL is designed to describe hardware where multiple operations occur simultaneously. This makes it ideal for modeling digital circuits and systems.

### Main Components of a VHDL Design

1. **Libraries and Packages** – Provide predefined data types, operators, and functions.
2. **Entity** – Defines the external interface of the design, including inputs and outputs.
3. **Architecture** – Describes the internal behavior and functionality of the entity.

---

## Core Structural Components

### Libraries and Packages

Two commonly used libraries in VHDL are:

- **STD Library** – Provides basic data types such as `bit`, `boolean`, `integer`, and `character`.
- **IEEE Library** – Provides standard logic types used in digital design.

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;
```

### Entity

An entity defines the external interface of a circuit.

**Example: 2-Input AND Gate**

```vhdl
entity AND_GATE is
    port(
        A : in std_logic;
        B : in std_logic;
        Y : out std_logic
    );
end entity AND_GATE;
```

### Architecture

The architecture defines the behavior of the entity.

```vhdl
architecture Dataflow of AND_GATE is
begin
    Y <= A and B;
end architecture Dataflow;
```

---

## VHDL Modeling Styles

### 1. Behavioral Modeling

Describes how the circuit operates using sequential statements.

```vhdl
architecture Behavioral of AND_GATE is
begin
    process(A, B)
    begin
        Y <= A and B;
    end process;
end architecture Behavioral;
```

### 2. Dataflow Modeling

Describes data movement through concurrent signal assignments.

```vhdl
architecture Dataflow of AND_GATE is
begin
    Y <= A and B;
end architecture Dataflow;
```

### 3. Structural Modeling

Builds larger circuits by interconnecting smaller components.

```vhdl
architecture Structural of AND_GATE is
    component AND2
        port(X, Z : in std_logic; W : out std_logic);
    end component;
begin
    U1 : AND2 port map(X => A, Z => B, W => Y);
end architecture Structural;
```

---

## Data Types and Signals

### `std_logic`

Supports multiple logic states:

| Value | Description |
|---------|-------------|
| `'0'` | Logic Low |
| `'1'` | Logic High |
| `'Z'` | High Impedance |
| `'U'` | Uninitialized |

### `std_logic_vector`

Used to represent a collection of logic bits.

```vhdl
std_logic_vector(7 downto 0)
```

This creates an 8-bit vector with bit 7 as the MSB and bit 0 as the LSB.

### Signals

Signals are internal connections used to transfer data within a design.

```vhdl
architecture Example of MY_CIRCUIT is
    signal internal_wire : std_logic;
    signal data_bus : std_logic_vector(7 downto 0);
begin
end architecture Example;
```

---

## VHDL Simulation Flow

```text
Source Code (.vhd)
        ↓
Analysis (ghdl -a)
        ↓
Elaboration (ghdl -e)
        ↓
Simulation (ghdl -r)
        ↓
VCD Waveform File
        ↓
GTKWave Visualization
```

### Stages

- **Analysis** – Checks syntax and semantic correctness.
- **Elaboration** – Links entities with architectures and builds the design hierarchy.
- **Simulation** – Executes test cases and generates outputs.
- **Waveform Visualization** – Displays signal behavior using GTKWave.

---

## Discussion

This experiment introduced the complete VHDL development workflow using VS Code, GHDL, and GTKWave.

A key concept observed during simulation was **concurrency**. Unlike software programs that execute sequentially, VHDL models hardware where multiple operations occur simultaneously. The GTKWave waveforms demonstrated how outputs responded immediately to input changes, accurately reflecting real digital circuit behavior.

---

## Conclusion

This experiment successfully demonstrated the process of designing, compiling, simulating, and verifying a simple VHDL circuit using open-source tools.

Key concepts covered:

- Libraries and Packages
- Entities and Architectures
- Signals and Data Types
- VHDL Modeling Styles
- Simulation and Waveform Analysis

The successful simulation and waveform verification provided practical experience with the VHDL development workflow and established a foundation for future digital design experiments.