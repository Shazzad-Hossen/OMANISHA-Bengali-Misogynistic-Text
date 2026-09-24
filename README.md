
# OMANISHA: A Benchmark Dataset for Identifying and Categorizing Bengali Misogynistic Text

OMANISHA (Online Misogynistic Annotated Natural-language Instances for Sentiment and Hate Analysis) is a Bengali dataset developed to support the automatic detection of misogynistic discourse in online spaces. Misogynistic content on online platforms has serious psychological, social, and institutional consequences for women, as it contributes to gender inequality, normalizes gender-based violence, and discourages women from participating freely in digital communities. Despite the global significance of Bengali, computational resources for detecting gender-based online abuse in Bengali remain limited. OMANISHA addresses this gap by providing a reliable, publicly accessible dataset for online misogyny detection. 

The dataset consists of 7,017 instances, with each instance assigned to one of four predefined categories.

-	Non-misogynistic: 2,420 samples
-	Stereotype: 1,744 samples
-	Derogation: 1,527 samples
-	Sexual harassment: 1,326 samples

To develop the dataset, we reviewed public online discourse to understand common linguistic patterns, abusive expressions, and contextual features of misogynistic text. Based on these observations, all dataset samples were independently constructed by the authors, ensuring originality, ethical compliance, and suitability for responsible academic research. To avoid copyright, privacy, and platform-related concerns, we ensured that the dataset does not contain any verbatim or directly paraphrased social media comments.

The dataset includes both formal and informal Bengali texts, reflecting real-world online communication patterns. English translations are also provided to enhance cross-lingual accessibility and support comparative NLP research. To ensure annotation reliability, each sample was independently annotated by two native Bengali annotators selected from a pool of four annotators with diverse gender, religious, ethnic and geographical backgrounds. Annotation disagreements were resolved through structured consultation with a third annotator. Annotation quality was evaluated using Cohen’s Kappa (κ = 0.76) and Krippendorff’s Alpha (α = 0.75), indicating substantial inter-annotator agreement. Additionally, pairwise Jaccard Similarity scores among the classes range from 0.12 to 0.21, suggesting clear taxonomic distinction across the defined categories.

The preprocessing pipeline includes duplicate removal, text normalization and coherence checking to ensure data quality and integrity. Unlike binary misogyny detection datasets that simply classify content as misogynistic or non-misogynistic, OMANISHA offers fine-grained category-level annotations, enabling more precise analysis and content moderation. By making this dataset publicly available for research purposes, OMANISHA aims to advance low-resource Bengali NLP, support explainable AI-driven content moderation and encourage further innovation and collaboration within the Bengali NLP community.