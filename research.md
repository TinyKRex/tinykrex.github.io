---
title: Research
layout: default
---

# Research

## Closing the DBTL loop in metagenomic enzyme discovery

*M.S. thesis work, KAIST / KRIBB, 2025 – present*

Environmental metagenomes hold an enormous reservoir of genes from species that cannot be
cultured, but turning those sequences into confirmed function is still hard. Homology-based
screening is fast and cheap, yet only returns sequences that already resemble known enzymes.
Activity-based screening finds genuinely novel enzymes, but at a throughput and cost that
limits how far you can look. Both share a deeper problem: the results of one round cannot feed
back into how the next round picks candidates. The Design–Build–Test–Learn cycle never closes.

My thesis builds a platform where it does — **protein language model embeddings as the
selection engine, cell-free protein synthesis and a biofoundry as the validation engine**.

### Design — selection in representation space, not alignment space

I embedded roughly **6.9 million ORFs** extracted from eight metagenome samples (forest soil,
marine, plant rhizosphere, riparian soil) into a 1,024-dimensional vector database, mapped 97
curated lipases/esterases into the same space, and used their mean vector as a centroid. Ranking
every ORF by cosine similarity to that centroid — with UMAP used to inspect the cluster
structure of the candidate set — yielded **976 candidates**, including distant sequences that
homology search would never return.

### Build — making rounds comparable

Iteration only means something if every round runs under identical conditions, so the validation
workflow came first.

- **Tailing PCR** with T7 promoter and terminator built into the primer 5′ tails collapsed the
  DNA library route from four steps (ORF PCR → purification → quantification → Gibson assembly →
  linear PCR) to two. A gradient PCR (50–65 °C) resolved the 12 °C Tm gap between the forward
  and reverse anchors.
- **In-house S30 extract** from a GroEL/GroES-overexpressing strain removed the batch-to-batch
  variation and chaperone shortfall of commercial kits: ~2.5× the yield by GFP comparison, and
  pNPO/pNPB/pNPP activity in the CalB positive control that the commercial kit could not detect.
- **Automation.** An Echo 525 acoustic dispenser and automated liquid handlers standardized the
  96/384-well expression–dilution–assay process, with an sfGFP expression control on every plate
  to monitor plate-to-plate variation.

### Test — Round 1

**823 ORFs** across nine library groups, expressed by CFPS and assayed against **three pNP
substrates** at 405 nm: about **2,500 quantitative activity measurements**. Rather than an
arbitrary threshold, I used a **robust Z-score** (median and MAD of the inactive ORF population
on each plate) and required both Z ≥ 3 and a net absorbance above the plate's CalB positive
control. That gave **43 hit candidates (5.2%)**, of which 7 were active on all three substrates
and 3 on two. Confirmation by replicate measurement is in progress.

### Learn — two ways the loop feeds back

1. **Center shifting.** Validated hits join the known-sequence set and shift the reference
   centroid. The contrastive model I developed already maintains class centers by exponential
   moving average, so this update happens inside the learning loop. Because embeddings implicitly
   carry information about cell-free expressibility and activity at 37 °C, the reference point
   converges toward the region that is both functionally similar to the target *and* verifiable
   in this experimental system.
2. **Learned metric.** Round 1's per-substrate activity data become supervised labels for a
   lightweight model — a frozen ESM-C 600M encoder (1,152-d) with trainable attention pooling and
   projection heads (~6M parameters). Critically, the **780 ORFs with no detected activity are
   experimentally demonstrated negatives**, not negatives inferred from sequence distance, and
   they define the negative pairs for metric learning. A fixed "cosine distance to a centroid"
   is replaced by a distance learned from experiments.

### Interpreting hits structurally

**ESMFold** generates predicted structures for the full candidate set without MSAs; **Foldseek**
confirms whether low-identity hits nonetheless share the α/β-hydrolase fold; **FoldDisco** searches
for the discontinuous catalytic motif geometry (Ser–His–Asp triad, oxyanion hole) that separates
active candidates from inactive ones. This both audits what the model learned and supplies
interpretable features for the next round.

---

## Protein language model representations

*Collaborative work, presented at KMB 2025*

Protein language models are usually read out by average pooling across residues. We found that
**overlooked single-token embeddings** can carry global information about the whole protein, and
applied this to bacterial essential-gene prediction, improving performance by up to **17%** over
average pooling.

---

## Research interests

- Representation learning for proteins, and what those representations encode beyond sequence
- Closing the gap between computational prediction and wet-lab outcome
- Cell-free systems and biofoundry automation as a fast, reproducible test bed
- Enzyme discovery and engineering for industrial and environmental applications
