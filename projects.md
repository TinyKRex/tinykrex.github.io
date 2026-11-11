---
title: Projects
layout: default
---

# Projects

## MetaForge — Deep Learning-Based Discovery of Moonlighting Enzymes
*IDEA-B Synthetic Biology Competition, MSIT / Korea Synthetic Biology Council · Mar. – Oct. 2026*
*Student team of 4, with an advising researcher and professor · my role: candidate selection and validation design*

Korea's first national synthetic biology competition drew 104 teams from 37 institutions; ours was
one of the **15 graduate-division teams** that reached the final, and the project was funded as a
commissioned research project at KRIBB.

The premise had to be justified first: a literature and database review showed that multifunctional
proteins are heavily over-represented among proteins linked to drug side effects, which is what
made the single-function assumption behind conventional enzyme discovery worth attacking.

Then the work had to fit an eight-month budget. We collected 14 enzyme–substrate reactions from
BRENDA, UniProt and prior literature, then ran control experiments to drop every combination where
the biosensor cross-detected the substrate itself or lacked sensitivity. That removed half of the
initial candidates, but the remaining **7 reaction systems** let us screen **380 metagenomic
candidates against 7 substrates under 4 reaction conditions, roughly 10,000 conditions, in three
days**. Deciding what to discard early was what made the schedule possible.

## MAKEAT — AI Diet-Tracking App
*K-Software Empowerment BootCamp (640 h), Sungkyunkwan University · 2022 – 2023*
*Excellence Award, healthcare track*

A mobile app that logs meals automatically by classifying photographs of food. I handled the
database, and volunteered for the Android/Flutter development role when no one else wanted it,
learning the stack during the project.

Individual projects in the same program: an oral medication image classifier, and an analysis of
COVID-19 case data.

## LLM agents for my own research workflow
*Personal projects, 2025 – present · repositories private*

The parts of research that repeat are also the parts where inconsistency does the most damage, so
I have been moving them into agents that run the same way every time.

- **Paper agent.** Turns an English paper PDF into a Korean reading copy and a summary deck, using
  a fixed glossary so that terms stay consistent across papers.
- **Meeting minutes.** Converts a recording into structured minutes, which keeps a record of
  decisions that would otherwise live in someone's notebook.
- **Lab notebook assistant.** Expands a short experimental plan into a full record against a fixed
  template — the same standardization problem as the screening workflow, one level up.
- **Job-posting digest.** Collects postings from several sources on a daily schedule, filters them
  against a written set of criteria, and mails a report. It runs unattended in CI.

These repositories are private because they hold personal material, but I am happy to walk through
the code and the agent design in an interview.
