---
title: Generating and Plotting Word Frequencies in Subtitle Files
date: 2020-09-10

# Put any other Academic metadata here...
---

# Generating and Plotting Word Frequencies in Subtitle Files


```python
from IPython.display import Image
Image(width=600, filename='/Users/gsaxton/Dropbox/screenshots/rosariotijeras.jpg') 
```




![jpeg](./Word%20Frequencies%20with%20Rosario%20Tijeras_2_0.jpeg)



# Overview

This tutorial covers a variety of word-based analyses using Python PANDAS. Specifically, we'll generate a dataset with word frequencies from a text corpus, plot those frequencies, and see how those frequencies compare to other collections of texts. Along the way, we'll cover reading in and parsing text files, creating word frequency datasets, plotting bar graphs and word clouds, and playing with Python *sets* to compare groups of objects, among other things. 

As you will quickly see, as a break from the typical organization datasets I'm using, in this tutorial I'm using text derived from subtitle files I downloaded from Netflix. I've been watching a Mexican TV show called *Rosario Tijeras*, and to understand it I really need the Spanish subtitles. This tutorial is based on the *.srt* (subtitle) files I downloaded from the first 10 episodes of Rosario Tijeras. If you're interested in following along, to download the .srt files I used the method contained in this link: http://www.nihongonobaka.com/extracting-subtitles-from-netflix/

I hope you enjoy this tutorial. If you know any Spanish, you may see some surprising vocabulary here. :)

#### Sample .srt file
*srt* files generally follow a standard three-block format: 1) a line with an integer (starting with 1 and increasing in increments of 1 with each block), 2) a span of time, and 3) the dialogue. Here is a snapshot from the Episode 1's *srt* file. 


```python
from IPython.display import Image
Image(width=250, filename='/Users/gsaxton/Dropbox/screenshots/srt.png') 
```




![png](./Word%20Frequencies%20with%20Rosario%20Tijeras_5_0.png)



# Import packages and set viewing options

First, we will import several necessary Python packages and set some options for viewing the data. We will be using the <a href="http://pandas.pydata.org/">Python Data Analysis Library,</a> or <i>PANDAS</i>, extensively for our data manipulations.


```python
import numpy as np
import pandas as pd
from pandas import DataFrame
from pandas import Series
```


```python
# http://pandas.pydata.org/pandas-docs/stable/options.html
pd.set_option('display.max_columns', None)
# http://pandas.pydata.org/pandas-docs/stable/options.html
pd.set_option('display.max_colwidth', 250)
```


```python
pd.__version__
```




    '0.21.0'



I'm using version 0.21.0 of PANDAS (and Python 3.6)

We'll be producing some figures at the end of this tutorial so we need to import various graphing capabilities. The default Matplotlib library is solid. 


```python
import matplotlib
print(matplotlib.__version__)
```

    2.1.0



```python
from pylab import*
```

One of the great innovations of ipython notebook is the ability to see output and graphics "inline," that is, on the same page and immediately below each line of code. To enable this feature for graphics we run the following line.


```python
%matplotlib inline  
```

We will be using <i>Seaborn</i> to help pretty up the default Matplotlib graphics. Seaborn does not come installed with Anaconda Python so you will have to open up a terminal and run <i>pip install seaborn</i>.


```python
import seaborn as sns
print(sns.__version__)
```

    0.8.1


<br>The following line will set the default plots to be bigger.


```python
plt.rcParams['figure.figsize'] = (15, 5)
```

# Create DataFrame with Subtitle File Names, Word Counts, and Subtitle Text

##### Set working directory


```python
cd '/Users/gsaxton/Dropbox/RosarioTijeras'
```

    /Users/gsaxton/Dropbox/RosarioTijeras


<br>List subtitle files in folder -- you can see there are 10 files here. 


```python
ls
```

    Rosario.Tijeras.S01E01.WEBRip.Netflix.srt
    Rosario.Tijeras.S01E02.WEBRip.Netflix.srt
    Rosario.Tijeras.S01E03.WEBRip.Netflix.srt
    Rosario.Tijeras.S01E04.WEBRip.Netflix.srt
    Rosario.Tijeras.S01E05.WEBRip.Netflix.srt
    Rosario.Tijeras.S01E06.WEBRip.Netflix.srt
    Rosario.Tijeras.S01E07.WEBRip.Netflix.srt
    Rosario.Tijeras.S01E08.WEBRip.Netflix.srt
    Rosario.Tijeras.S01E09.WEBRip.Netflix.srt
    Rosario.Tijeras.S01E10.WEBRip.Netflix.srt


#### Create list of all 10 *.srt* files and print out 


