---
title: Research
layout: default
---

# Research

## Iterative embedding-based screening of metagenomic enzymes

*M.S. thesis work, KAIST / KRIBB, 2025 – present*

Environmental metagenomes carry genes from microbes that cannot be cultured, which makes them a
good source of new enzymes. Getting from those sequences to confirmed function is the hard part.
Homology-based search is cheap but only returns sequences that already resemble known enzymes.
Activity-based screening finds genuinely new ones but is limited by throughput and cost. Neither
approach has a way of using the results of one round to improve how the next round selects
candidates, so the Design–Build–Test–Learn cycle stays open.

My thesis connects the two halves: protein language model embeddings select the candidates, and
cell-free protein synthesis on a biofoundry measures what they actually do.

### Design — selecting candidates in embedding space

I extracted ORFs from 16 metagenome samples and generated ProtT5 embeddings for about
**5.3 million** of them, stored as a 1,024-dimensional vector database. I then took 98 bacterial
lipases with reported structures, mapped them into the same space, and used their mean embedding
as a reference vector. Ranking the metagenomic ORFs by cosine similarity to that vector gives a
candidate list that includes sequences too distant for homology search to return.

The assumption behind this is that a pretrained representation encodes catalytic function,
structure and biochemical properties together, so functional proximity can show up as distance
even when sequence identity is low. Whether that assumption holds is exactly what the screening
step tests.

### Build — making the rounds comparable

Iteration is only meaningful if every round runs under the same conditions, so I standardized
the validation workflow before running the screen.

- **Library construction.** Building the linear expression cassettes by tailing PCR, with the T7
  promoter and terminator carried in the primer 5′ tails, replaced a longer route that went
  through purification, quantification and Gibson assembly. A gradient PCR resolved the Tm gap
  between the forward and reverse anchors.
- **Cell-free extract.** I prepared S30 extract in-house from a GroEL/GroES-overexpressing
  strain. This removed the batch-to-batch variation of commercial kits and gave roughly 2.5×
  the expression yield by GFP comparison, along with activity on pNPO, pNPB and pNPP in the CalB
  positive control that the kit had not detected.
- **Automation.** An Echo 525 acoustic dispenser and automated liquid handlers standardized the
  96/384-well expression, dilution and assay steps, with an sfGFP expression control on every
  plate so that plate-to-plate variation in cell-free expression could be monitored.

### Test — Round 1

I screened **855 candidate ORFs** from nine libraries, drawn from seven metagenomes, against
three pNP substrates of different chain lengths, reading absorbance at 405 nm.

Instead of setting a threshold by hand, I used a robust Z-score computed from the background
signal on each plate, and required both Z ≥ 3 and a net absorbance above that plate's CalB
positive control. That gave **43 hit candidates (5.0%)**, of which **16 were active on two or
more substrates**. Because this is a single-replicate screen, every hit is at this stage a
statistical outlier; confirmation by replicate measurement is ongoing.

### Learn — feeding the results back

The measured activities and hit calls are the training data for the next round, and they feed
back in two ways.

1. **Updating the reference vector.** Confirmed hits join the known-enzyme set, which moves the
   reference vector toward the region that is both functionally close to the target and
   expressible in this particular cell-free system.
2. **Learning the metric.** The per-substrate measurements become labels for an activity
   prediction model built on a frozen ESM-C encoder with trainable pooling and projection heads.
   The ORFs with no detected activity matter as much as the hits here: they are experimentally
   demonstrated negatives rather than negatives guessed from sequence distance, which is what
   makes a learned distance metric possible at all.

The quantity I care about across rounds is the hit rate among the top-ranked candidates. Round 1
set that baseline at 5.0%, and whether iteration works is a question about whether that number
moves.

### Interpreting hits structurally

I generate predicted structures for the candidate set with ESMFold, which needs no MSA, and use
Foldseek to check whether hits with low sequence identity nonetheless share the α/β-hydrolase
fold. FoldDisco then searches for the catalytic motif geometry itself: the Ser–His–Asp triad and
the oxyanion hole, which sit far apart in sequence but close together in space. This is how
remote homology recovered by embedding distance gets structural support, and it also supplies
interpretable features for the next round of selection.

---

## Protein language model representations

*Collaborative work, presented at KMB 2025*

Protein language models are usually read out by averaging over residue tokens. We found that
single-token embeddings, which are normally discarded, can carry global information about the
whole protein, and applied this to bacterial essential-gene prediction, where it improved
performance by up to 17% over average pooling.

---

## Research interests

- Representation learning for proteins, and what those representations encode beyond sequence
- Closing the gap between computational prediction and wet-lab outcome
- Cell-free systems and biofoundry automation as a fast, reproducible test bed
- Enzyme discovery and engineering for industrial and environmental applications
- How evidence generated by AI models can be documented and controlled well enough to stand up
  in a regulated development process
