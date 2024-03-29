# Positioning-Wenzhounese-in-Chinese-Southern-dialects
Where does Wenzhounese stand lexically? <br>
What makes a dialect dialect and different from Mandarin lexically? <br>
What makes each dialect different from others lexically? <br>

## Data 
- File name is "cmn-yue-wuu-wen-parallel-simplified_final" and uploaded here.
- The data is parallel sentences of Mandarin (cmn), Shanghainese (wuu) and Cantonese (yue) with each 140 sentences and is downloaded from [Tateoba](https://tatoeba.org/en).
- The 140 sentences of Wenzhounese (wen) are translated by myself from the Mandarin (cmn) sentences of Tateoba.
- Data is run over [chinese-converter](https://github.com/zachary822/chinese-converter) to convert chinese traditional characters into their simplified correspondents. (except some of traditional cantonese characters are not converted.)
- All punctuation are removed.
  - punc = ["。", "，", "！", "？", "'", "\"", ",", ".", "、", "?", "「", "」"]

## Methods
Five different methods are chosen and applied. 

## Results
- 1000 random sampling with replacement is employed for the result of every method to acquire a general distribution.
- The distributions are all visualized by using kdeplot from [seaborn](https://seaborn.pydata.org/generated/seaborn.kdeplot.html).
- The results of four methods show consistency (check each method for details).
