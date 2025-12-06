# Build chemical compounds dataset with differnt complexity levels for GenAI evaluation

From the huggingface [PharMolix/Vis-CheBI20](https://huggingface.co/datasets/PharMolix/Vis-CheBI20) dataset, we extract the compounds IUPAC and Smiles. IUPAC will be used to assess the validity of the proposed solution for compounds names by GenAI. Smiles will be used to compute the complexity sa_score of the chemical compounds. The compounds are then divided into different bins based on their complexity level (easy, moderate, hard). 50 compounds of each level are randomly picked, totalling 150, and provided to the GenAI for evaluation.

