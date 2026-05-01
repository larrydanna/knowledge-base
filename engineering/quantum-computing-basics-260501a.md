# Quantum Computing Basics

**Date:** 2026-05-01  
**Category:** engineering  
**Tags:** `quantum`, `qubits`, `circuits`, `measurement`, `computing`

---

## TL;DR

- A classical bit is either `0` or `1`; a qubit can be in a weighted state of both until measurement
- Quantum programs are usually described as **circuits**: prepare qubits, apply gates, then measure
- A gate does not mean "do magic"; it is a controlled transformation of the qubit state
- Measurement turns a quantum state into ordinary classical bits, which is the only part you finally get back
- The practical bridge is: **state -> gate -> interference -> measurement**

---

## Start with the classical picture

A normal program manipulates **bits**. Each bit is in one definite state:

- `0`
- `1`

Classical logic gates such as **AND**, **OR**, and **NOT** transform those bits step by step.

That gives us a useful starting bridge:

| Classical computing | Quantum computing |
|---|---|
| bit | qubit |
| logic gate | quantum gate |
| register of bits | register of qubits |
| program / instruction sequence | circuit |
| read variable value | measure qubit |

This mapping is not perfect, but it is close enough to build intuition.

---

## What a qubit really adds

A **qubit** is the basic unit of quantum information.

The low-level idea is that a qubit has two basis states, usually written as:

- `|0>`
- `|1>`

Unlike a classical bit, a qubit can also be in a combination of both:

```text
alpha|0> + beta|1>
```

That expression is called a **quantum state** or **superposition**.

The important concrete idea is not "it is both at once in a sci-fi sense."  
The useful meaning is:

- the qubit has an internal state with two amplitudes
- those amplitudes determine what happens when you measure it
- before measurement, you should think in terms of **probability amplitudes**, not final bit values

If `|alpha|^2 = 0.8` and `|beta|^2 = 0.2`, then measuring the qubit gives:

- `0` about 80% of the time
- `1` about 20% of the time

So the first practical bridge is:

**A qubit is not "a bit with more storage." It is a tiny state machine governed by amplitudes.**

---

## Superposition without the hype

Superposition is often explained badly.

A better concrete version is:

- a classical bit stores one current answer
- a qubit stores a state that can evolve toward different measured outcomes

That does **not** mean a quantum computer simply "tries every answer at once" and then hands you the right one. If that were true, quantum computing would be much easier than it is.

What matters is that quantum states can **interfere**.

Some paths through a computation reinforce each other. Others cancel out. Good quantum algorithms are designed so that wrong answers tend to cancel and useful answers become more likely when measured.

This is why the real power is not just superposition. It is:

1. Prepare a state space
2. Transform it with gates
3. Shape probabilities through interference
4. Measure at the end

---

## Gates are transformations, not commands

In classical code, a gate feels like a boolean operation.

In quantum computing, a **gate** is better understood as a transformation of the qubit state.

Three useful concrete examples:

### X gate

This is the closest thing to a classical NOT gate.

```text
|0> -> |1>
|1> -> |0>
```

### H gate (Hadamard)

This is the gate people use early because it creates useful superposition.

```text
|0> -> (|0> + |1>) / sqrt(2)
|1> -> (|0> - |1>) / sqrt(2)
```

You do not need to memorize the math yet. The concrete takeaway is:

- `H` takes a definite state and spreads it into a balanced quantum state

### CNOT gate

This is a two-qubit gate:

- one qubit is the **control**
- one qubit is the **target**
- if the control is `1`, the target flips

This gate becomes important because it can create **entanglement**.

---

## Measurement is where quantum becomes ordinary again

Measurement is the part most like crossing a boundary.

Before measurement:

- the system is described by amplitudes
- the qubit may be in superposition

After measurement:

- you get an ordinary classical result like `0` or `1`
- the quantum state collapses to match that result

That means a quantum program is not something you can inspect freely while it runs, the way you inspect normal variables in a debugger. Measuring early changes the state.

This is one of the biggest mental shifts for software people.

> [!IMPORTANT]
> You do not directly "read the superposition." You only get classical outcomes from measurement, usually after repeating the circuit many times.

---

## Why repeated runs matter

A single circuit run often gives only **one sampled result**.

So real quantum work usually means:

1. Build a circuit
2. Run it many times
3. Collect measurement counts
4. Look at the distribution

For example, after many runs you might observe:

```text
00 -> 498
11 -> 502
01 -> 0
10 -> 0
```

That kind of output is often more meaningful than one individual run.