```python
import os
import re
indir = '/Users/gsaxton/Dropbox/RosarioTijeras'
```

In the next line of code we are using a Python *list comprehension*. This creates a Python *list* from all the files ending with '.srt' that are located in our *indir* directory.


```python
txt_files = [file for file in os.listdir(indir) if file.endswith('.srt')]
print("# of *.txt files in directory:",len(txt_files), '\n')
print('List of *.txt filenames (first 10 only):', txt_files[:], '\n')
```

    # of *.txt files in directory: 10 
    
    List of *.txt filenames (first 10 only): ['Rosario.Tijeras.S01E10.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E03.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E05.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E08.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E06.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E07.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E04.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E09.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E02.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E01.WEBRip.Netflix.srt'] 
    


### Create empty dataframe (dataset) for subtitle database
We are going to create a dataset with 10 rows -- one per subtitle file. This next block of code sets up the empty dataframe. 


```python
columns = ['filename', 'number_words', 'content']
df = pd.DataFrame(data=np.zeros((0,len(columns))), columns=columns)
print('# of columns:', len(df.columns))
print('# of observations:', len(df))
df.head()
```

    # of columns: 3
    # of observations: 0





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>filename</th>
      <th>number_words</th>
      <th>content</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



#### Use list of filenames as first ID column in dataframe then print out dataframe
PANDAS convention, like *R*, is to refer to a dataset as a 'dataframe', hence the conventional use of *df* as the name of the dataset. In this next block we are filling the empty values of *df*'s 'filename' column with the values in our previously generated Python list *txt_files*.


```python
df['filename'] = txt_files
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>filename</th>
      <th>number_words</th>
      <th>content</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rosario.Tijeras.S01E10.WEBRip.Netflix.srt</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Rosario.Tijeras.S01E03.WEBRip.Netflix.srt</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Rosario.Tijeras.S01E05.WEBRip.Netflix.srt</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rosario.Tijeras.S01E08.WEBRip.Netflix.srt</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rosario.Tijeras.S01E06.WEBRip.Netflix.srt</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rosario.Tijeras.S01E07.WEBRip.Netflix.srt</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Rosario.Tijeras.S01E04.WEBRip.Netflix.srt</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Rosario.Tijeras.S01E09.WEBRip.Netflix.srt</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Rosario.Tijeras.S01E02.WEBRip.Netflix.srt</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Rosario.Tijeras.S01E01.WEBRip.Netflix.srt</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



#### Create list of punctuation to remove from text
In order to generate proper word counts, we need to remove punctuation. We can get most of the punctuation marks from Python's *string* package. 


```python
from string import punctuation
print(punctuation)
```

    !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~


<br>We just need to copy the above output and then add '¡¿' to the end and we'll be good to go.


```python
punctuation = '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~¡¿'
print(punctuation)
```

    !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~¡¿


### Loop over each row of dataset, open subtitle file that is associated with *filename* column, add values for *number of words* and combined subtitle *content*, and clean that content.

The is our most difficult part of our code. I won't go over everything but I have added some annotations to the code where appropriate. The basic steps are that we are first reading in each file in our *indir* directory and applying some *Python-fu* to it to strip out the dialogue from the *str* files. That part is fairly technical, so I'll just say that we are removing the non-dialogue that is found in square brackets, such *[tema musical]* or *[bocinazos]*, removing punctuation, and a few other transformations. This is all done in a temporary dataframe called *dft*. Once we have the content in the format we're happy with, we then match file with the relevant row in our dataframe *df*, and update *df* with that subtitle file's content and word count.


```python
from os import system
import subprocess
from itertools import groupby
import re
pattern = r'\[.*?\]'
#re.sub(pattern, '', s)

from collections import namedtuple
Subtitle = namedtuple('Subtitle', 'number start end content')

