# Scaling Giants
## Architecture Lessons from Tech's Most Demanding Systems

Systems that serve very large numbers of users don't just have more traffic. They have different engineering problems: tail latency dominates, failure is constant, and correctness has to survive retries. This book studies how specific companies solved those problems, using the papers, engineering posts and incident reports they published, and extracts the decisions and trade-offs a working engineer can reuse.

> **Status: being rewritten.** The first draft (v1, in the Markdown folders below) made claims it did not source, and several of its headline figures were wrong. v2 rebuilds every chapter on primary sources and is written in [YAML Markup Standard v2](scaling_giants_book_index.yaml) so one renderer can produce the web, PDF and ebook editions. Chapters are published one at a time, each with every figure checked against its source. Until a chapter's v2 replacement lands, treat its v1 text as an unverified draft.

---

## Who This Is For

**Primary:** Staff+ engineers and senior individual contributors designing systems that need to scale, or who want to understand why the systems they work on are built the way they are.

**Secondary:** Engineering managers, solutions architects and technical leads who make infrastructure decisions and need to speak credibly about scale trade-offs.

---

## Sourcing Policy

Every figure cites a primary source: a paper, the company's own engineering post or incident report, official documentation, or a regulatory filing. A figure that cannot be traced to one is cut, not rounded or estimated. The planned sources for each chapter are listed in the book index.

---

## v2 Outline

The book index, [`scaling_giants_book_index.yaml`](scaling_giants_book_index.yaml), is the authoritative reading order.

**Part I: Foundations**
1. Foundations of Scale

**Part II: Domain Architectures**

2. Payments: Correctness Under Retries
3. Storage and Durability
4. Data Processing at Google
5. Sharded and Globally Distributed Databases
6. Social Graphs and Caching
7. Messaging and Event Streams
8. Geospatial Marketplaces
9. Content Delivery and the Edge
10. Real-Time Systems and Games

**Part III: Operating at Scale**

11. Failure at Scale
12. AI Training Infrastructure

**Part IV: Synthesis**

13. Patterns Across Domains

Appendices: a glossary, and the sources for each chapter.

---

## v1 Draft (being replaced)

These files remain until their v2 chapters land, then they are removed.

- [Preface](front-matter/preface.md)
- [Chapter 1: Foundations of Scale](part-1-foundations/chapter-01-foundations-of-scale.md)
- [Chapter 2: Financial and Payment Systems](part-2-domain-architectures/chapter-02-financial-payment-systems.md)
- [Chapter 3: Search and Discovery at Scale](part-2-domain-architectures/chapter-03-search-discovery-at-scale.md)
- [Chapter 4: Social and Communication Platforms](part-2-domain-architectures/chapter-04-social-communication-platforms.md)
- [Chapter 5: Content and Media Delivery](part-2-domain-architectures/chapter-05-content-media-delivery.md)
- [Chapter 6: Gaming and Interactive Systems](part-2-domain-architectures/chapter-06-gaming-interactive-systems.md)
- [Chapter 7: Cloud Infrastructure and Storage](part-2-domain-architectures/chapter-07-cloud-infrastructure-storage.md)
- [Chapter 8: Data and Analytics Systems](part-2-domain-architectures/chapter-08-data-analytics-systems.md)
- [Chapter 9: Next-Generation Computing](part-3-next-generation/chapter-09-next-gen-computing.md)
- [Chapter 10: Emerging Architectures](part-3-next-generation/chapter-10-emerging-architectures.md)
- [Chapter 11: Synthesis and Future](synthesis/chapter-11-synthesis-and-future.md)
- Appendices: [A](appendices/a-technology-stack-matrix.md), [B](appendices/b-scaling-metrics-benchmarks.md), [C](appendices/c-open-source-tools.md), [D](appendices/d-glossary.md)

---

## License

Prose content: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)  
Code examples: [MIT](LICENSE)

---

## Author

**Raghav Dinesh** | [github.com/ruwgxo](https://github.com/ruwgxo)

Detection and Security Platform Engineer, building production systems since 2012.
