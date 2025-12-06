# Build chemical compounds dataset with differnt complexity levels for GenAI evaluation

Using PharMolix/Vis-CheBI20 dataset, chemical compounds Smiles and images are compiled. Using sa_score, the compounds are classified into three complexity levels (easy, moderate, hard). 50 of each level are sampled, and presented to 3 GenAI bots (Gemini, GPT, and Grok). The prediction is evaluated with a score and a diagnosis.

[Notebook](https://colab.research.google.com/drive/1ZnmmPhU5PPsADRccGiB674qY5GISpcAy?usp=sharing)