for root, dirs, filenames in os.walk(indir):
    print("# of files in directory:", len(filenames), '\n')
    print (root, dirs, filenames, '\n')
    filenames = [f for f in filenames if f!='.DS_Store']
    for file in filenames[:]:
        subtitle_text = open(os.path.join(root, file), 'r').read()
        index = df[df['filename'] == file].index.tolist()[0]
        
        #https://stackoverflow.com/questions/23620423/parsing-a-srt-file-with-regex
        # "chunk" our input file, delimited by blank lines
        with open(file) as f:
            res = [list(g) for b,g in groupby(f, lambda x: bool(x.strip())) if b]
            #print (res)
            
            subs = []
            for sub in res:
                if len(sub) >= 3: # not strictly necessary, but better safe than sorry
                    sub = [x.strip() for x in sub]
                    number, start_end, *content = sub # py3 syntax
                    #number, start_end, content = sub[0], sub[1], sub[2:]   # py 2 syntax
                    start, end = start_end.split(' --> ')
                    subs.append(Subtitle(number, start, end, content))  
            dft = pd.DataFrame({'content':subs})
            dft['new'] = dft['content'].apply(lambda x : x.content)
            dft['new2'] = dft['new'].apply(lambda x : re.sub(pattern, ' ', x[0]))
            dft['new3'] = dft['new'].apply(lambda x : ' '.join(x[1:]))
            dft['new4'] = dft['new2']+' '+dft['new3']
            dft['new4'] = np.where(dft['new2']=='Subtitles downloaded with "Netflix subtitle downloader" UserScript by Tithen-Firion.', '', dft['new4'])          
            dft['new5'] = dft['new4'].apply(lambda x : ''.join(c for c in x if c not in punctuation))
            dft[:10]    
            df.loc[index, 'content'] = ' '.join(dft['new5'].tolist())
            df.loc[index, 'number_words'] = len(' '.join(dft['new5'].tolist()).split())
