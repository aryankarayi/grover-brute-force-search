# Grover's Algorithm in Brute-Force Attacks

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://grover-brute-force-search.streamlit.app/)
![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

An interactive Streamlit app that compares **classical brute-force search** with **Grover's quantum search algorithm** when looking for a target password in an unordered list. Built with [Qiskit](https://www.ibm.com/quantum/qiskit) during the Quantum Ready program.

**[Try the live demo](https://grover-brute-force-search.streamlit.app/)** · **[Screenshots](#screenshots)** · **[Run it locally](#run-it-locally)**

---

## What it does

- Builds a real Grover circuit (oracle + diffuser) in Qiskit for **2 to 10 qubits**, which means a search space of up to **1,024 passwords** taken from a list of common passwords.
- Simulates the circuit with Qiskit's `Statevector` and plots the probability of measuring the target after each Grover iteration.
- Compares the number of classical checks (O(N)) against Grover oracle calls (about O(√N)) for the chosen target.
- Includes a scaling explorer and a short security discussion of what Grover's algorithm means for symmetric key sizes.

> **Note:** the quantum algorithm runs on a classical simulator, so every comparison counts *oracle calls and checks*, not wall-clock time.

## Screenshots

### Experiment dashboard

![Full dashboard view](docs/full_page.png)

### Grover iterations at the maximum setting

![Target probability over many iterations](docs/max_iterations.png)

## How it works

1. Start with a uniform superposition over all N = 2ⁿ password indices.
2. The **oracle** flips the phase of the target index.
3. The **diffuser** reflects every amplitude about the mean, boosting the target's amplitude.
4. Repeat about ⌊(π/4)·√N⌋ times, then measure.

### How the cost scales

Grover's algorithm gives a *quadratic* speedup: roughly √N oracle calls instead of up to N classical checks.

| Qubits | Search space (N) | Classical checks (worst case) | Grover iterations ⌊(π/4)·√N⌋ |
|:------:|:----------------:|:-----------------------------:|:----------------------------:|
| 2      | 4                | 4                             | 1                            |
| 4      | 16               | 16                            | 3                            |
| 6      | 64               | 64                            | 6                            |
| 8      | 256              | 256                           | 12                           |
| 10     | 1,024            | 1,024                         | 25                           |

## Run it locally

Requires Python 3.10+.

```bash
git clone https://github.com/aryankarayi/grover-brute-force-search.git
cd grover-brute-force-search
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
streamlit run streamlit_app.py
```

On macOS or Linux, activate the virtual environment with `source .venv/bin/activate` instead.

The app opens at `http://localhost:8501`.

## Project structure

```
streamlit_app.py          # app and Grover circuit code
10k-common-passwords.txt  # password list used as the search space
requirements.txt          # Python dependencies
.streamlit/config.toml    # Streamlit theme
docs/                     # README screenshots
LICENSE                   # MIT license
```

## Tech stack

- **Python** 3.10+ 
- **Qiskit** for building and simulating the Grover circuit
- **Streamlit** for the interactive web app

## Team

Built during the 10-week Quantum Ready program by:

- Aryan Karayi ([@aryankarayi](https://github.com/aryankarayi))
- Sami Nadweh ([@sami22345](https://github.com/sami22345))
- Fabio Castro ([@FabioCastroMorffi](https://github.com/FabioCastroMorffi))
- Evan Hinojosa ([@Farbirb](https://github.com/Farbirb))

## License

MIT, see [LICENSE](LICENSE).
