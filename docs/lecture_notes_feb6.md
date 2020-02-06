These are lecture notes to accompany the slides that we would have covered in Psyc 408 today, Thursday Feb 6 2020. It is approximately what I would have said during lecture, and only lightly edited.

**Attendance Points Instructions**

In 2-3 sentences, tell me one thing you learned from today's lecture materials that:
1.	surprised you, or
2.	you think will be important to remember going forward,
And why that thing is surprising/important.

Submit via compass: <https://compass2g.illinois.edu/>

Because I didn't get this posted in time for it to be done during today's class time, you have ONE WEEK to complete this assignment (due Thursday, February 13th by 11:59pm).
 

Picking up where we left off on Tuesday...
 
## Population Genetics & Ancestry 
<https://jaimederringer.github.io/psyc408/docs/slides_ancestry.pdf>
 
We had been talking about how ancestry, in the context of a genetic study, is a statistical measure (usually expressed as Principal Components, or PCs) of similarity between the genotypes of different people. People with more similar principal component scores, even going out to the 20th or 100th estimated principal components, have more similar genotypes than would be expected based on chance alone. As new mutations arise in every generation, they may be passed down within families, which means folks who have similar patterns of mutations, even if they are neutral or non-functional, share a more recent common ancestor. Looking at a group of putatively unrelated participants, we can effectively tell who are 3rd cousins versus who are 20th cousins, and everything in between.
 
**Slide 17 of 18: Example**
 
Unfortunately for our ability to figure out "what genes do", this means that genes are passed down within families in a very similar pattern to how culture, or environmental exposures, or resource availability may track within generations, either over time or even within a single generation. For example, suppose it were suddenly decreed that all Icelanders must wear tophats. The policy takes effect on Jan 1. On Jan 2, you collect data from all over the world on tophat-wearing, along with DNA. You would find that the mutations that happen to appear among Icelanders more than among other ancestries are strongly correlated with tophat-wearing. But if you 'controlled for' (Icelandic and other) ancestry by including principal components as covariates in your statistical analysis, those correlations between genetic variants and tophat-wearing would disappear.
 
This slide shows a study that illustrates the same effect with real-world data. This study was interested in identifying genetic variants associated with Multiple Sclerosis (MS). However, the available sample was not a random or representative sample (it never is). Panel A here shows the number of cases (folks with MS, in red text) and controls (folks without MS, in black text) included in the study broken down by each country of origin. As you can see, the numbers aren't similar proportions from each country: some contributed only cases, while others contributed substantially more controls than cases. Panel B shows the plot of the first two principal components for all the participants (1) split by case-control status and (2) color-coded by country of origin. As you can see, (1) the countries differ in terms of their average PCs (participants labeled with the same color tend to cluster together), and (2) the distribution of colors (representing countries) differs between the case and control groups. This sampling scheme has created a confound - or an unintended nuisance correlation - between ancestry and MS case-control status.
 
**Slide 18 of 18: QQ plots**
 
This is one of the common ways we summarize the results of the millions of tests that are done in a genome-wide association study (GWAS, "gee-WAHs"), when we check each available genotyped SNP ("snip") for correlation with a phenotype of interest. When so many tests are done, there will be some very low p-values (how we tend to evaluate statistical significance) by chance alone. To take that into account, we can compare our observed distribution of p-values (the values used to array points - which each of which represents the result of one tested SNP - along the vertical y-axis) to the distribution of p-values that would be expected by chance alone (that's the values used to array points along the horizontal x-axis). The dotted black line running along the diagonal is where we would expect the points to fall if there were no effects (that is, if the observed distribution and the expected distribution were the same). Points falling above the line indicate more SNPs with lower p-values than would be expected by chance alone. The plot to the left, labeled 'No correction', shows the result of the GWAS of MS when the PCs are NOT included as a covariate. That is, it looks like ALL the SNPs have lower p-values than expected by chance, and so we might conclude that ALL the SNPs are associated with MS. This divergence is summarized by the lambda coefficient: here it's 2.5, which is HUGE. Once the top 100 PCs are included as covariates (the results shown in the right-side plot), however, it drops to 1.221 (values closer to 1 are considered less likely to reflect substantial stratification). There are still a lot of SNPs more strongly associated with MS than would be expected by chance alone (MS is heritable and polygenic - many genes, not just one), but there's also some SNPs (densely plotted in that bottom left corner, it's actually MOST of the SNPs) that are unrelated to MS status.
 
## A (very brief) history of eugenics
<https://jaimederringer.github.io/psyc408/docs/slides_eugenics.pdf>
 
**Slide 2: Galton & Eugenics**
 
