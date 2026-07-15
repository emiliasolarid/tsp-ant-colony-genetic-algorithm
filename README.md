# TSP: Ant Colony Optimisation & Genetic Algorithm

Emilia Solari del Sol | AI Search coursework, Durham University

## What this is
Two metaheuristic algorithms implemented in Python to solve the Travelling Salesperson
Problem (TSP): Ant Colony Optimisation (AlgA) and a Genetic Algorithm (AlgB). Each has a
basic implementation and an enhanced version built on top of it, tested across ten city files
of varying size (from 12 to 535 cities).

Full description of the enhancements: [`AISearchProforma.pdf`](./AISearchProforma.pdf)

## Enhancements

**Ant Colony Optimisation**
- Min-max pheromone bounds to prevent premature convergence
- Elitist strategy emphasising the best tour found so far
- Candidate lists (nearest-neighbour restriction) to reduce computation per step
- 2-opt local search applied after each ant's tour construction
- Dynamic adjustment of alpha/beta parameters as the search progresses, intensified on stagnation

**Genetic Algorithm**
- Intelligent population initialisation: 70% random, 30% nearest-neighbour-seeded tours
- Adaptive mutation rate that increases under detected stagnation
- Two mutation operators (swap and inversion) alternated during search
- 2-opt local search applied probabilistically to offspring
- Problem-size adaptive parameters (population size, iterations, local search intensity)
- Edge sampling in 2-opt for large instances to control computation cost

Full rationale and design discussion for each is in the proforma linked above.

## Results

Best tour length and runtime found per city file, for each algorithm (best result from
either the basic or enhanced implementation, as required by the assignment's submission
format):

| City file | AlgA (ACO) length | AlgA runtime (s) | AlgB (GA) length | AlgB runtime (s) |
|---|---|---|---|---|
| 012 | 56 | 0.0 | 56 | 0.0 |
| 017 | 1,444 | 0.0 | 1,444 | 0.0 |
| 021 | 2,549 | 0.5 | 2,549 | 0.0 |
| 026 | 1,473 | 1.5 | 1,492 | 0.0 |
| 042 | 1,192 | 6.8 | 1,236 | 0.1 |
| 048 | 12,358 | 7.9 | 13,338 | 0.2 |
| 058 | 25,652 | 6.8 | 26,148 | 0.3 |
| 175 | 24,184 | 30.3 | 21,795 | 0.8 |
| 180 | 4,350 | 6.7 | 2,040 | 0.9 |
| 535 | 57,983 | 86.9 | 49,844 | 6.2 |

A few things stand out:
- On the smallest instances (12–21 cities) both algorithms find identical or near-identical tours, which is expected since these are close to optimal for either method at this scale.
- On the two largest instances (180 and 535 cities), the Genetic Algorithm found noticeably shorter tours than Ant Colony Optimisation, and did so 10–14x faster.
- Ant Colony Optimisation's runtime grows much faster with problem size: 86.9s at 535 cities versus 6.2s for the Genetic Algorithm on the same file. This tracks with ACO's higher per-iteration cost (pheromone updates and candidate-list evaluation across all ants) compared to the Genetic Algorithm's cheaper per-generation operations.

Note: these figures are the best tour found using either the basic or enhanced implementation of each algorithm, not a like-for-like basic-vs-enhanced comparison — the underlying data doesn't isolate the enhancement's individual contribution per file.

## Files
- `AlgAbasic.py` / `AlgAenhanced.py` - Ant Colony Optimisation, basic and enhanced
- `AlgBbasic.py` / `AlgBenhanced.py` — Genetic Algorithm, basic and enhanced
- `AISearchProforma.pdf` — full writeup of enhancements and design rationale

## Notes
- Built on supplied skeleton code as part of a university AI Search coursework assignment.
- No non-standard modules used (per assignment constraints) - implementations rely only on the Python standard library.
- Each basic/enhanced pair shares identical core parameters (population size, iteration count, etc.) so that any improvement in tour quality is attributable to the enhancement itself.
