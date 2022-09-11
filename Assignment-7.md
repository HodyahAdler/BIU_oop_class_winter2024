# Hearst Patterns

## Introduction

In this assignment, we will see an interesting application using regular expressions.


[Hypernymy](https://en.wikipedia.org/wiki/Hyponymy_and_hypernymy) (also called IS-A relation) is a semantic relation between two noun phrases, hypernym and hyponym,
such that the hyponym is a subtype of the hypernym. For example, _cat_ and _dog_ are hyponym of _animal_ because they are types of animals. 
Hypernym relations are hierarchical, so a word can have multiple hypernyms. For example, _dog_ is a hyponym of _animal_, _canine_ and _mammal_.  


Hypernym relations are important and fundamental for many tasks. To illustrate that, let's consider the following question-answering example:

```
Document: 
After eating a delicious meal, Yossi took a dessert made of banana.

Question:
Which fruit did Yossi eat?
```

Knowing that `banana` is a `fruit` can help an automatic system for question answering to answer correctly the answer
`banana` and not `meal`.


However, annotating such relations across all possible pairs of words is not feasible. 
Therefore, many methods have been developed in the last decades in order 
to **automatically** construct a database of hypernym relations from large corpora.


A well-established approach to do so is using lexico-syntactic patterns, often called 
Hearst patterns (as the idea was introduced by Marti Hearst in [this](https://github.com/HodyahAdler/-BIUoop2022summer/blob/main/ass7/C92-2082.pdf) paper). 
For example, given the sentence "_semitic languages_ **such as** _Hebrew_ or _Arabic_ are composed of consonants and voyels", we can infer that both _Hebrew_ and _Arabic_ are semitic languages. Such relations
can be retrieved using a simple regular expression. 



There are two parts in this assignment:
1. Construct a database of hypernym relations
2. Hypernym discovery 


## Part 1: Construct a database of hypernym relations

  

Create a class called `CreateHypernymDatabase` (directly under `src`) with a main method
that receives two arguments: (1) the path to the directory of the corpus 
and (2) the path to the output file.  
Your program will read all the files in the directory, find and aggregate hypernym relations 
that match the Hearst patterns using regular expressions, and save them in a `txt` file.  


Databases of hypernym relations are usually constructed over a **huge** corpus (e.g all Wikipedia articles, 
millions of website contents). As you don't have the computational resources to process such input
in a reasonable run-time, we provide you a subset of articles in English. Please download [here](https://drive.google.com/drive/folders/11aVnX9r-k5iy2GafZd-o5lBBgeNRuFDN?usp=sharing) the compressed
data, unzip it and put the directory wherever you want. Each document is composed 
of a list of paragraphs, a paragraph per line. In each paragraph, words and punctuations are separated by space. 


As mentioned earlier, hypernym relations are semantic relations between two 
[noun phrases](https://en.wikipedia.org/wiki/Noun_phrase) (NP)
which can include multiple words. In the example above, "Hebrew" and "Arabic" are subtypes 
of "semitic languages" and not only "languages". 
Although finding NPs in a text is a problem on its own, we already did that for you and annotated
(automatically) all NPs in the text in the following format. 
 

```
... <np>semitic languages</np> such as <np>Hebrew</np> or <np>Arabic</np> 
are composed of <np>consonants</np> and <np>voyels</np> .
```

It's not a linguistic course, so it's OK if you don't understand how NPs are constructed, just treat them as a span of words.

There are a lot of Hearst patterns, but you'll implement only a partial list, as described below. For brevity, we omit the NP tags from the examples 
but they appear in the data (`{}` means optionally): 


1. `NP {,} such as NP {, NP, ..., {and|or} NP}`.  
In this pattern, the first NP is the hypernym and the NPs after the words "such as" are hyponyms.   
Example: "semitic languages such as Hebrew or Arabic are composed of consonants and voyels"  
semitic language ⟶ Hebrew  
semitic language ⟶ Arabic  

2. `such NP as NP {, NP, ..., {and|or} NP}`   
Here again, the first NP is the hypernym and the NPs after the words "as" are hyponyms.   
Example: "courses taught by such lecturers as Hemi, Arie, and Hodyah are great"   
lecturers ⟶ Hemi  
lecturers ⟶ Arie  
lecturers ⟶ Hodyah  

3. `NP {,} including NP {, NP, ..., {and|or} NP}`    
Here again, the first NP is the hypernym and the NPs after the words "including" are hyponyms. 

4. `NP {,} especially NP {, NP, ..., {and|or} NP}`    
Here again, the first NP is the hypernym and the NPs after the words "especially" are hyponyms.

5. `NP {,} which is {{an example|a kind|a class} of} NP`       
Here, the first NP is the hyponym and the second in a hypernym. 
Example: "Object oriented programming, which is an example of a computer science course" 
You should accept the following: (the "," is optionally)
    - NP {,} which is NP
    - NP {,} which is an example of NP
    - NP {,} which is a kind of NP
    - NP {,} which is a class of NP


 
 
Notice that we don't want to differentiate between "animals ⟶ cat", "animal ⟶ cats" or 
"animal ⟶ cat" as they capture the same relation.
To do so, we should use the canonical form for each NPs, which is also called [lemma](https://en.wikipedia.org/wiki/Lemma_(morphology)). 
 Again, since this is not a linguistic course, we already lemmatized all NPs so that you don't need to find their canonical form. In addition, we also don't want to distinguish between "Animal --> cat" and "animal --> cat". Therefore, you
 need to lower all NPs before applying the regular expressions. 

  
The same relation (e.g animal ⟶ dog) can appear using multiple patterns. For each relation, you need to
count how many times it appears in overall.


At the end of the process, group the hyponyms of the same hypernyms (also called co-hyponyms), 
ignore hypernyms that have less than 3 distinct hyponyms and save the predicted
 relations in a file. If a file exists in the path provided as argument, 
  your program will overwrite it, otherwise, you will create a new file at the given path.
The format of the file should be as follows:

```
hypernym: hyponym1 (x), hyponym2 (x) ...
hypernym: hyponym1 (x), hyponym2 (x) ...
...
```

where (x) corresponds to the number of occurrences of the relations (across all possible patterns) 
in the corpus. 
For each hypernym, you need to sort the list of co-hyponyms according to (x) in a descending order. 
If two hyponyms have the same number of relations, you should sort them alphabetically, as follows:

```
country: united kingdom (10), israel (9), japan (9)
```

Additionally, the hypernyms should also be sorted alphabetically.


Useful tips:

- You're highly recommended to check your regular expressions on an online platform such as [regex101](https://regex101.com/) before applying it on the full corpus.
- Since the corpus is still big, don't debug your code on the full corpus. Instead, you can create your own files and see if your regex catch them.  


## Part 2

Create a class file called `DiscoverHypernym` (directly under `src`) with a main method that will get 2 arguments: (1) the absolute path to the directory of the corpus and (2) a lemma.  
Your program will search all the possible hypernyms of the input lemma and print them to the console as follows.  

```
hypernym1: (x)
hypernym2: (x)
...
```

where (x) corresponds to the number of occurrences of the relations (across all possible patterns) 
in the corpus. 
Like in Part 1, hypernyms need to be sorted in a descending order according to (x).
You can assume that the format of the directory is the same as in Part 1. 


If the input lemma doesn't appear in the corpus, you should print: 
`The lemma doesn't appear in the corpus.`


## What to submit?

You need to submit the two classes with main methods (`CreateHypernymDatabase` and `DiscoverHypernym`)
 as well as all other classes (and packages) that are needed to run these scripts.

Also, you need to submit the files of hypernyms that you obtain in Part 1. 
This file should directly under the folder `ass7` (not under `src`!) 
and should be called `hypernym_db.txt`. 

As in previous assignments, we provide you the [build.xml](https://github.com/HodyahAdler/-BIUoop2022summer/blob/main/ass7/build.xml) with the
with the targets `run1` and `run2` for the two parts. Please follow the submission guidelines and 
submit a zip file with the folder `src` and the file `build.xml` so that we can run the following commands:

```bash
unzip ass7.zip 
ant compile 
ant run1 
ant run2 
```

(with the corresponding arguments for `run1` and `run2`)

**PLEASE DON'T SUBMIT THE CORPUS !!!!!**

## Notes


* As the process is fully automatic, the list of hypernym-hyponym relations will include inevitable noise. 
There are many ways to reduce the noise but it's out of the scope of this assignment, so it's OK if some relations don't make sense.
* Unlike previous assignments, we don't provide you any skeleton of code 
and don't ask you how to structure your classes or how to name them (except the two classes with the main function). 
We assume (and expect!) that you have already acquired sufficient knowledge to decide yourself
how to build your solution.   
* You may loose points if your code doesn't respect the OOP paradigms that we learnt during the course.
* **Be careful to submit in the correct format, your code will be tested automatically, so any deviation from the 
required format will be penalized.**


Good luck and enjoy your last OOP assignment!