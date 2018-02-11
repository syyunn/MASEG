# MASEG

### On Mathematical Approximation of Syntactic Elements in English Garmmar

#### Abstact

English basically consists of semantic of each word and syntatical concatenations of those. This paper introduces the computational skills to approximate the sysntic functions underylying in English, especially regarding adjectival relation and verb phrase.

This techinique helps us to implement different syntatic intepretation-rules when we embed sentences into numeric vectors so that the information flow in English can be vividly represented in terms of numrical analytics. 

#### Basic Example

**1. adjectival relation**


```python
from gensim import models
```


```python
# First, Load Google Word2Vec
model = models.KeyedVectors.load_word2vec_format('/Users/zachary/Downloads/GoogleNews-vectors-negative300.bin', binary=True)
```


```python
strong = model.word_vec("strong")
affection = model.word_vec("affection")
```


```python
##Assume that "+" is the best linear operator for adjectival descrpiton
#we need to approximate the function that corresponds to the following '+' operation. 

strong_affection = strong + affection 
```


```python
# strong_affection
```


```python
model.most_similar(positive = [strong_affection])
```




    [('affection', 0.8356942534446716),
     ('strong', 0.6486073136329651),
     ('admiration', 0.6161672472953796),
     ('fondness', 0.5639020800590515),
     ('adoration', 0.5518056750297546),
     ('devotion', 0.5325543880462646),
     ('affinity', 0.5254735350608826),
     ('affectionate', 0.5161572098731995),
     ('unwavering', 0.5138853192329407),
     ('emotional_attachment', 0.5132750272750854)]



#### 2. verb phrase

The term "verb phrase" refers to verb + preposition in this paper. For example, the phrases **"compete for"** and **"compete against"** has a differnet meaning, for example, the first one refers to **Earn** food and waters, however, the second one refers to **Fight** against predator or enemies.


```python
compete = model.word_vec("compete")
for_ = model.word_vec("for")
against = model.word_vec("against")

compete_for = compete + for_
compete_against = compete + against


print(model.most_similar(positive= [compete_for], topn = 30)) # Earn Sth
print(model.most_similar(positive= [compete_against], topn= 30)) # fight 
```

    [('compete', 0.9114097952842712), ('competing', 0.7168686985969543), ('competed', 0.6029462218284607), ('competes', 0.5943122506141663), ('Competing', 0.5690189003944397), ('competiting', 0.5617682933807373), ('competition', 0.5574514865875244), ('vie', 0.555402398109436), ('competitive', 0.5256400108337402), ('excel', 0.5188025832176208), ('competitively', 0.517188549041748), ('participate', 0.49898895621299744), ('for', 0.4911567270755768), ('qualify', 0.4883973002433777), ('play', 0.4861796498298645), ('vye', 0.47311726212501526), ('Contestants_vie', 0.4700601100921631), ('competeing', 0.468980997800827), ('meet', 0.46778348088264465), ('perform', 0.4665444791316986), ('towin', 0.46446576714515686), ('defend', 0.461179256439209), ('qualifiy', 0.4500739872455597), ('earn', 0.4472329020500183), ('Rosetta_Inpharmatics_technologies', 0.4462941884994507), ('compettion', 0.4456409811973572), ('succeed', 0.44148489832878113), ('compeition', 0.43257802724838257), ('win', 0.432461678981781), ('showcase', 0.4291384816169739)]
    [('compete', 0.8138852119445801), ('against', 0.6782257556915283), ('competing', 0.6208139657974243), ('defend', 0.5850394368171692), ('competes', 0.5573731660842896), ('competed', 0.5379895567893982), ('againt', 0.5123570561408997), ('beat', 0.5107874870300293), ('play', 0.5106145739555359), ('win', 0.5033345818519592), ('agaisnt', 0.49825844168663025), ('competition', 0.49575841426849365), ('agianst', 0.49424609541893005), ('competiting', 0.49165210127830505), ('Competing', 0.48029109835624695), ('lock_horns', 0.4732126295566559), ('trounce', 0.4729048013687134), ('Beyonce_Irreplaceable_Rihanna_Umbrella', 0.47220245003700256), ('competitive', 0.466503381729126), ('competitively', 0.465944766998291), ('Asics_Invitational', 0.4536173343658447), ('aginst', 0.4514920711517334), ('compettion', 0.4511793851852417), ('outswam', 0.44952863454818726), ('fight', 0.4458543658256531), ('outplay', 0.44318604469299316), ('dominate', 0.4420851171016693), ('outmuscle', 0.44158491492271423), ('aganst', 0.44060447812080383), ('agains', 0.4382237195968628)]

