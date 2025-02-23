# TAADO_Analyses

This repository contains the two analyses conducted using TAADA and reported in an anonymous for now paper. They are as follows

Study 1

Our first study is corpus-based and relies on a large-scale collection of text excerpts which each have associated human judgments of readability. The goal of the study is to assess relationships between the TAADA decoding features and the readability judgments.

Methods
Corpus. To assess the links between morphological elements of texts and text readability, we used the CommonLit Ease of Readability (CLEAR) corpus (Crossley et al., 2022). The corpus consists of 4,724 text excerpts, which comprise around 800,000 words. The corpus was created for the purpose of developing and evaluating different readability formulas. To obtain distinct readability assessments for the text excerpts, teachers were recruited from CommonLit's teacher network. Teachers were asked to review pairs of text samples and judge which excerpt was simpler for students to understand. Following the exclusion of outliers, contributions from 1,116 educators were retained, amounting to 111,347 comparative assessments in total. A Bradley-Terry model (Bradley & Terry, 1952) was used to compute pairwise comparison scores for the teachers’ judgments of text ease to calculate unique readability scores for each excerpt. The final scores reflect the “Easiness” in terms of comprehension for each excerpt in the corpus. 

Statistical Analyses. To predict text reading ease scores found in the CLEAR corpus, we used the decoding indices in TAADA as predictor variables in a linear model. We first ensured that none of the TAADA variables correlated strongly with text length (r > .699) and also calculated bivariate Pearson correlations for all TAADA variables using the cor.test() function in R (R Core Team, 2020) to identify highly collinear features among the TAADA variables. If two or more variables correlated at r > .699, the variable(s) with the lowest correlation with the ease of readability score was removed and the variable with the higher correlation was retained. We also only retained variables that demonstrated at least a small relationship with the ease of readability scores (r > .099).
	We used the CARET package (Kuhn, 2008) in R to develop linear models. Model training and evaluation were performed using a ten-fold cross-validation model using stepwise selection from the leapSeq() function. Estimates of accuracy are reported using the amount of variance explained by the developed models (R2). The model was checked for suppression effects. The relative importance of the indices in each model was calculated using the calc.relimp() function in the relaimpo package (Grömping, 2006) using the lmg metric (Lindeman et al., 1980). lmg takes into account both the direct relationship between the independent and dependent variable (i.e., the bivariate correlation) and the indirect relationship between the independent and dependent variable (i.e., the amount of variance explained when included in a multivariate model).