The concrete bridge here is:

**Classical programs usually produce one deterministic output; quantum programs often produce a distribution you analyze statistically.**

---

## Entanglement: correlation that is built into the state

Entanglement is a relationship between qubits where the system must be described as a whole, not as independent parts.

One common example is this two-qubit state:

```text
(|00> + |11>) / sqrt(2)
```

If you measure the first qubit:

- sometimes you get `0`
- sometimes you get `1`

But once you do, the second qubit matches it.

The important low-level point is not just "they are linked." It is:

- the pair has one shared state
- you cannot fully explain each qubit separately

That shared structure is what many quantum protocols depend on.

---

## Circuits are the most concrete way to think

Quantum programs are commonly drawn as **circuit diagrams**.

Basic reading rules:

- each horizontal line is a qubit
- time moves left to right
- boxes and symbols are gates
- the meter symbol means measurement

A tiny example:

```text
q0: ---H---M---
```

This means:

1. Start with qubit `q0`, usually in `|0>`
2. Apply a Hadamard gate
3. Measure it

Because `H` creates an even superposition from `|0>`, repeated runs should produce about half `0` and half `1`.

Now a more interesting one:

```text
q0: ---H---@---M---
           |
q1: -------X---M---
```

This means:

1. Put `q0` into superposition
2. Use `q0` to control a CNOT on `q1`
3. Measure both

That circuit creates an entangled pair from `|00>`, and repeated runs tend to produce `00` or `11`, not random independent bits.

---

## Where the math starts to matter

You can learn useful intuition before going deep into the math, but eventually quantum computing rests on:

- vectors
- matrices
- complex numbers
- probabilities from squared magnitudes

That is why quantum computing often feels like a mix of:

- computer science
- linear algebra
- physics

If you are coming from programming, the most practical math bridge is:

| Idea | Concrete meaning |
|---|---|
| state vector | the current quantum state |
| gate matrix | the transformation applied to that state |
| amplitudes | values that influence measurement probabilities |
| measurement probabilities | squared magnitudes of amplitudes |

You do not need all of linear algebra on day one, but you do need to accept that quantum state is more naturally represented as math than as ordinary variables.

---

## What quantum computers are actually good at

Quantum computers are **not** general replacements for classical machines.

They are interesting when a problem has structure that quantum mechanics can exploit, especially in areas like:

- simulating quantum systems
- some search and optimization problems
- certain cryptographic and algebraic problems
- some chemistry and materials problems

For everyday CRUD apps, web APIs, dashboards, and business logic, a classical computer is still the right tool.

That is another useful bridge: think of quantum as a **specialized compute model**, not the next laptop CPU.

---

## Common misunderstandings

### "A qubit is just a bit with many values"

No. A qubit is not a tiny float or a mini array. Its power comes from state evolution, interference, and measurement behavior.

### "Quantum computers try every answer at once"

Not in the useful sense people imagine. Without interference and algorithm design, measurement just gives you samples, not magic answers.

### "If I add more qubits, I just get linearly more power"

No. The joint state space grows exponentially, which is why quantum systems are powerful but also hard to control.

### "Quantum output is random, so it is useless"

Not if the circuit is designed correctly. The goal is usually to shape the probability distribution so repeated measurements reveal useful structure.

---

## A good first mental model

If you want one practical model to keep:

1. **Initialize** qubits, usually to `|0>`
2. **Transform** them with gates
3. **Create structure** through superposition and entanglement
4. **Amplify or cancel** possibilities through interference
5. **Measure** to get classical bits
6. **Repeat** enough times to understand the result distribution

That model is simple, but it is close to how many introductory quantum circuits are actually used.

---

## Sources

[1] [Microsoft Learn - Overview of quantum computing](https://learn.microsoft.com/en-us/azure/quantum/concepts-overview)  
[2] [Microsoft Learn - The qubit](https://learn.microsoft.com/en-us/azure/quantum/concepts-the-qubit)  
[3] [Microsoft Learn - Quantum circuit diagram conventions](https://learn.microsoft.com/en-us/azure/quantum/concepts-circuits)  
[4] [IBM Quantum Learning - Basics of quantum information](https://quantum.cloud.ibm.com/learning/en/courses/basics-of-quantum-information)  
[5] [IBM Quantum Documentation - Introduction to Qiskit and IBM Quantum](https://quantum.cloud.ibm.com/docs/en/guides)

## See Also

[1] [Unlocking Quantum Computing - Slides and Interactive Workshop](https://unlockingquantumcomputing.com/)