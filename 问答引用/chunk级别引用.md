# RAG文档中chunk级别的引用


## 要点
- 首先，介绍任务：包括输入chunk的结构，以及输出答案和引用的格式
- 其次，通过example,让LLM学习认识这种问答模式
- 最后，给出真实数据输入的格式

[LongCite](https://github.com/THUDM/LongCite)
## prompt案例：
```markdown
Your task is to add citations to the existing answer. Specifically, when a factual statement S in the answer uses information from context snippets l1, l2, ..., ln, please add citations by appending these snippet numbers to S in the format "<statement>{S}<cite>[{l1}][{l2}]...[{ln}]</cite><statement>". For other sentences such as such as introductory sentences, summarization sentences, reasoning, and inference, you still need to append "<cite></cite>" to them to indicate they need no citations.  Except for adding citations, do not change the orginal content and format of the existing answer.

Here is an example:

[Contexts Start]
Snippet [1]
appears to be a major indicator of its probability for hosting a planet. Previous studies, e.g.,, showed that main-sequence (MS) stars that host giant planets are metal-rich. This finding is supported by the large exoplanet search surveys around MS stars reporting a connection between planet frequency and metallicity, and a survey of 160 metal-poor main-sequence stars finding no evidence for Jovian planets.\n\nUntil now, only very few planets have been detected around stars with metallicities as low as [Fe/H]= $-1$, i.e. 10% of the sun’s metallicity. The detection of PS

Snippet [2]
the star. This star is classified as a red HB (RHB) star (Fig. 1) and its metal content is [Fe/H]$_\\mathrm{mean}=-2.09$, i.e. about 1% that of the Sun. So far, is not known as a binary system. Detailed stellar parameters can be found in Supporting Online Material, Section [text1].\n\nPrevious radial velocity (RV) measurements of showed a systematic velocity of about 300 $\\mathrm{km\\,s}^{-1}$ with respect to the Sun, indicating that the star belongs to the stellar halo. Indeed, the star

Snippet [3]
^{-1}$\n$m_{2} sin{i}$    1.25 $\\pm$ 0.05     M$_{\\mathrm{Jup}}$  \n$a$               0.116 $\\pm$ 0.01    AU                  \n\n\nBecause a large number of known exoplanets have orbital semi-major axes between 0.01 and 0.06 AU, the distance between the periastron and the star itself is not unusual. The non-circular orbit ($e=$0.25), however, is not expected for a close-in giant planet around a post RGB star.\n\nIn the case of,

Snippet [4]
in the next giant phase. b could be a planet that is just about to be engulfed by its star.\n\n, with a mean metallicity estimate of [Fe/H]=-2.1, is far more metal-poor than any previously known exoplanet hosting star (Fig. 3). For the existing theories of hot giant planet formation, metallicity is an important parameter: in particular, it is fundamental for the core-accretion planet formation model. It might be that initially, in the planet formation phase, had a higher metallicity, and that during its subsequent evolution, it lost its heavier elements. For example, during the

Snippet [5]
arent magnitudes have been converted to absolute magnitudes by considering the distance modulus and extinction given by. The gap separating the blue and red Horizontal Branch (HB) is due to RR Lyrae instability strip. The CMD location of implies that it is a core He-burning star, located a the blue edge of the RHB. Further candidates for post RGB stars hosting planets/brown dwarf, V391 Peg, HW Vir and HD 149382 are displayed as crosses.\n\nSupporting online material\n\nThis supplementary online material is part of the article with the title ”A Giant Planet Around a Metal-poor Star of Extragal
[Context End]

[Question]
How does the metallicity of PSR B1620 b, at around 1% of the Sun's, compare to other known exoplanet host stars?

[Existing Answer Start]
Based on the document, the metallicity of PSR B1620 b is very low compared to other known exoplanet host stars:

- PSR B1620 b has a metallicity of [Fe/H]=-2.09, which is about 1% of the Sun's metallicity.

- This makes it far more metal-poor than any previously known exoplanet hosting star, as stated: "with a mean metallicity estimate of [Fe/H]=-2.1, is far more metal-poor than any previously known exoplanet hosting star".

- The document also states that previous surveys of 160 metal-poor main-sequence stars found no evidence for Jovian planets, and very few planets have been detected around stars with metallicities as low as [Fe/H]= -1.

So in summary, PSR B1620 b's metallicity of just 1% of the Sun's is exceptionally low compared to other stars known to host exoplanets. This makes the discovery of its exoplanet very noteworthy in the context of planet formation theories that depend on metallicity.
[Existing Answer End]

[Answer with Citations]
<statement>Based on the document, the metallicity of PSR B1620 b is very low compared to other known exoplanet host stars:<cite></cite></statement>

<statement>- PSR B1620 b has a metallicity of [Fe/H]=-2.09, which is about 1% of the Sun's metallicity.<cite>[2]</cite></statement>

<statement>- This makes it far more metal-poor than any previously known exoplanet hosting star, as stated: "with a mean metallicity estimate of [Fe/H]=-2.1, is far more metal-poor than any previously known exoplanet hosting star".<cite>[4]</cite></statement>

<statement>- The document also states that previous surveys of 160 metal-poor main-sequence stars found no evidence for Jovian planets, and very few planets have been detected around stars with metallicities as low as [Fe/H]= -1.<cite>[1]</cite></statement>

<statement>So in summary, PSR B1620 b's metallicity of just 1% of the Sun's is exceptionally low compared to other stars known to host exoplanets. This makes the discovery of its exoplanet very noteworthy in the context of planet formation theories that depend on metallicity.<cite></cite></statement>


Now get ready to add citations for the following test case. 

[Contexts Start]
<<context>>
[Context End]

[Question]
<<question>>

[Existing Answer Start]
<<answer>>
[Existing Answer End]

[Answer with Citations]
```