df
```

    # of files in directory: 11 
    
    /Users/gsaxton/Dropbox/RosarioTijeras [] ['Rosario.Tijeras.S01E10.WEBRip.Netflix.srt', '.DS_Store', 'Rosario.Tijeras.S01E03.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E05.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E08.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E06.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E07.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E04.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E09.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E02.WEBRip.Netflix.srt', 'Rosario.Tijeras.S01E01.WEBRip.Netflix.srt'] 
    





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>filename</th>
      <th>number_words</th>
      <th>content</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rosario.Tijeras.S01E10.WEBRip.Netflix.srt</td>
      <td>4728.0</td>
      <td>Báilalo báilalo Eso Bonito bonito Caín  Muy bien  Eso  Y bueno le dicen el Brandon se llama Brandon Brandon Brandon Y pues nos conocimos No me suena Brandon   Quién es Brandon  Y somos somos  Amigos carnalitos  Ah Ese también quiero que bail...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Rosario.Tijeras.S01E03.WEBRip.Netflix.srt</td>
      <td>5565.0</td>
      <td>Toño Toño Espérame   Ábrela güey  Apúrale güey Nos están siguiendo  Dónde No los veo  Córrele güey  Ábreme ándale  Pues ésta no se abre Está mal güey Súbete a la cajuela que nos están siguiendo Córrele súbete a la cajuela güey    Milo Sabes qu...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Rosario.Tijeras.S01E05.WEBRip.Netflix.srt</td>
      <td>6351.0</td>
      <td>Puta madre   Estás ahí solo  Aquí estoy  Aquí estoy solo  Qué  No siento nada güey  Ya nos dejaron aquí  Oigan  Ey Oigan  No mames es en serio  Oigan      puerta se abre Alguien viene alguien viene Emilio estás bien   Sí estás bien tú  Sí   Gü...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rosario.Tijeras.S01E08.WEBRip.Netflix.srt</td>
      <td>5874.0</td>
      <td>Ay mija    Las mujeres como nosotras tenemos que aprovechar las oportunidades que nos da la vida Hmm Enderézate  El mundo está lleno de mujeres bonitas pero inteligentes somos pocas Hmm Así que ponte lista Ve por tu dinero o no Aquí estás para...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rosario.Tijeras.S01E06.WEBRip.Netflix.srt</td>
      <td>5928.0</td>
      <td>i No manches Rosarioi  El Brandon me trae por las nubes Ay sí Ahorita te trae por las nubes mi carnal Y luego te va a traer por las nubes otro   Y luego otro  Ay ya Cómo eres  Pues es la neta cisterna  A ti te gustan todos  Pues sí Bueno n...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rosario.Tijeras.S01E07.WEBRip.Netflix.srt</td>
      <td>5909.0</td>
      <td>No ya Tengo que colgar  Ya me voy Sí haz paro jefa Ya   Ahí está Mira nada más Vente     Ay pero sabe qué don Gonza Pues es que me da harta pena ir así Mire ni me arreglé ni nada  A ver cómo vienes  Hazle una vueltecita Despacito así  Ay don G...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Rosario.Tijeras.S01E04.WEBRip.Netflix.srt</td>
      <td>6043.0</td>
      <td>Ahora sí ya nos podemos ir Sí pero cómo  Qué hubo Yola  Oye quería ver si nos podían dar uni ridei para el cantón Lo que pasa es que no tenemos como irnos Cómo que no tienen cómo regresarse Agarren dinero y pidan un taxi Lo dejaste en la mes...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Rosario.Tijeras.S01E09.WEBRip.Netflix.srt</td>
      <td>5318.0</td>
      <td>Analicemos las evidencias sí Encontraron su celular y el mío tirados en medio del campo Según su versión yo fui el último en verla En resumidas cuentas significa que estoy frito Antonio qué voy a hacer  Qué voy a hacer  Invítame algo de tomar ...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Rosario.Tijeras.S01E02.WEBRip.Netflix.srt</td>
      <td>5822.0</td>
      <td>Suéltame Cristóbal Mamá  Suéltame   Cristóbal  No le grites a tu mamá Mira Cristóbal a mi jefa no le va a gustar que estés aquí Así que mejor vete alivianando   No importa lo que le guste a tu mamá Importa lo que a ti te va a gustar    Lárg...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Rosario.Tijeras.S01E01.WEBRip.Netflix.srt</td>
      <td>5917.0</td>
      <td>Carajo Puta madre Carajo muévete  Me voy a morir  No no no te vas a morir no te vas a morir   Mírame  Mírame a mí No te me vayas Mírame       Joven oríllese por favor Ayúdeme se está muriendo  Se me está muriendo  Okey Reporto un accid...</td>
    </tr>
  </tbody>
</table>
</div>



# Create list of all words
In the above dataset we can have 10 rows, with the *content* column in each row holding the complete subtitle text for that respective file. We'll use that to generate a comprehensive list of subtitle text. 

I'll show you a few iterations of working with PANDAS dataframe lists. First, we can use the *tolist( )* command to generate a list from any column in a PANDAS dataframe. In this next block of code we see that, as expected, there are 10 elements in a list generated from the *content* column.


```python
print(len(df['content'].tolist()))
print(type(df['content'].tolist()))
```

    10
    <class 'list'>


<br>However, we don't want a list with 10 elements. Rather, we want a single, combined *string* of subtitle text. We can get that through the *join* command. In the following block we create the above list then join all 10 elements, with a space between each element. We then print out the first 25 characters.


```python
print(len(' '.join(df['content'].tolist())))
print(type(' '.join(df['content'].tolist())))
print("First 25 characters: ", ' '.join(df['content'].tolist())[:25])
```

    297468
    <class 'str'>
    First 25 characters:       Báilalo báilalo Eso 


<br>We still need to do one thing -- we need to break our combined string up into words. We do this with the *split( )* command in Python, which breaks the string up at each space. The output is a list with as manuy elements as there are words in the list. We see below that there are 57,455 elements (words) in our combined list -- in other words, the first 10 episodes of *Rosario Tijeras* collectively use 57,455 words. 


```python
print(len(' '.join(df['content'].tolist()).split()))
print(type(' '.join(df['content'].tolist()).split()))
print("First 5 words: ", ' '.join(df['content'].tolist()).split()[:5])
```

    57455
    <class 'list'>
    First 5 words:  ['Báilalo', 'báilalo', 'Eso', 'Bonito', 'bonito']


<br>Now let's assign the above to a list called *word_list*


```python
word_list = ' '.join(df['content'].tolist()).split()
print(len(word_list))
print("First 5 words: ", word_list[:5])
```

    57455
    First 5 words:  ['Báilalo', 'báilalo', 'Eso', 'Bonito', 'bonito']


<br>Lastly, we'll use a list comprehension to make all words in *word_list* lower case.


```python
word_list = [word.lower() for word in word_list]
print(len(word_list))
print("First 5 words: ", word_list[:5])
```

    57455
    First 5 words:  ['báilalo', 'báilalo', 'eso', 'bonito', 'bonito']


# Count frequencies for words

Now we can see which words are employed most frequently in our the subtitles. We can do this simply in Python. Every word in our dataset is included in this list. It has 57,455 elements (words). Now how can we get a count for each word? By using `value_counts()` !  We can perform pure Python operations on this list, but in order to use the `value_counts()` function, which is a PANDAS feature, we need to first convert it to a PANDAS Series object. In the code below we thus convert the list to a PANDAS series and then run `value_counts()` and display the top 25 most frequent words.


```python
Series(word_list).value_counts()[:25]
```




    no      2507
    que     2078
    a       1973
    qué     1160
    la      1135
    de      1112
    te       920
    es       884
    me       868
    y        830
    sí       735
    ya       688
    lo       643
    el       626
    por      609
    se       591
    en       544
    pues     537
    yo       513
    con      454
    un       427
    está     426
    pero     393
    para     393
    mi       387
    dtype: int64



### Create a Dataframe with Frequency Counts for Each Tag
We can then easily convert this into a dataframe. We see there are 5,616 rows. That is, the subtitles include 5,616 different words in total across the first 10 episodes.


```python
wordcount_df = DataFrame(Series(word_list).value_counts())  
wordcount_df.columns = ['frequency']
print(len(wordcount_df))
wordcount_df[:10]
```

    5616





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>frequency</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>no</th>
      <td>2507</td>
    </tr>
    <tr>
      <th>que</th>
      <td>2078</td>
    </tr>
    <tr>
      <th>a</th>
      <td>1973</td>
    </tr>
    <tr>
      <th>qué</th>
      <td>1160</td>
    </tr>
    <tr>
      <th>la</th>
      <td>1135</td>
    </tr>
    <tr>
      <th>de</th>
      <td>1112</td>
    </tr>
    <tr>
      <th>te</th>
      <td>920</td>
    </tr>
    <tr>
      <th>es</th>
      <td>884</td>
    </tr>
    <tr>
      <th>me</th>
      <td>868</td>
    </tr>
    <tr>
      <th>y</th>
      <td>830</td>
    </tr>
  </tbody>
</table>
</div>



<br>We can then plot the most frequent words.


```python
plt.rcParams['figure.figsize'] = (20, 10)
wordcount_df['word_frequency'][:40].plot(kind='bar')
axhline(0, color='k')
xticks(fontsize = 12,rotation = 0, ha='center')
#savefig('25 most popular tags.png', bbox_inches='tight', dpi=300, format='png')
show()
```


![png](./Word%20Frequencies%20with%20Rosario%20Tijeras_56_0.png)


<br>When you're plotting a lot of bars, it is often better to have a horizontal bar graph. Below we generate one with the top 50 words.


```python
plt.rcParams['figure.figsize'] = (20, 10)
sns.set_style("whitegrid")
wordcount_df['word_frequency'][:50].plot(kind='barh').invert_yaxis()
axhline(0, color='k')
xticks(fontsize = 12,rotation = 0, ha='center')
yticks(fontsize = 12)
#savefig('25 most popular tags.png', bbox_inches='tight', dpi=300, format='png')
show()
```


![png](./Word%20Frequencies%20with%20Rosario%20Tijeras_58_0.png)


# Word cloud

### Create Text Document of all hashtags for creating Tag Cloud

Now let's create a <i>word cloud</i>. What we need to do is to create a single text file that contains every word used. To create a string document that contains every word used in the subtitles, we can just convert our list `word_list` into a string via the `' '.join(word_list)` command. This tells Python to join every item in our list together -- with a space in between each tag -- into a single combined text string called `all_words`. 


```python
word_list[:5]
```




    ['báilalo', 'báilalo', 'eso', 'bonito', 'bonito']




```python
all_words = ' '.join(word_list)
all_words[:20]
```




    'báilalo báilalo eso '



### Create Word Cloud

Lots of people have contributed to making Python a success. Often people will make public a package designed to fulfill a certain purpose. If something is available for your specific needs you may as well use it rather than reinventing the wheel. So, first I'll show you how to use Andreas Mueller's `WordCloud` package to visualize our tag cloud. Assuming you're using Anaconda Python, open up your Terminal and run <i>pip install wordcloud</i> -- https://github.com/amueller/word_cloud

Then import the package`


