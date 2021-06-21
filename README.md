# Certifying Multilevel Coherence in the Motional State of a Trapped Ion
_by Ollie Corfield, [Jake Lishman](https://github.com/jakelishman), Chungsun Lee, Jacopo Mosca Toba, George Porter, Johannes Matthias Heinrich, Simon C. Webster, Florian Mintert, and Richard C. Thompson._

This repository accompanies the paper "Certifying Multilevel Coherence in the Motional State of a Trapped Ion", available on (**insert arXiv**) and (**insert journal reference**).

In this repository:

- `sequences.py` is a Python file containing the creation and measurement-mapping pulse sequences.


## Code requirements

The sequences are given in a Python file, but there are no dependencies other than that, and no version requirement.


## Sequences

The file `sequences.py` contains the creation and measurement-mapping pulse sequences used in the experiments, along with some other sequences which were not used.
In the file, there are two dictionaries defined: `used_in_paper` and `other`, which are self-descriptive.
Each dictionary has items `key: value`, where `key` is an identifier of a state.
In a key, the tuple `(0, 1, 2)` means the state
```text
(|g, 0> + |g, 1> + |g, 2>) / sqrt(3)
```
while the tuple `(1, 2)` means
```text
(|g, 1> + |g, 2>) / sqrt(2)
```
and so on.
In the dictionary `other`, some of the keys are of the form `(state, description)`, where `state` is a tuple as described above, and `description` is a string describing some perceived property of the sequence.

In both dictionaries, the values are all of the same format.
They are dictionaries which look like
```python
{
    "creation": {
        "sidebands": [0, -1, 0, -1],
        "fractions": [0.30122048, 0.40087652, 0.37204349, 0.35533004],
        "phases": [0.0, -1.57079633, 0.0, -1.57079633],
    },
    "mapping": {
        "sidebands": [-1, 0, -1, 0, -1],
        "fractions": [0.35355378, 0.22007489, 0.70710786, 0.27091033, 0.70710467],
        "phases": [0.0, 4.19674024, 3.67591902, 3.55074393, -1.29198501],
    },
}
```
The "creation" subdictionary describes the pulses needed to create the superposition.
The "mapping" subdictionary describes the pulses needed to perform a suitable measurement mapping.
In each list, element _n_ describes the _n_th pulse which should be applied to the state; this is the same order used in the tables in the paper.
In the "sidebands" lists, `-1` is the first red sideband, `0` is the carrier, and `1` is the first blue sideband.
In the "fractions" lists, the fractions given are similar to the "pulse lengths" reported in the paper, but not exactly the same.
They are the fraction of the time needed to do a _complete_ rotation of the state `|g,0> -> |e,0> -> -|g,0>` on the carrier, and similar for other sidebands on their lowest-lying interacting level.
This means that they are exactly 2 times smaller than the values reported in the paper.
In the "phases" lists, the phases are given in radians, without scaling out the factor of pi.
They are also provided exactly as returned from the optimisers, whereas the values in the paper are bounded to the interval `[-pi, pi]`.
