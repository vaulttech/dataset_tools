# Tools for the _Customer Reviews Dataset_

The tools here are made to process the dataset available in
https://www.cs.uic.edu/~liub/FBS/sentiment-analysis.html
(specifically, the annotated 5 Products dataset)

#Available tools:

## `generate_training_data.py`

Generates two output files. The first of them contains, for each line
in the file (containing the aspects, the polarity of the aspects, and
the sentence where the aspects appear), only the sentence, with words
separated by space. Review titles are ignored (since they don't
contain aspects). For example, the first three lines of the output of
for the `Canon G3.txt` file would be:

```
i recently purchased the canon powershot g3 and am extremely satisfied with the purchase . 
the camera is very easy to use , in fact on a recent trip this past week i was asked to take a picture of a vacationing elderly group . 
after i took their picture with their camera , they offered to take a picture of us . 
```

The second file generated by `generate_training_data.py` is composed
of BIO tags. B tags indicate that a word is the beginning of an
aspect. I tags indicate that a word is the continuation of an aspect
(i.e., I tags have to always follow B tags). O tags indicate that the
word is not part of any aspect. (see
[this Stack Overflow question](https://stackoverflow.com/questions/17116446/what-do-the-bilou-tags-mean-in-named-entity-recognition)
for a similar tagging scheme)

For example, for those three lines shown above, the result would be:

```
O O O O B-A I-A I-A O O O O O O O O
O O O O O O B-A O O O O O O O O O O O O O O O O O O O O O O O
O O O O O O O O O O O O O O O O O O
```

Because sometimes the aspect name is a little different from whatever
is written in the sentence (e.g., the review may say "useful features",
but the aspect is actually "feature"), the script will check for the
lemma of the words. It will also try to separate words connected by
hyphens (for similar reasons).


