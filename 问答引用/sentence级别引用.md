# RAG问答句子级别的引用

## 要点
- 首先，介绍任务：包括输入chunk的结构，以及输出答案和引用的格式
- 其次，通过example,让LLM学习认识这种问答模式
- 最后，给出真实数据输入的格式

[LongCite](https://github.com/THUDM/LongCite)
## prompt案例
```markdown
You will receive a passage and a factual statement. Your task is to identify the parts in the passage (i.e., chunks <C{s_1}>-<C{e_1}>, <C{s_2}>-<C{e_2}>, ..., <C{s_n}>-<C{e_n}>) that support some key points of the statement, and output the chunk number in the format:
'''
[s_1-e_1]
[s_2-e_2]
...
[s_n-e_n]
'''
If the passage contains no key information relevant to the statement, you must output "No relevant information".

Here are some examples:

[Passage Start]
<C0>In the last two decades, several hundred planets have been detected beyond our Solar-system. <C1>Most of these extra-solar planets orbit sun-like stars. <C2>A small number have been detected around stars that are in their late evolutionary state, such as Red Giant Branch (RGB) stars and pulsars. <C3>The phase directly after the RGB stage, the Horizontal Branch (HB), however, is still unexplored; therefore, there is no empirical evidence for whether close-in planets, i.e., those with semi-major axes less than 0.1 AU, survive the giant phase of their host stars. <C4>Besides its evolutionary stage, a star’s chemical composition appears to be a major indicator of its probability for hosting a planet. <C5>Previous studies, e.g.,, showed that main-sequence (MS) stars that host giant planets are metal-rich. <C6>This finding is supported by the large exoplanet search surveys around MS stars reporting a connection between planet frequency and metallicity, and a survey of 160 metal-poor main-sequence stars finding no evidence for Jovian planets. <C7>Until now, only very few planets have been detected around stars with metallicities as low as [Fe/H]= $-1$, i.e. 10% of the sun’s metallicity. <C8>The detection of PSR B1620 b, a Jovian planet orbiting a pulsar in the core of the metal-poor globular cluster M4 ([Fe/H]=$-1.2$), suggests, however, that planets may form around metal-poor stars, although the formation mechanism of this particular planet might be linked to the dense cluster environment.
[Passage End]

[Statement]
The document also states that previous surveys of 160 metal-poor main-sequence stars found no evidence for Jovian planets, and very few planets have been detected around stars with metallicities as low as [Fe/H]= -1.

[Output]
[6-7]

[Passage Start]
<C0>而三位眼睛好的行人往往是排成一行走,你走你的,我走我的,还方便聊天,碰到石头水沟时大家各自知道怎么避开。<C1>他们也有一列走的时候,那时他们走的路一定是最通畅的。<C2>一位真正懂炒股的人通常不愿别人跟着买,因为你可以跟我买,但我要卖的时候你不知道,结果可能害了你。<C3>如果卖股票时还要记着通知你,心理负担多大。<C4>亏的话怎么办？<C5>朋友,下点功夫,研究股票的运动规律,学着选择买点和卖点。<C6>想跟朋友买卖不要紧,掂掂他是什么材料。<C7>喜欢你跟着的通常本身是瞎子,瞎子喜欢带路的。<C8>(我博士不喜欢有人跟的。<C9>我说点什么以,也是为了想说明一个问题) 家训:9、该卖股票的时候,要当机立断,千万别迟疑！ <C10>我在1994年11月2日的炒股日记上有这样一句话:股数2千,进价17.25,升到23.50,没有在21.50卖出,今跌到16.25,蠢啊蠢！<C11>！<C12>！<C13>痛啊痛！<C14>！<C15>！<C16>这是四年前的记录,我已记不清当时的具体情况,从上面的几句话,我知道自己将卖点定在21.50,当股票以23.50跌到21.50的时候,不知什么鬼原因使我迟疑,没有即时采取行动。<C17>在11月2日的时候,股票跌到16.25。<C18>我原保证8000元的利润,现倒亏2000元。<C19>我痛呼蠢啊蠢。<C20>股票波动从来花样百出,它在跌的时候,总会不时给你个小反弹,给你一线希望,让你觉得跌势已开始转头。<C21>股票重新下跌,你原来的希望破灭,准备割肉放弃时,它又来个小反弹,重新把你拴住。<C22>开始小小的损失,经过几个这样的来回,变成了大损失。<C23>这就是已学会\"止损\"的股友还会亏大钱的原因。
[Passage End]

[Statement]
6. 该卖的时候就果断卖出,不要迟疑。

[Output]
[9-9]

[Passage Start]
<C0>Cooloola Tramway\nThe Cooloola Tramway is a heritage-listed tramway at Great Sandy National Park, Cooloola Recreation Area, Cooloola, Gympie Region, Queensland, Australia. <C1>In the 1870s it was known as the Kaloola Railway. <C2>It is also known as Cooloola Railway, SEQ-5N 22, Pettigrew's Railway, and Pettigrew's Tramway. <C3>It was added to the Queensland Heritage Register on 12 July 2013.\n\n<C4>History \n\nWilliam Pettigrew's Cooloola timber operation began in the 1860s with the extraction of timber from Woolann (the area around Lake Poona). <C5>Bullock teams were used to drag Kauri pine logs to the mouth of Seary's Creek. <C6>The sandy nature of the terrain and lack of feed for horses and bullocks made traditional forms of timber transport unfeasible and Pettigrew had to find a solution to access the rich timber of inland Cooloola. <C7>The answer was the construction of a tramway: Cooloola Tramway opening in October 1873 as Queensland's first major private railway.\n\n<C8>Of all Queensland's natural resources \"timber was the most visible and abundant to the first Europeans\". <C9>Early European accounts of Queensland frequently refer to the extensive stands of timber which lined the coast and river banks. <C10>In south-east Queensland the dominant timber species were softwoods such as Hoop (Araucaria cunninghamii) and Kauri pine (Agathis robusta). <C11>When Moreton Bay was opened up to free settlement in 1842 the colony did not have a sawmill and logged timber was either pit sawn and used locally, or sent south for milling and/or export.\n\n<C12>The timber industry played a vital role in the economic development of Queensland and William Pettigrew was instrumental in this process. <C13>He was born in Ayrshire, Scotland, in 1825 and came to Moreton Bay in 1849 as one of Dr John Dunmore Lang's immigrants on board the.\n\n<C14>Pettigrew continued to seek out timber resources which could be milled at Dundathu. <C15>In September 1863, he set off in the paddle steamer Gneering to search for stands of timber that were reported to exist in the Noosa area. <C16>On his return Pettigrew concluded that the timber was disappointing and inaccessible. <C17>However, others did not agree and by the end of 1863, timber-getters were operating in the lower Noosa area. <C18>Pettigrew turned his attention to the north, and in late June 1865 Pettigrew landed at the head of Tin Can Bay to examine the area further.\n\n<C19>His discovery of Kauri pine in the Woolann area of north Cooloola provided the main source of timber for the Dundathu Sawmill. <C20>By 1865, Pettigrew's men were using bullock teams to drag Kauri pine logs from Woolann (the area around Lake Poona). <C21>Early timber-getters are recorded as using a corduroy crossing of tea-tree branches and saplings to cross the tidal flats in the northern Cooloola area. <C22>Pettigrew's men dragged the logs to the mouth of Seary's Creek, tied them into large rafts and towed them through the Tin Can Bay Inlet, Great Sandy Strait and up the Mary River. <C23>Tugs were then used to haul the rafts of timber to Dundathu.\n\n<C24>The sandy nature of the terrain and lack of feed for horses and bullocks made the use of draught animals for transport very difficult. <C25>Pettigrew needed to develop a more expedient alternative. <C26>In July 1865 Pettigrew noted in his diary that  of railway, the majority of which would cross flat, \"barren\" sandy country, would enable the timber to be taken out of inland Cooloola to Tin Can Bay. <C27>Pettigrew had previously written to Arthur Macalister-the Minister for Lands and Works-about a railway between his operations on the Maroochy and Mooloolah rivers, and was told that the government would not fund railways, and therefore they must be private.
[Passage End]

[Statement]
Based on the doc, before they built the Cooloola Tramway, William Pettigrew and William Sim used bullock teams to drag Kauri pine logs from Woolann (the area around Lake Poona) to the mouth of Seary's Creek.

[Output]
[4-5][7-7]

Now get ready to process the following test case.

[Passage Start]
<<context>>
[Passage End]

[Statement]
<<statement>>

[Output]
```