In 1883, Frances Galton, who is considered the father of modern behavior genetics and happened to be Charles Darwin's cousin, coined the term "eugenics," meaning, from the Greek terms eu- and genos, "good genes." The early proposals for advancing eugenics was through government incentives (essentially, paying) for "eminent" people to marry and have children. Galton defined eminence as being rich (coming from rich families), educated (certainly not universally available), and having an eminent profession (like doctor, judge, scientist - again, not options that were equally available to everyone).
 
**Slide 3: "The inventor of eugenics has a surprisingly good idea about how to cut cake."**
 
The past and present of human behavior genetics is inextricably linked with the history of eugenics, not only because behavior genetics has been used to justify eugenic policies, which have overwhelmingly been abusive and violent, and targeted primarily at racial/ethnic/religious minorities, women, and people with disabilities. The reality is that the men and women who advocated for eugenic policies developed the methods that we still use today, often with the express purpose of producing data and statistics to support their advocacy. We cannot simply stop using their methods – not just within behavior genetics, but across the sciences overall: Karl Pearson, who developed the correlation (Pearson correlation), was Galton's protege (wikipedia's word) and developed the correlation statistic to formally quantify Galton's observation that parents and children tended to be similar on "eminence," which he took as necessarily indicative of biological transmission. We cannot simply erase these men from our history or our science, so we need to acknowledge the bad with the good, and use knowledge of the past to consider how we can do better now and in the future.
 
**Slide 4: Nazi Eugenic Policies**
 
When most people think of eugenics, they think of the Nazis. In the lead up to and during World War II, the Nazis enacted policies ranging from propaganda encouraging folks to be aware of family history of mental or physical illness when deciding who to marry and have children with, to enacting laws forbidding whites from marrying non-whites, making abortion illegal for women deemed to be 'fit' (of good, presumably genetic, quality), registration of disabilities and illnesses leading to the forced surgical sterilization of over 400,000 people. And this is all in addition to the Holocaust, in which 6 million Jews and millions of other people from marginalized groups, including the disabled, the Romani, and people suspected of being gay.

What is less often discussed is that many of these policies, including forced sterilization, were in fact based on existing US policies. And the Nazi versions of the US policies were not necessarily more severe or violent. For example, the US laws forbidding interracial marriage defined "white" much more strictly. Racial and ethnic identification in the US has typically followed "the one-drop rule": one-drop of non-white blood (or, any evidence of non-white heritage) excluded a person from the "white" demographic category.
 
**Slide 5: US Sterilization Programs**
 
The US was the first place in which eugenic sterilization policies were put into place. Around the turn of the 1900s, several states had legislation move increasingly further until in 1907 the first policies were enacted in Indiana. In 1927, the US Supreme Court upheld (8-1) Virginia's eugenic sterilization policy in the case of Buck v Bell. Immediately, similar policies spread quickly across the US.
 
**Slide 6: US Sterilization Programs**
 
Non-eugenic sterilization exists, as well. Therapeutic sterilization typically refers to cases where women with extremely painful periods or uncomfortable or potentially cancerous tumors choose to have those organs removed, or cases where people choose surgical interventions (tubal ligation or vasectomies) to voluntarily, with full informed consent, serve as a form of permanent birth control. Punitive sterilization is typically non-surgical (eg. "chemical castration") and used as a condition of release for repeat sex offenders. Eugenic sterilization, however, is specifically targeted a controlling the reproduction of others, regardless of their consent, with the goal of reducing the rates of mental and physical disabilities in the population. In the US, over the course of the six or so decades that eugenic sterilization policies were in place in the US, over 60,000 people were forcibly sterilized. Overwhelmingly, the people targeted by the state-directed eugenics boards that made such decisions were women or girls, especially those who were poor or black.
 
After World War II and the widespread revelation of the Nazi's atrocities, public opinion of eugenic sterilization declined. But these policies didn't simply disappear – the last eugenic sterilization in the US occurred in Oregon in 1981. 1981. That is not a typo. 1981.
 
This is not ancient history. Many of the victims of these policies are still alive. Follow the link below to watch a 15-minute video, where you'll hear members of these state eugenics boards discussing how they made these decisions, you'll meet a woman who was sterilized by a eugenics board as a child after she became pregnant from a rape. And you'll meet her son, who was born by c-section at the same time that she was surgically sterilized. The state did this to her, North Carolina, has committed $10 million in compensation for victims of its eugenics program. Even if all 7,600 people sterilized by that state were alive and able to claim their share, that comes out to $1,315 per person.
 
**Video Link:**
<https://www.youtube.com/watch?v=Nshj9rCTPdE>