```python
from wordcloud import WordCloud
```

<br>At that point it's pretty simple to generate a tag cloud from our `all_words` variable. 


```python
wordcloud = WordCloud().generate(all_words)
plt.imshow(wordcloud)
plt.axis("off")
plt.show()
```


![png](./Word%20Frequencies%20with%20Rosario%20Tijeras_67_0.png)


Most packages include a multitude of options. Use the question mark to see a description of the available options.


```python
WordCloud?
```

<br>Sebastian Raschka also has a tutorial that explores some of the options in Mueller's WordCloud package. Sebastian's code requires we install PIL. In your terminal run <i>conda install pil</i> -- http://sebastianraschka.com/Articles/2014_twitter_wordcloud.html

Sebastian also uses a custom font. Try to download and install a custom font; e.g., http://ff.static.1001fonts.net/c/a/cabin-sketch.bold.ttf  For more about fonts on a Mac see this: https://support.apple.com/en-us/HT201722  Note the location of the downloaded font and let's use it in a new version of the word cloud


```python
wordcloud = WordCloud(font_path='/Users/gsaxton/Library/Fonts/cabin-sketch.bold.ttf',
                      background_color='white',
                      width=5600,
                      height=2800
                     ).generate(all_words)
plt.imshow(wordcloud)
plt.axis('off')
plt.show()
```


![png](./Word%20Frequencies%20with%20Rosario%20Tijeras_72_0.png)


