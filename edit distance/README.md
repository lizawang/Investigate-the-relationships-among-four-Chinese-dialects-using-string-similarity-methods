# EDIT DISTANCE
## Tool
- Function *ndiff* from [*difflib*](https://docs.python.org/3/library/difflib.html#)
## Underlying algorithm 
- [Ratcliff/Obershelp pattern recognition](https://en.wikipedia.org/wiki/Gestalt_pattern_matching)<br>
This algorithm tries to find the longest matching pattern/characters.<br>
"The matching characters are defined as the longest common substring plus recursively the number of matching characters in the non-matching regions on both sides of the longest common substring."
- The advantage of this algorithm is that it can find the matching character of the second string that is not aligned with that of the first string in the same position.

## Some Details:
- Punctuation are removed from strings.
  - punc = ["。", "，", "！", "？", "'", "\"", ",", ".", "、", "?", "「", "」"]
- *ndiff* doesn't return the minimum edit steps. Instead it returns double edit steps.
It has no subsitution edits but only edit steps with "-" for deletion, "+" for addition, and " " for matching, as following: <br>
(changing sentence a into sentence b) <br>
a = "这个苹果很酸" <br>
b = "搿只苹果老酸个"

```  
  - 这
  - 个
  + 搿
  + 只
    苹
    果
  - 很
  + 老
    酸
  + 个
```
- The subsitution is self-extracted from the returns of *ndiff* in the function *get_each_edit* which finds the deletions and additions between matching characters and pair them up as susbstituions like in above case "这个" with "搿只", "很" with "老". The subsitutions actually show very good alignments of the two languages.
- The edit distance ratio is acquired by dividing the total length of the two strings with all the deletion and addition edits. <br>
  - For above example, total edits = 3 "-" + 4 "+" = 7, total length of two strings is 6 + 7 = 13, so the edit distance ratio is 7/13 = 0.53846154 which means it needs half of the characters edits to change string a to string b. The largest ratio will be 1.0 when the two strings are totally different and all characters have to be either deleted or added. And the smallest ratio is 0.0 when the two strings are the same and there are no edits.
- To choose to use edit distance ratio instead of similarity ratio is just an intuitive decision considering that the dialects being delt with(especially Cantonese) are more different than similiar to each other.
- The edit distance ratios of 140 sentence pairs of each two languages are randomly sampled 1000 times for plotting.

## Distribution Results(mean, median, standard deviation)
- Cantonese(yue) is most distinct from Mandarin(cmn). Wenzhounese(wen) and Shanghainese(wuu) have very close edit ratio distributions to Mandarin(cmn), with wen showing slightly more small values of ratios in the distribution.
- Comparing among wen, wuu and yue, we can clearly see that wen and wuu are closest to each other(the least edit ratio), but interestingly that wen appears to be less distant from yue than wuu.
- What's also interesting to find is that the distances between wen, wuu and yue are further than their distances to cmn. They are all closer to Mandarin than to each other except that wen and wuu are closer than yue with cmn.
