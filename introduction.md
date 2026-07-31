# Introduction

## Background

SNOMED CT is the world's most comprehensive clinical terminology, used to record, exchange and analyse clinical information across primary care, secondary care and, increasingly, AI-driven clinical tools. Organisations that have not yet adopted SNOMED CT, or that use it only partially, face a migration: moving existing clinical data and workflows off legacy code systems — ICD-9, ICD-10, READ codes, proprietary local codes — onto a SNOMED CT foundation, or extending SNOMED CT use into areas where it is not yet embedded.

A SNOMED CT migration is rarely a single technical task. It touches the data (how existing records are converted and represented), the systems clinicians use (interfaces, workflows, decision support), the organisation's terminology governance, and its relationships with partner organisations and vendors. Each of these dimensions carries its own decisions and risks, and organisations that treat migration as "just a data conversion project" consistently underestimate what is involved.

Migrations are undertaken for a specific mix of reasons — safer clinical decision support, standards-based interoperability, AI readiness, regulatory requirements — and the right approach for one organisation is rarely the right approach for another. What is consistent across successful migrations is that the strategic decisions are made deliberately and early, informed by the experience of organisations that have been through the process before.

## Purpose

The purpose of this guide is to be a practical companion for organisations planning or executing a migration to SNOMED CT. It sets out the strategic decisions that shape a migration, the dimensions a migration plan should address, common strategies for converting data, common pitfalls and how to avoid them, and how to test and verify that a migration has succeeded. Its objective is to help migration teams make deliberate, well-informed decisions rather than defaulting to whatever approach the tooling or a vendor happens to offer.

## Audience

The primary audience of this guide is organisations directly planning or executing a SNOMED CT migration — national release centres (NRCs), hospitals, primary care networks, and health authorities.

We also expect this guide to be useful for EHR and health IT vendors building products and platforms for organisations undertaking these migrations, since a vendor's roadmap and the decisions available to their customers are closely linked.

Although this guide is not targeted at clinicians or other end users of clinical systems, it contains material that may help those coordinating change management with clinical teams during a migration — in particular the discussion of user adoption in [Why Migrate to SNOMED CT](1-why-migrate-to-snomed-ct.md) and of verification in [Testing and Verification](8-testing-and-verification.md).

## Document Overview

This guide covers the full arc of a SNOMED CT migration and is structured in five parts:

**Foundations** sets out why organisations migrate and the landscape they are migrating into.

* [Why Migrate to SNOMED CT](1-why-migrate-to-snomed-ct.md) sets out the eight strategic objectives a migration can support, and why a contained first phase is usually the most realistic starting point.
* [The Architectural Context](<2 the-architectural-context/README.md>) describes the standards and infrastructure — FHIR, openEHR, HL7 V2, terminology servers, and more — that a migration plan must account for.

**Strategic Decisions** covers the two decisions that shape every migration, independent of its size or timeline.

* [Terminology Strategy](3-terminology-strategy.md) explains the reference-to-primary spectrum and the decision of how directly clinicians will engage with SNOMED CT.
* [System and Data Migration](4-system-and-data-migration.md) distinguishes changes to the underlying data from changes to the systems clinicians use, and why conflating the two creates avoidable failure.

**Planning and Execution** turns those decisions into a plan and carries it out.

* [Planning a Migration](5-planning-a-migration.md) sets out the five dimensions a migration plan should cover: scope, functional requirements, risk assessment, timing and approach, and skills and resources.
* [Data Migration Strategies](6-data-migration-strategies.md) describes the strategies available for converting data, and when each is appropriate.
* [Common Challenges](7-common-challenges.md) describes the most common planning and execution mistakes, and how to avoid them.

**Verification and Ongoing Operations** covers how to confirm a migration has succeeded and how to sustain it afterwards.

* [Testing and Verification](8-testing-and-verification.md) sets out the three-tier testing framework used to verify that a migration has succeeded.
* [Managing SNOMED CT Implementation Maturity](9-managing-implementation-maturity.md) describes the ongoing processes mature implementations put in place after go-live.

**Appendices** provide supporting reference material.

* [Case Studies](<10 case-studies/README.md>) illustrates the range of approaches organisations take to migration, from minimum-viable compliance migrations to multi-year phased programmes.
* [Quick Reference](11-quick-reference.md) provides a glossary of the terms used throughout this guide.