### Create version of word cloud on *wordle* 
The `WordCloud` package is excellent for quickly generating a quality tag cloud. However, for more customization of our word cloud we can go to the website http://www.wordle.net. First, we save a copy of our combined text string to our computer.


```python
with open('all_words.txt', 'a') as out:
    out.write(all_words)
```

<br>Now copy and paste the contents of our document <i>all_words.txt</i> into http://www.wordle.net. Note that on my Mac at least, you can't use Chrome or Firefox. Safari works.

Note that I generally have to take a screenshot to capture word clouds on Wordle. The image below is a screen shot of a first word cloud I created: The font is "Telephoto," layout is "Horizontal," and color is "Ghostly." The word cloud below is also edited to remove names -- *Rosario, Brandon, Antonio,* etc. You can interpret the word cloud as showing the most frequent words in the database -- and the bigger the word, the more frequent it is used. If you took high school or college Spanish, you may not recognize some of the words. *Rosario Tijeras* depicts life in the *colonias* of Mexico City (*D.F.*) and therefore has a lot of slang that is specific to Mexico and/or the *D.F.* There are lots of good websites that can give you the definitions of some of the more colorful terms. :)


```python
from IPython.display import Image
Image(width=1000, filename='/Users/gsaxton/Dropbox/screenshots/tijeras_word_cloud.png') 
```




![png](./Word%20Frequencies%20with%20Rosario%20Tijeras_76_0.png)




