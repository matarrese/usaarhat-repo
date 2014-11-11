
**How to tokenize text with Moses toolkit?**

```
MOSES_SCRIPT=/home/expert/mosesdecoder/scripts

echo """„Frau Präsidentin! Ist meine Stimme mitgezählt worden?"""
echo """„Frau Präsidentin! Ist meine Stimme mitgezählt worden?""" | perl ${MOSES_SCRIPT}/tokenizer/tokenizer.perl -l de

echo """„Frau Präsidentin! Ist meine Stimme mitgezählt worden?""" > test.in
cat test.in | perl ${MOSES_SCRIPT}/tokenizer/tokenizer.perl -l de > test.out
cat test.out
```

**How to TrueCase text with Moses toolkit**

```
echo "Barack Obama is the president of the United States of America .
Obama lives in the White House ,
The United States of America is also call USA .
USA is an acronym .
Also , the united states would like to be capitalized ." > test.tok.en

perl ${MOSES_SCRIPT}/recaser/train-truecaser.perl --model truecase-model.en --corpus test.tok.en
perl ${MOSES_SCRIPT}/recaser/truecase.perl --model truecase-model.en < test.tok.en > test.tok.truecase.en

cat test.tok.truecase.en
```

**How to clean corpus by length with Moses toolkit?**

```
MOSES_SCRIPT=/home/expert/mosesdecoder/scripts

echo "Miss President, Is my voice been counted?" > test.en
echo "This is too short." >> test.en
echo "„Frau Präsidentin! Ist meine Stimme mitgezählt worden?" > test.de
echo "Das ist zu kurz." >> test.de

cat test.en
cat test.de

cat test.de | perl ${MOSES_SCRIPT}/tokenizer/tokenizer.perl -l de > test-tok.de
cat test.en | perl ${MOSES_SCRIPT}/tokenizer/tokenizer.perl -l en > test-tok.en

wc -l *

perl ${MOSES_SCRIPT}/training/clean-corpus-n.perl test-tok en de test-clean 6 10
cat test-clean.en
cat test-clean.de

perl ${MOSES_SCRIPT}/training/clean-corpus-n.perl test-tok en de test-clean 1 6
cat test-clean.en
cat test-clean.de
```