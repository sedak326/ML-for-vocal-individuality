# Vocal Individuality in White-naped Mangabey Males

**Published:** African Primates 19(1): 1-8, 2025
**Authors:** Seda Kavlak, Mireia M. Martin, Foster Poasangma, Mª Teresa Abelló, Andrea Dempsey, Núria Badiella-Giménez
**Institutions:** West African Primate Conservation Action (WAPCA), Ghana; Universitat Oberta de Catalunya, Spain; Parc Zoològic de Barcelona, Spain

Full paper included as `APVol191Kavlaketal.pdf`.

---

This project marks my pivot from animal biology to machine learning. I was presented with a real conservation problem, needed to identify individual animals by their vocalizations, and solved it by extracting acoustic features and training a linear discriminant classifier. It was the first time I understood what ML actually was and how directly it could be applied to problems that matter. That's what made me want to work in this space.

---

## The Problem

The white-naped mangabey (*Cercocebus lunulatus*) is an endangered West African primate. WAPCA breeds individuals in captivity and releases them into the wild to reinforce shrinking wild populations. Once an animal is in the forest, recapturing it to check on it is invasive and stressful. Passive Acoustic Monitoring (PAM) is the non-invasive alternative, placing audio recorders in the habitat to detect vocalizations. But species-level detection isn't enough. To know whether a specific released individual is surviving and integrating, you need to identify it by voice. That requires a classifier that can tell individuals apart from their calls alone, and first requires knowing whether the signal even exists. No one had tested this for *C. lunulatus*.

---

## Data and Feature Extraction

We recorded the "wahoo" alarm calls of three adult male white-naped mangabeys at Accra Zoo. From each recording we extracted 10 acoustic features using Praat: duration of the "wa" and "hoo" syllables, dominant frequency, fundamental frequency, and the first four formants of the full call. These hand-crafted features form the feature vector fed into the classifier.

---

## Classification

We trained a **Linear Discriminant Analysis (LDA)** classifier on the feature vectors. LDA finds the linear combinations of features that maximize between-class variance relative to within-class variance, producing a lower-dimensional space in which classes are maximally separated. Each recording is then assigned to the nearest class centroid in that space.

To evaluate generalization we used **leave-one-out cross validation**, where each sample is classified by a model trained on all remaining samples. This is appropriate for small datasets where a held-out test split would be too small to be meaningful.

**Results:**
- 7 of 10 acoustic features showed statistically significant differences between individuals
- Training accuracy: 59%
- Cross-validated accuracy: 76%

This is the first documented evidence of vocal individuality in *C. lunulatus* males.

---

## Limitations and Next Steps

The classifier was trained on three individuals and 14 recordings per individual, a very small dataset. The lower accuracy compared to similar studies (blue monkeys: 100%, baboons: 72%) is likely a combination of small sample size and the known bias of PRAAT's formant tracker toward human vocal tract geometry rather than mangabey anatomy. Better-tuned feature extraction would likely improve separation.

The natural next step is replacing hand-crafted acoustic features with learned representations. Audio classification models trained directly on spectrograms, or pretrained audio encoders fine-tuned on primate vocalizations, would not depend on manual feature engineering and could scale to larger populations. The signal for individual identification is there. The bottleneck is data.

---

## Note

Sadly, I don't have access to my analysis code anymore. However, feature extraction was done manually in Praat and classification in SPSS.