```python
wordcount_df[50:100]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>frequency</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>vas</th>
      <td>185</td>
    </tr>
    <tr>
      <th>muy</th>
      <td>182</td>
    </tr>
    <tr>
      <th>todo</th>
      <td>180</td>
    </tr>
    <tr>
      <th>ah</th>
      <td>180</td>
    </tr>
    <tr>
      <th>carnal</th>
      <td>171</td>
    </tr>
    <tr>
      <th>sé</th>
      <td>171</td>
    </tr>
    <tr>
      <th>mira</th>
      <td>171</td>
    </tr>
    <tr>
      <th>güey</th>
      <td>168</td>
    </tr>
    <tr>
      <th>porque</th>
      <td>166</td>
    </tr>
    <tr>
      <th>quiero</th>
      <td>164</td>
    </tr>
    <tr>
      <th>ahí</th>
      <td>164</td>
    </tr>
    <tr>
      <th>estás</th>
      <td>159</td>
    </tr>
    <tr>
      <th>favor</th>
      <td>153</td>
    </tr>
    <tr>
      <th>su</th>
      <td>147</td>
    </tr>
    <tr>
      <th>estoy</th>
      <td>144</td>
    </tr>
    <tr>
      <th>gracias</th>
      <td>142</td>
    </tr>
    <tr>
      <th>jefa</th>
      <td>137</td>
    </tr>
    <tr>
      <th>ese</th>
      <td>130</td>
    </tr>
    <tr>
      <th>ni</th>
      <td>129</td>
    </tr>
    <tr>
      <th>del</th>
      <td>128</td>
    </tr>
    <tr>
      <th>ahora</th>
      <td>126</td>
    </tr>
    <tr>
      <th>tengo</th>
      <td>125</td>
    </tr>
    <tr>
      <th>tiene</th>
      <td>123</td>
    </tr>
    <tr>
      <th>este</th>
      <td>120</td>
    </tr>
    <tr>
      <th>hacer</th>
      <td>120</td>
    </tr>
    <tr>
      <th>oye</th>
      <td>119</td>
    </tr>
    <tr>
      <th>algo</th>
      <td>117</td>
    </tr>
    <tr>
      <th>esto</th>
      <td>116</td>
    </tr>
    <tr>
      <th>verdad</th>
      <td>114</td>
    </tr>
    <tr>
      <th>sabes</th>
      <td>112</td>
    </tr>
    <tr>
      <th>pasa</th>
      <td>110</td>
    </tr>
    <tr>
      <th>pasó</th>
      <td>106</td>
    </tr>
    <tr>
      <th>quién</th>
      <td>104</td>
    </tr>
    <tr>
      <th>ella</th>
      <td>102</td>
    </tr>
    <tr>
      <th>hay</th>
      <td>102</td>
    </tr>
    <tr>
      <th>esa</th>
      <td>98</td>
    </tr>
    <tr>
      <th>ir</th>
      <td>98</td>
    </tr>
    <tr>
      <th>ahorita</th>
      <td>98</td>
    </tr>
    <tr>
      <th>mí</th>
      <td>96</td>
    </tr>
    <tr>
      <th>simón</th>
      <td>93</td>
    </tr>
    <tr>
      <th>también</th>
      <td>91</td>
    </tr>
    <tr>
      <th>tienes</th>
      <td>90</td>
    </tr>
    <tr>
      <th>sea</th>
      <td>90</td>
    </tr>
    <tr>
      <th>esta</th>
      <td>90</td>
    </tr>
    <tr>
      <th>estar</th>
      <td>88</td>
    </tr>
    <tr>
      <th>mejor</th>
      <td>88</td>
    </tr>
    <tr>
      <th>dónde</th>
      <td>86</td>
    </tr>
    <tr>
      <th>ser</th>
      <td>86</td>
    </tr>
    <tr>
      <th>ti</th>
      <td>85</td>
    </tr>
    <tr>
      <th>quieres</th>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>



# Compare with 1,000 most common words
If anyone is not familiar with Mexican slang, some of the above words might be new to you, *¡Es la neta, güey!*  To highlight some of the most notable differences, let's compare our *RosarioTijeras* word frequencies to a frequency list available at *Wiktionary* that is built on a massive database of Spanish movie subtitles. We can use *html5lib* (you may have to *pip install html5lib*) and PANDAS to read the table directly into a new dataframe, which we'll call *df1000*.


```python
import html5lib
url = 'https://en.wiktionary.org/wiki/Wiktionary:Frequency_lists/Spanish1000'
df1000 = pd.read_html(url, header=0, index_col=0)[0]
df1000 = df1000.reset_index()
print('# of words in dataframe:', len(df1000))
df1000[:5]
```

### Remove names from *wordcount_df*
Before we compare the two databases, let's remove proper names from our *RosarioTijeras* dataframe *wordcount_df*. I found a handy list of character names here: https://en.wikipedia.org/wiki/Rosario_Tijeras_(Mexican_TV_series)#Cast


```python
wordcount_df = wordcount_df.drop('brandon', 0)
wordcount_df = wordcount_df.drop('rosario', 0)
wordcount_df = wordcount_df.drop('antonio', 0)
wordcount_df = wordcount_df.drop('betancourt', 0)
wordcount_df = wordcount_df.drop('emilio', 0)
wordcount_df = wordcount_df.drop('echegaray', 0)
wordcount_df = wordcount_df.drop('cristóbal', 0)
wordcount_df = wordcount_df.drop('gonzález', 0)
wordcount_df = wordcount_df.drop('camilo', 0)
wordcount_df = wordcount_df.drop('susana', 0)
wordcount_df = wordcount_df.drop('yolanda', 0)
wordcount_df = wordcount_df.drop('lety', 0)
wordcount_df = wordcount_df.drop('leticia', 0)
wordcount_df = wordcount_df.drop('sam', 0)
wordcount_df = wordcount_df.drop('samantha', 0)
wordcount_df = wordcount_df.drop('peludo', 0)
wordcount_df = wordcount_df.drop('luis', 0)
wordcount_df = wordcount_df.drop('enrique', 0)
wordcount_df = wordcount_df.drop('sudarsky', 0)
wordcount_df = wordcount_df.drop('ruby', 0)
wordcount_df = wordcount_df.drop('delia', 0)
wordcount_df = wordcount_df.drop('fierro', 0)
wordcount_df = wordcount_df.drop('don', 0)
wordcount_df = wordcount_df.drop('gonzalo', 0)
wordcount_df = wordcount_df.drop('marta', 0)
wordcount_df = wordcount_df.drop('paula', 0)
wordcount_df = wordcount_df.drop('restrepo', 0)
wordcount_df = wordcount_df.drop('toño', 0)
```


```python
print(len(df1000))
print(len(wordcount_df))
```

    1000
    5588


##### Compare top 1,000 words
Python *sets* are great for determining the *difference* or the *intersection* of two lists. In the next line of code we take the difference of two sets -- the top 1,000 words from the *Wiktionary* list and the top 1,000 words from our *RosarioTijeras* database. We see there are 390 words that are different; the other 610 words are common to both lists. 


```python
print(len(set(df1000['word'].tolist()) - set(wordcount_df[:1000].index.tolist())))
```

    390



```python
print(len( set(wordcount_df[:1000].index.tolist()) - set(df1000['word'].tolist())))
```

    390


##### Top 500 words
Similarly, we see there are 188 different words among the top 500.


```python
print(len(set(df1000[:500]['word'].tolist()) - set(wordcount_df[:500].index.tolist())))
```

    188



```python
print(len( set(wordcount_df[:500].index.tolist()) - set(df1000[:500]['word'].tolist())))
```

    188


##### Top 200
And 59 different words among the top 200.


```python
print(len(set(wordcount_df[:200].index.tolist()) - set(df1000[:200]['word'].tolist())))
print(len(set(df1000[:200]['word'].tolist()) - set(wordcount_df[:200].index.tolist())))
print(len(set(df1000[:200]['word'].tolist()) - set(wordcount_df[:200].index.tolist())))
```

    59
    59
    59


<br>Let's print out those 59 words:


```python
print(set(wordcount_df[:200].index.tolist()) - set(df1000[:200]['word'].tolist()))
```

    {'onda', 'ven', 'nomás', 'ah', 'madre', 'salir', 'chamba', 'digo', 'vámonos', 'órale', 'ves', 'general', 'ahorita', 'ándale', 'oye', 'ay', 'pues', 'dar', 'simón', 'perdón', 'moto', 'dejar', 'escuela', 'cacho', 'cabrón', 'nel', 'van', 'además', 'mal', 'jefa', 'mamá', 'mija', 'luego', 'manches', 'hija', 'hermano', 'cámara', 'amor', 'familia', 'barrio', 'ey', 'contigo', 'tranquila', 'carnal', 'acá', 'tranquilo', 'toda', 'hubo', 'ustedes', 'unos', 'pasó', 'eh', 'serio', 'niña', 'güey', 've', 'conmigo', 'neta', 'muchas'}


##### Top *Rosario Tijeras* words that are not in Wiktionary top 1,000 list
Now let's see how many of the top 200 *Rosario Tijeras* words are not in the top 1,000 Wiktionary list words. There are 21 of them.  


```python
print(len(set(wordcount_df[:200].index.tolist()) - set(df1000['word'].tolist())))
print(len(set(df1000['word'].tolist()) - set(wordcount_df[:200].index.tolist())))
print(set(wordcount_df[:200].index.tolist()) - set(df1000['word'].tolist()))
```

    21
    821
    821
    {'onda', 'nomás', 'chamba', 'órale', 'ahorita', 'ándale', 'simón', 'moto', 'cacho', 'nel', 'cabrón', 'jefa', 'mija', 'manches', 'cámara', 'ey', 'barrio', 'tranquila', 'carnal', 'güey', 'neta'}



```python
print('Top 100 Spanish words not in top 100 Rosario Tijeras:', set(df1000[:100]['word'].tolist()) - set(wordcount_df[:100].index.tolist()))
```

    Top 100 Spanish words not in top 100 Rosario Tijeras: {'son', 'hola', 'ha', 'puedo', 'señor', 'sólo', 'soy', 'sus', 'creo', 'fue', 'dios', 'eres', 'estaba', 'dos', 'tan', 'cuando', 'casa', 'era', 'vez', 'tiempo', 'él', 'nunca', 'todos', 'he', 'puede'}


<br>Lastly, we can also find the 5 words that are in the *Rosario Tijeras* top 100 that are not found in the Wiktionary top 1,000 list: *carnal, ahorita, jefa, güey,* and *simón*.


```python
print('# of top 100 Rosario Tijeras words not in top 1,000 Spanish words:', len(set(wordcount_df[:100].index.tolist()) - set(df1000['word'].tolist())))
print('Top 100 Rosario Tijeras words not in top 1,000 Spanish words: ', set(wordcount_df[:100].index.tolist()) - set(df1000['word'].tolist()))
print('# of top 100 Rosario Tijeras words in top 1,000 Spanish words:', len(set(wordcount_df[:100].index.tolist()).intersection(set(df1000['word'].tolist()))))
print('# of top 100 Spanish words not in top 100 Rosario Tijeras:', len(set(df1000[:100]['word'].tolist()) - set(wordcount_df[:100].index.tolist())))
print('# of top 100 Rosario Tijeras words in top 1,000 Spanish words:', len(set(wordcount_df[:100].index.tolist()).intersection(set(df1000[:100]['word'].tolist()))))
```

    # of top 100 Rosario Tijeras words not in top 1,000 Spanish words: 5
    Top 100 Rosario Tijeras words not in top 1,000 Spanish words:  {'carnal', 'ahorita', 'jefa', 'güey', 'simón'}
    # of top 100 Rosario Tijeras words in top 1,000 Spanish words: 95
    # of top 100 Spanish words not in top 100 Rosario Tijeras: 25
    # of top 100 Rosario Tijeras words in top 1,000 Spanish words: 75


<br>In this tutorial we have covered how to read in and parse subtitle files, generate a frequency count for each of the words included in our dataframe and to plot the results. We have also covered how to make comparisons between lists. I hope you have found it educational. If so, please share.

For more Notebooks as well as additional Python, Big Data, and data analytics tutorials, please visit http://social-metrics.org or follow me on Twitter <a href='https://twitter.com/gregorysaxton'>@gregorysaxton</a>