![image](https://github.com/user-attachments/assets/0489cd2f-4ea2-4abc-ad9b-598c00698b84)

Study 2

Our second study is not corpus-based but rather behavioral and is meant to provide a more fine-grained analysis of decoding. The data comes from younger readers tasked with reading a text aloud. The read alouds were recorded and each word produced by the students was coded as being accurate or inaccurately pronounced (i.e., miscues). Miscues were coded as words where a child made a deletion, omission, mispronunciation, substitution or self-correction when reading. 

The data for this study could not be shared, but the methods and analyses are shareable.

Datasets
The full dataset used in the second study as extracted from three different read aloud studies conducted in the same lab using the same protocols. Across all three studies, there were 296 total participants who produced 653 distinct words comprising 534 distinct lemmas. In total, there were 120,822 observations of students reading a word aloud, on which participants had no miscues for 114,374 observations and had a miscue for 6,475 observations. 

The goal of the first study was to identify behavioral and neuronal weaknesses in children that have late-emerging reading difficulties. There were 77 participants in this dataset, who were between the ages of 6-8 (M = 7.51, SD = 0.32) when data was collected. The sample was 45.45% male, and their reported race was 62.34% White, 31.17% Black/African American, 5.19% more than one race, and 1.30% Native American. Four passages in this study were taken from the Qualitative Reading Inventory (QRI; Caldwell & Leslie, 2000), which tasked participants with reading passages aloud and answering questions related to the passages to measure word identification, fluency, and comprehension. There were two expository and two narrative passages in total, although participants were counterbalanced to read one narrative and one expository passage out of the four. The first narrative passage was about a mouse in a house, which contained 250 words, and the second was about a surprise gift which contained 210 words. The first expository passage contained 76 words and was about the brain and the five senses. The second was about air and contained 85 words.

The goal of the second study was to understand fundamental characteristics of the learner in relation to the text complexity features required for skilled reading comprehension. There were 142 participants in this dataset, who were between the ages of 10-14 (M=11.78, SD = 1.34). The sample was 54.23% male students and the reported races were 76.26% White, 12.95% Black/African American, 2.16% Asian, 5.76% more than one race, and 2.88% preferred not to answer. These two expository passages were experimenter-created and were controlled to be as identical as possible based on cohesion, vocabulary, decoding, and syntax (Spencer et al., 2019). The first expository passage was about deserts, and the second was about toads. Both passages contained 305 words. 

The goal of the third study was to understand the role executive functioning plays across reading comprehension development. There were 77 participants in this dataset who were between the ages of 7-9 (M=8.39, SD = 0.34). The sample was 41.56% male students and reported their race as: 81.82% White, 12.99% Black/African American, 5.20% Asian, 3.90% more than one race, and 2.60% preferred not to answer. These four passages were experimenter-created and controlled to be as identical as possible based on number of words, sentence length, word length, word frequency, word concreteness, reading ease, and grade level (Del Tufo, Earle, & Cutting al., 2019). There were two expository and two narrative passages in total, although participants were counterbalanced to read one narrative and one expository passage out of the four. The first expository passage was about the artic circle, and the second was about hot air balloons. The first narrative passage was about a grasshopper, and the second was about a monkey and a cat. All four passages contained 350 words.

Data compilation. From the ~120,000 words, we removed all function words so that only content words remained (398 unique words and 54,943 observations). From there, each TAADA feature for each unique word was added to a table. Each of the unique words in the table was checked to see if there were any NA values for the TAADA variables. The variables related to weighted probability counts (min, average, and max) for consonant, vowel, and all character counts showed NA values for three words (eye, moonless, and seethrough). These words were removed from the data frame leaving 395 unique words and 54,465 observations. We also looked for TAADA variables that showed high zero counts of over 20% of the data (i.e., no reported value for the word). Five TAADA variables showed high zero counts. All variables were related to neighborhood effects (e.g., number of orthographic and phonographic neighbors along with frequency of phonographic and orthographic neighbors) and were removed. The final table included 395 unique words, 54 decoding variables, and 54,465 observations.
	The final table had a few important considerations. The first is that the data is repeated with each participant providing multiple data points. The second is that the table showed a strong ceiling effect with 51,287 of the observations showing no miscues and 3,178 observations showing miscues. Lastly, the outcome variable in the table was binary (miscue or no miscue). Statistical modeling on the raw data would likely capitalize on the imbalanced classification codes reported in the dataset; thus, we elected to randomly oversample the data prior to analyses. We selected oversampling versus undersampling because research indicates that oversampling does not suffer from overfitting for behavioral data or other performance degrading effects (Vanhoeyveld & Martens, 2018). We oversampled using the Random Over-Sampling Examples (ROSE; Lunardon et al., 2014) package in R so that we had 51,287 observations for both miscues and non-miscues. 

Statistical Analysis. To examine differences in miscued and correctly spoken words based on decoding variables reported in TAADA, we first controlled for multi-collinearity and effect sizes within the data as reported in Study 1 using dummy coded variables for miscued and correctly spoken words. We then scaled the remaining variables and constructed a generalized linear mixed model (GLMM) using the lme4 package in R. A GLMM can include both fixed and random effects along with binomial distributions when developing a classification model (Faraway, 2016). In our GLMM model, the response variable was each spoken word as a binomial response defined as either correct (coded as 0) or miscued (coded as 1). The fixed effects were the decoding features from TAADA that were not highly correlated. Random effects were used quantify variation across participants. We ran two GLMMs. The first was a baseline model that only include random effects. The second was a full model that included random and fixed effects. All models were checked for suppression effects and hand-pruned if suppression effects were noted. An ANOVA comparison was made between the first and second models to examine differences in strength.

