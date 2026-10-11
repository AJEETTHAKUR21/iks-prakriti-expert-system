# Ayurvedic Prakriti Classification as a Rule-Based Expert System

**IKS Concept as CS Concept** | T.Y.B.Sc. Computer Science (Sem V), 2026-27
Smt. Devkiba Mohansinhji Chauhan College of Commerce and Science, Silvassa

**Submitted by:** Ajeet Thakur
**Guide:** Asst. Prof. Sini V.

## About the project

This project models the Ayurvedic assessment of an individual's constitution (Prakriti) as a rule-based expert system. Observed traits (lakshanas) such as body frame, skin, digestion and sleep are treated as facts. Guidelines from the Charaka Samhita and Sushruta Samhita are encoded as 30 IF-THEN production rules.

A forward-chaining inference engine accumulates Vata, Pitta and Kapha scores and classifies the result as a pure, dual-dosha or balanced (Sama) constitution. An explanation module lists every rule that fired, so each decision is transparent.

> **Note:** This is an academic classification tool. It is not a medical diagnosis or treatment system.

## IKS to CS mapping

| IKS element | CS element |
|---|---|
| Tridosha (Vata, Pitta, Kapha) | Output classes / score accumulators |
| Lakshana (observed trait) | Fact (attribute-value pair) |
| Shastra's guidelines | IF-THEN production rules (knowledge base) |
| Vaidya's reasoning | Inference engine (forward chaining) |
| Mishra Prakriti (dual) | Multi-label tie-breaking rule |
| Sama (balanced) Prakriti | Threshold rule on score spread |
| Vaidya explaining the assessment | Explanation module (rule trace) |

## How it works

1. If fewer than 6 of the 10 attributes are answered, the result is **Insufficient data**.
2. If the highest and lowest scores differ by at most 1, the result is **Tridoshic (Sama)**.
3. Else if the top two scores differ by at most 2, the result is a **dual-dosha** (e.g. Vata-Pitta).
4. Else the result is the **pure dosha** with the highest score.

Score ties are broken in the order Vata, Pitta, Kapha, so the output is always deterministic.

## Files

| File | Description |
|---|---|
| `prakriti_expert_system.py` | Knowledge base, inference engine, explanation module and CLI |
| `test_prakriti.py` | 16 unit tests |
| `IKS-PROJECT.pdf` | Full project report |

## How to run

Requires Python 3 (standard library only).

```bash
# Interactive mode
python3 prakriti_expert_system.py

# Demo with sample input
python3 prakriti_expert_system.py --demo

# Run all tests
python3 test_prakriti.py
```

### Sample output (demo)

```
Result : Vata (pure)
Scores : Vata=12, Pitta=0, Kapha=0
Rules fired:
  R01: frame = thin -> Vata +2
  R04: skin = dry -> Vata +1
  ...
```

## Tests

16 test cases cover pure, dual and balanced constitutions, boundary conditions, partial input, invalid values, unknown attributes, explanation consistency and rule-base size.

## Limitations

- Simplified knowledge base (10 attributes, 30 rules), not the full classical corpus
- Weights and thresholds are design choices and would need expert validation
- Inputs are self-assessed and forced into three categories
- Vikriti (current imbalance), age, season and region are not modelled

## References

1. Charaka Samhita, Vimana Sthana, Chapter 8
2. Sushruta Samhita, Sharira Sthana, Chapter 4
3. Russell, S. and Norvig, P., *Artificial Intelligence: A Modern Approach*
