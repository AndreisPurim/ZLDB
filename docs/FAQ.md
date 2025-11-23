# **ZLDB – Frequently Asked Questions**

Answered by A. Purim.

Last updated on 22/11/2025

## **1. General Questions**

**What is the ZLDB? Why was this dataset created?**

The ZLDB project started with a few questions that all converged. The first came from a conversation with a foreign friend, where I tried to explain why terms such as "zé lensky", "demensky", and "pedinsky" kept appearing on Brazilian social media. This friend thought they were typos, and I explained that no — these were ironic terms Brazilians used to refer to Zelensky.

This led to a larger question: how do Brazilians communicate on social media? For example, are Brazilians more ironic than people in other countries when discussing political events?

To explore this, we needed a topic where both Brazilians and non-Brazilians discuss the same subject, so we could compare discourse quantitatively. The war in Ukraine seemed like a good candidate. We could take one dataset of Brazilian tweets and another of U.S. tweets and compare.

This choice made more sense than an event like COVID, which involves a lot of internal political dynamics, whereas Ukraine involves relatively fewer domestic political variables for both Brazil and the U.S.

However, we quickly realized that no exclusive dataset of Brazilian tweets on the war existed at all (in fact, very few political-topic datasets in Portuguese exist). So after discussing it with some friends, we decided to build one.

Then things escalated: a linguist friend suggested researching indexicality/enregisterment in Brazilian online culture, and I realized there was no dataset for that either.

So we started looking for other under-documented social-media terms in Brazilian Portuguese. And it keeps expanding...

**What research gaps does it aim to fill?**

In short: the absence of Brazilian/Portuguese-language Twitter data about the Russia–Ukraine war, and the broader lack of structured datasets covering under-researched Brazilian social-media expressions and phenomena.

**Who maintains the dataset?**

Mostly me (A. Purim), with occasional help from friends. This is a personal, spare-time project, so some parts may take a while.

**Is the dataset peer-reviewed or published in an academic venue?**

Yes. Check the end of the README for citation instructions.

---

## **2. Ethical & Political Questions**

**Do you (the creator) have opinions on the Russia–Ukraine war?**

Yes (as I assume most people do). However, personal bias should not interfere with my work as a neutral researcher and annotator, which is why I follow written guidelines and check international stance-detection literature.

My personal views are not the basis for the labeling logic. Tweets are annotated based on explicit guidelines.

Of course, biases can still appear, which is why feedback and independent replications are welcome.

**Does this dataset promote any political agenda?** 

No.

**Why collect politically sensitive content?**

Because political discourse is an essential part of linguistic and social-media research. Studying how people talk about public events (especially divisive ones) helps researchers understand:

- how communities construct political identity  
- how irony, sarcasm, and slang evolve  
- how misinformation spreads  
- how different countries frame the same global event  
- how online polarization manifests linguistically  

The aim of ZLDB is descriptive: to observe these phenomena rather than endorse or amplify any viewpoint.

**Are the tweets anonymized or processed in accordance with Twitter/X's TOS? What privacy protections are used?**

Yes. The dataset strictly follows the Twitter/X Developer Policy:

- No raw tweet text is shared.  
- No usernames, profile metadata, or personal information are stored or redistributed.  
- Only tweet IDs, timestamps, stance labels, and non-reversible features (embeddings, hashed tokens) are provided.  
- Anyone using the dataset must "hydrate" tweets through Twitter's API, which automatically respects deletions, suspensions, and user privacy.

The dataset never redistributes raw user content, only numeric IDs and derived features.

**Why does the dataset only include tweet IDs rather than raw text? Why does it include embeddings / hash tokens?**

Because Twitter explicitly forbids the redistribution of raw tweet content in public datasets. Derived features (embeddings, hash tokens) are included because they are non-reversible and legally allowed.

The derived features still allow researchers to use the dataset in a fast manner without having to search the raw text. It was the best compromise we could come up with.

**Is this dataset safe/ethical to use for academic work?**

Yes. It follows the standard ethical model used by many Twitter-based corpora:

- Fully compliant with Twitter/X TOS  
- No personal data  
- Transparent methodology  
- Explicit limitations and disclaimers  
- Focus on linguistic, sociological, and computational research  

This should, in most cases, be enough to satisfy questions of ethical use, although local IRB/ethics rules should always be checked.

---

## **3. Technical Questions**

**What are "hash_tokens" and why do you use them?**

`hash_tokens` are non-reversible hashes of tokens from the tweet text. They enable approximate lexical analysis (e.g., token overlap, vocabulary size, clustering) without exposing raw text or violating TOS.

**How are embeddings generated? Which model is used?**

Embeddings are generated offline using a sentence/Transformer model (e.g., a Portuguese or multilingual encoder). The exact model name and version are documented in the repository and inside `text_info.embedding_model`.

**What is the `text_info` field?**

`text_info` is a derived-text metadata block. It typically includes: `has_text`, `embedding_model`, `embedding_dim`, `embedding` vector, `hash_space`, `hash_tokens`, and `hash_version`.

**Why are embeddings included if raw text is not shared?**

Embeddings allow researchers to run semantic analyses (clustering, similarity, probing) without access to raw text. They are non-reversible in practice and compatible with Twitter/X TOS.

**What features are included beyond stance labels (e.g., irony, toxicity, etc.)?**

Depending on the subset, ZLDB may include labels such as stance, irony/sarcasm, sometimes toxicity/offense, and other experimental tags. The exact schema is documented in the repository.

**How frequently is it updated?**

Updates are irregular and best-effort. This is a spare-time project, so new dumps or labels appear when I have time and new research questions.

---

## **4. Licensing and Terms**

**What license governs the dataset? Is commercial use allowed?**

The code and dataset files in this repository are released under the MIT License. In principle this permits commercial use, but **any use must also comply with Twitter/X TOS**, which may restrict certain kinds of commercial exploitation of tweet data.

**What parts of the dataset are open vs. restricted?**

The ID-level data and derived features (embeddings, hashes, labels) are public under the dataset license and Twitter/X TOS. Any raw text, private admin files, or local scripts used on raw tweets remain private and are not distributed.

**Does this violate Twitter/X's terms?**

No. ZLDB only redistributes IDs and derived, non-reversible features, which is the standard allowed practice. Users must hydrate tweets themselves via Twitter/X-compliant tools.

---

## **5. Safety & Limitations**

**What limitations should researchers be aware of?**

ZLDB is biased because it collects the opinions of people who use Twitter. Moreover, it depends on the keywords used for the query. It is not representative of all Brazilians or all political views.

Any models or analysis trained on ZLDB may inherit topic, stance, and demographic biases present in the data. They should not be used as "ground truth detectors" of ideology or morality.

**Is the dataset balanced (stance, geography, time)? Are political extremists over-represented? Are certain demographic groups underrepresented?**

No. Data should be treated as observational, not balanced by design.

Highly engaged or extreme users are often more vocal and may be over-represented. This does not mean they reflect majority opinion.

Some demographic groups are almost certainly underrepresented. Again: nothing in ZLDB should be interpreted as a full demographic picture of Brazil.

---

## **6. Meta / Community Questions**

**Can the community contribute?**

Yes. Contributions such as bug fixes, analysis scripts, and carefully documented new subsets are welcome. Please open an issue or pull request.

**When will ___ be published? How can I request new features or fixes?**

Open a GitHub issue describing what you need (clarity in the guidelines, new splits, extra metadata, bug fixes). I will address them on a best-effort basis.

**Will there be future expansions (e.g., 2025, 2026, other conflicts)?**

Yes, that is the intention. However, this depends on my schedule and research priorities.
