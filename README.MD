# python-ascii-art
A command line tool for generating ascii art from reference images.

Examples are in the 'pictures' directory, and an explanation of how it works is below.

# Usage
`python3 main.py -c <compression factor> -i <input file> -o <output file>`

# Technical details

Here be dragons.

```
''''''''''''''''''''''''''''''''''''''''''''\\''''''''''''''''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''YY''''''CC''''''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''11!!''''''jj''''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''99''''''EE;;''''''''''''''''''''''''''''''''''''''''
'''''''''''''''''''''''''''''''''''''''''''''''';;99''''''99''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''ZZEE''''''''XX''''''''''XX99''''nn99''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''9999qq\\::9999YY''''''''99qq''''99qq''''''''''''''''''''''''''''''''''''
''''''''''''''''229999999999999999999999999999TT''''oo9955''''99qq''''''''''''''''''''''''''''''''''
''''''''''''''''''9999999999999999999999999999999999999999qq''1199PP''''''''''''''''''''''''''''''''
'''''''''''''';;hh99999999999999999999999999999999999999999955[[9999aa''''''''''''''''''''''''''''''
''''''xx9999999999999999999999999999999999999999999999999999999999999999''''''''''''''''''''''''''''
''''''''\\99999999999999999999999999999999999999999999999999999999999999qq''''''''''''''''''''''''''
''''''''__9999999999999999aa''''''''''''''!!pp999999999999999999999999999999''''''''''''''''''''''''
''''''ee99999999999999rr''''''''''''''''''''''''}}9999999999999999999999999999''''''''''''''''''''''
''::99999999999999qq''''''''''''''''''''''''''''''''LL99999999999999999999999999''''''''''''''''''''
''XX99999999999999''''''''''''''''''''''''''''''''''''''qq999999999999999999999999''''''''''''''''''
''''''9999999999''''''''''''''''''''''''''''''''''''''''''VV9999999999999999pp9999PP''''''''''''''''
''''UU99999999pp''''''''''''''''''''''''''''''''''''''''''''xx99999999999999''''9999;;''''''''''''''
''++9999999999::''''''''''''''''''''''''''''''''''''''''''''''nn999999999999FF'';;9999''''''''''''''
''999999999999''''''''''''''''''''''''''''''''''''''''''''''''''44999999999999YY''YY99jj''''''''''''
qq999999999999''''''''''''''''''''''''''''''''''''''''''''''''''''99999999999999PP==9999''''''''''''
''''9999999999''''''''''''''''''''''''''''''''''''''''''''''''''''''9999999999999999999966''''''''''
''''9999999999''''''''''''''''''''''''''''''''''''''''''''''''''''''\\99999999999999999999;;''''''''
''''9999999999''''''''''''''''''''''''''''''''''''''''''''''''''''''''''9999999999999999kk''''''''''
''''999999999999''''''''''''''''''''''''''''''''''''''''''''''''''''''''''kk99999999999999''''''''''
''YY999999999999''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''!!999999999999ZZ''''''''
''55jjjj99999999pp''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''PP999999999977''''''
''''''''9999999999ff''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''jj9999999999TT''''
''''''''999999999999>>''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''??9999999999aa''
''''''''FF999999999999^^''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''II999999999999
''''''''''99[[9999999999JJ''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''999999999999
''''''''''''''''9999999999%%'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''';;9999999999
''''''''''''''''''XX9999999999''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''99999999,,
''''''''''''''''''''((9999999999CC''''''''''''''''''''''''''''''''''''''''''''''''''''''''999999==''
''''''''''''''''''''''''ee9999999999vv''''''''''''''''''''''''''''''''''''''''''''''''''''99pp''''''
''''''''''''''''''''''''''''UU9999999999++''''''''''''''''''''''''''''''''''''''''''''''::''''''''''
''''''''''''''''''''''''''''''''UU9999999999YY''''''''''''''''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''ww9999999999VV''''''''''''''''''''''''''''''''''''''''''''''''''
'''''''''''''''''''''''''''''''''''''''']]9999999999FF''''''''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''!!qq99999999!!''''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''pp999999VV''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''qq9999qq''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''119999qq''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''6699qq''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''nn99qq''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''**99YY''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''++99''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''IIZZ''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''99''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''!!^^''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''pp''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''22''''''''''''''''''''''''''
```

## Generating the ideal ascii representation for your chosen image

When calling `image_to_string(image, square)`, there are rules to follow for the `square` parameter.

1. `square` ideally should be some factor of the width of the image
    - This means if the image is 512 px wide, the ideal square is any of  [2, 4, 8, 16, 32, 64, 128, 256]
    - For images with a prime (ie indivisible) width it is okay to use a square of arbitrary size, it will fill in any gaps intelligently
    - Some basic math can tell us that all numbers have two predictable factors, 1 and itself, this leads us to point 2.
2. `square` should be less than the width of the image and greater than 1.
    - If `square == 1`, each pixel is represented as a character. This is practically useless. It also mangled the image when I tested it, and I feel no obligation to support this. This is because any image greater than 44 * 44 in size would be too large to send in discord. Almost all images are larger than that, and if I can't send it in discord I don't need it.
    - If `square` is equal to the width of the image, the entire image will be represented as one character. This is useless for obvious reasons.    

## How it works

The way it works is fairly simple, I render a chosen alphabet of letters to individual images in the font I use, you can change this.
I then go through each of these letter images and take the mean of the pixel values in terms of 'lightness'.
This average is treated as the 'lightness' value for the letter.
Each letter is then added to a dict with the lightness as the key and the letter as the value.

From here, the image is read (without color), and it is split up into sections according to `square`.
The stream of pixels is then partitioned into rows based on the image width.
These rows are then partitioned into slices the length of `square`.
Following this, the list of the lists of slices of each row is partitioned again into segments of length `square`.

At this point, we have a list of `square` length segments of rows cut into `square` sizes.
The segments in each partitioned row are then zipped together.

This process is necessary to transform the image from one continuous stream of pixels into a list of evenly sized squares.
This is why the parameter is named `square`, the image is partitioned into `square * square` segments.

After obtaining each square, I again take the statistical mean.

This process is demonstrated in the example below.

## An example of the process with dummy data

Here we have an 8 x 8 example of what an image looks like when we turn it into its "lightness" values.
- The values are typically much higher than this, but this is an example using random data. The process is the same either way.
- Since our image is 8 x 8, 4 is a factor of the width, and we will be using 4 for the value of `square` in these examples.

```python
image = [6, 9, 8, 9, 3, 1, 8, 0,
         9, 2, 7, 4, 8, 1, 4, 7,
         0, 6, 7, 9, 3, 5, 7, 2,
         7, 1, 4, 8, 5, 3, 2, 6,
         0, 6, 1, 6, 8, 0, 3, 4,
         1, 9, 1, 2, 0, 0, 3, 5,
         7, 2, 8, 4, 8, 1, 9, 5,
         7, 0, 9, 2, 5, 3, 5, 6]
```

#### 1. Extracting rows of the image from the array

The first step is to partition the image, which is currently one continuous list, into rows. I will be using the same functions I used in the source to demonstrate.

Since we know our image is 8 x 8 (which we could learn from pil's image object in the real-world), we will partition by 8 to get rows.
This is the only time we partition by a number that is not `square`.
```python
step_one = partition_with_padding(image, 8)

# Result
step_one = [(6, 9, 8, 9, 3, 1, 8, 0),
            (9, 2, 7, 4, 8, 1, 4, 7),
            (0, 6, 7, 9, 3, 5, 7, 2),
            (7, 1, 4, 8, 5, 3, 2, 6),
            (0, 6, 1, 6, 8, 0, 3, 4),
            (1, 9, 1, 2, 0, 0, 3, 5),
            (7, 2, 8, 4, 8, 1, 9, 5),
            (7, 0, 9, 2, 5, 3, 5, 6)]
```

#### 2. Breaking rows into slices of length `square`

From here, we need to break each row into segments we can recombine later.
Think of this as preparing the x-axis to be formed into a square.

```python
step_two = [partition_with_padding(row, 4) for row in step_one]

# Result
step_two = [[(6, 9, 8, 9), (3, 1, 8, 0)],
            [(9, 2, 7, 4), (8, 1, 4, 7)],
            [(0, 6, 7, 9), (3, 5, 7, 2)],
            [(7, 1, 4, 8), (5, 3, 2, 6)],
            [(0, 6, 1, 6), (8, 0, 3, 4)],
            [(1, 9, 1, 2), (0, 0, 3, 5)],
            [(7, 2, 8, 4), (8, 1, 9, 5)],
            [(7, 0, 9, 2), (5, 3, 5, 6)]]
```

#### 3. Grouping our row slices together 


Following this step, the slices are then partitioned again into segments of length `square`.
Think of this as preparing the y-axis to be formed into a square.

```python
step_three = partition_with_padding(step_two, 4)

# Result
step_three = [([(6, 9, 8, 9), (3, 1, 8, 0)],
               [(9, 2, 7, 4), (8, 1, 4, 7)],
               [(0, 6, 7, 9), (3, 5, 7, 2)],
               [(7, 1, 4, 8), (5, 3, 2, 6)]),
              ([(0, 6, 1, 6), (8, 0, 3, 4)],
               [(1, 9, 1, 2), (0, 0, 3, 5)],
               [(7, 2, 8, 4), (8, 1, 9, 5)],
               [(7, 0, 9, 2), (5, 3, 5, 6)])]
```
#### 4. Recombining our partitioned and organized image

Now that we've prepared both axes, we can use the `zip` function and some nifty python syntax to pair the values from each square together easily.

```python
# If you've never seen or used zip before, it's easy and useful. zip([a, b], [c, d]) => [[a, c], [b, d]]

step_four = [list(zip(*row)) for row in step_three]

# Result
step_four = [[((6, 9, 8, 9),
               (9, 2, 7, 4),
               (0, 6, 7, 9),
               (7, 1, 4, 8)),
              ((3, 1, 8, 0),
               (8, 1, 4, 7),
               (3, 5, 7, 2),
               (5, 3, 2, 6))],
             [((0, 6, 1, 6),
               (1, 9, 1, 2),
               (7, 2, 8, 4),
               (7, 0, 9, 2)),
              ((8, 0, 3, 4),
               (0, 0, 3, 5),
               (8, 1, 9, 5),
               (5, 3, 5, 6))]]
```

#### 5. Averaging each row of each square

After organizing our squares, we then reduce each row in each square to its mean.

```python
step_five = [[[mean(segment) for segment in row] for row in square] for square in step_four]

# Result
step_five = [[[8, 5.5, 5.5, 5],
              [3, 5, 4.25, 4]],
             [[3.25, 3.25, 5.25, 4.5],
              [3.75, 2, 5.75, 4.75]]]
```

#### 6. Calculating the average of each square and returning them in rows

All that's left to get the final data we need to turn the image into corresponding characters is to reduce it even further by averaging each square. 

```python
step_six = [[mean(square) for square in row] for row in step_five]

# Result
step_six = [[6.0, 4.0625],
            [4.0625, 4.0625]]
```

I'd then loop through `step_six`, and get the character from the previously mentioned dictionary with the nearest value.
Because characters are taller than they are wide, every time I get a character from the dict I get two.
This seems to make the ratio just right.

Collecting every set of characters into a string would then ideally yield a quality image made from text.

That's all!

# Examples
### Hello
![](test/hello.png)

(cropped due to size)
```
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''WW'''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''WWWWWW''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''WWWW'''''''
WWWWWW''''''''''''''''__WWWWWW''''''''''''''''''''''''''''''''''''''WWWWWW''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''WWWW'''''
WWWWWW''''''''''''''''__WWWWWW''''''''''''''''''''''''''''''''''''''WWWWWW''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''EEWWGG'''
WWWWWW''''''''''''''''__WWWWWW''''''''''''''''''''''''''''''''''''''WWWWWW''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''WWWW'''
WWWWWW''''''''''''''''__WWWWWW''''''''''''''''''''''''''''''''''''''WWWWWW''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''QQWWNN'
WWWWWW''''''''''''''''__WWWWWW''''''''''''''''''''''''''''''''''''''WWWWWW''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''''''''''''''''33''''''''''''''''WWWW'
WWWWWW''''''''''''''''__WWWWWW''''''''''''IIWWWWWWWWWWWW''''''''''''WWWWWW''''''''''WWWWWW''''''''''''XXWWWWWWWWWWWW''''''''''''''''''''''''''''WWWWWW''''''''''''''WWWW;
WWWWWW''''''''''''''''__WWWWWW''''''''''BBWWWWWWWWWWWWWWWW''''''''''WWWWWW''''''''''WWWWWW''''''''''WWWWWWWWWWWWWWWWWWjj''''''''''''''''''''''''WWWWWW''''''''''''''WWWWW
WWWWWW''''''''''''''''aaWWWWWW''''''''IIWWWWWW''''''11WWWWWW''''''''WWWWWW''''''''''WWWWWW''''''''ggWWWWMM''''''**WWWWWW''''''''''''''''''''''''IIWW__''''''''''''''WWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWW''''''''WWWWWW''''''''''PPWWWW''''''''WWWWWW''''''''''WWWWWW''''''''WWWWWW''''''''''IIWWWWBB''''''''''''''''''''''''''''''''''''''''''TTWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWW''''''''WWWWWW''''''''''''WWWWEE''''''WWWWWW''''''''''WWWWWW'''''';;WWWW00''''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''__WWW
WWWWWW''''''''''''''''22WWWWWW''''''YYWWWW&&''''''''''}}WWWWWW''''''WWWWWW''''''''''WWWWWW''''''MMWWWW__''''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''''WWW
WWWWWW''''''''''''''''__WWWWWW''''''WWWWWWWWWWWWWWWWWWWWWWWWWW''''''WWWWWW''''''''''WWWWWW''''''WWWWWW''''''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''''WWW
WWWWWW''''''''''''''''__WWWWWW''''''00WWWWWWWWWWWWWWWWWWWWWWWW''''''WWWWWW''''''''''WWWWWW''''''WWWWWW''''''''''''''WWWWWW'''''''''''''''''''''''''''''''''''''''''',,WWW
WWWWWW''''''''''''''''__WWWWWW''''''^^WWWWGG''''''''''''''''''''''''WWWWWW''''''''''WWWWWW''''''PPWWWW**''''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''!!WWW
WWWWWW''''''''''''''''__WWWWWW''''''''WWWWWW''''''''''''''''''''''''WWWWWW''''''''''WWWWWW''''''''WWWWWW''''''''''''WWWWWW''''''''''''''''''''''''''''''''''''''''''00WWW
WWWWWW''''''''''''''''__WWWWWW''''''''WWWWWWdd''''''''''xx''''''''''WWWWWW''''''''''WWWWWW''''''''WWWWWW11''''''''WWWWWW\\''''''''''''''''''''''''yy''''''''''''''''WWWWW
WWWWWW''''''''''''''''__WWWWWW''''''''''WWWWWWWWaa;;33WWWWWW''''''''WWWWWW''''''''''WWWWWW''''''''''WWWWWWMM!!ssWWWWWWWW''''''''''''''''''''''''WWWWWW''''''''''''''WWWWE
WWWWWW''''''''''''''''__WWWWWW''''''''''''WWWWWWWWWWWWWWWWcc''''''''WWWWWW''''''''''WWWWWW''''''''''!!WWWWWWWWWWWWWWMM''''''''''''''''''''''''''WWWWWW''''''''''''''WWWW'
WWWWWW''''''''''''''''__WWWWWW''''''''''''''''MMWWWWWWjj''''''''''''WWWWWW''''''''''WWWWWW''''''''''''''11WWWWWW&&''''''''''''''''''''''''''''''CCWW;;''''''''''''rrWWWW'
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''WWWW^^'
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''',,WWWW'''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''WWWW'''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''00WWii'''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''WWYY'''''''
```


### Smile
![](test/smile.png)

```
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''++&&WWWW&&++''''''''''''''''''''''''''
''''''''''''''''''''XXWWWWWWWWWWWWWWWWWWWWXX''''''''''''''''''''
''''''''''''''''YYWWWWqq''''''''''''''''qqWWWWYY''''''''''''''''
''''''''''''''NNWWqq''''''''''''''''''''''''qqWWNN''''''''''''''
''''''''''''MMWW''''''''''''''''''''''''''''''''WWMM''''''''''''
''''''''''NNWW''''''''''''''''''''''''''''''''''''WWNN''''''''''
''''''''YYWW''''''''''''''''''''''''''''''''''''''''WWYY''''''''
''''''''WWqq''''''''''qqqq''''''''''''qqqq''''''''''qqWW''''''''
''''''XXWW''''''''''!!WWWW!!''''''''!!WWWW!!''''''''''WWXX''''''
''''''WWqq''''''''''MMWWWWMM''''''''MMWWWWMM''''''''''qqWW''''''
''''''WW''''''''''''MMWWWWMM''''''''MMWWWWMM''''''''''''WW''''''
''''++WW''''''''''''!!WWWW!!''''''''!!WWWW!!''''''''''''WW++''''
''''&&WW''''''''''''''qqqq''''''''''''qqqq''''''''''''''WW&&''''
''''WWWW''''''''''''''''''''''''''''''''''''''''''''''''WWWW''''
''''WWWW''''''''''''''''''''''''''''''''''''''''''''''''WWWW''''
''''&&WW''''''xxxx''''''''''''''''''''''''''''xxxx''''''WW&&''''
''''++WW''''''GGWW''''''''''''''''''''''''''''WWGG''''''WW++''''
''''''WW''''''''WWrr''''''''''''''''''''''''rrWW''''''''WW''''''
''''''WWqq''''''##WW''''''''''''''''''''''''WW##''''''qqWW''''''
''''''XXWW''''''''WWWW''''''''''''''''''''WWWW''''''''WWXX''''''
''''''''WWqq''''''''MMWWpp''''''''''''ppWWMM''''''''qqWW''''''''
''''''''YYWW''''''''''nnWWWWWWWWWWWWWWWWnn''''''''''WWYY''''''''
''''''''''NNWW''''''''''''''ppWWWWpp''''''''''''''WWNN''''''''''
''''''''''''MMWW''''''''''''''''''''''''''''''''WWMM''''''''''''
''''''''''''''NNWWqq''''''''''''''''''''''''qqWWNN''''''''''''''
''''''''''''''''YYWWWWqq''''''''''''''''qqWWWWYY''''''''''''''''
''''''''''''''''''''XXWWWWWWWWWWWWWWWWWWWWXX''''''''''''''''''''
''''''''''''''''''''''''''++&&WWWW&&++''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
```

### dazzle2
![](test/dazzle2.png)

```
ffWWWWWWhh''''WWWWII''''''''NNWW''''''MMWWWW,,''''''''''''''''''MMWWMM''''''''NNWWWWrr''''''WWWW11''''''''''''''MM''''''CCWWWW''''''WWWW''''YYWW''''WWWW''''''''WWWW'''''';;
''KKWWWWWW))''''WWWW<<''''''''WWWW''''''WWWWWW''''''''''wwMM'',,WWMM''''''''MMWWWW''''''!!WWWW''''''''''''''''''QQ''''''''WWWW''''''rrWWRR''''WW''''WWWWWW''''''>>WWMM''''''
''''NNWWWWWW,,''rrWWWW''''''''''WWWW''''''WWgg''''''NNjjWW$$''''''''''''''MMWWWW''''''VVWW&&''''''''''''RR''''''''WW''''''ggWW&&''''''WWWW''''WW''''''WWWWMM''''''CCWWRR''''
''''''WWWWWWWW''''ZZWWWW''''''''''WWNN''''''''''''FF''nnMM''''''''WWRR''uuWWWW''''''00WWYY''''''''''>>WWWWJJ''''''II__''''''WWWW''''''WWWW''''MM;;''''11WWWW00''''''RRWW22!!
''''''''WWWWWWWW''''RRWWWW''''''''--WWDD''''''''''!!''++''''''''WWWW''''''''''''''WWWW''''''''''''BBWWWWWW''''''''''WW''''''BBWW++''''!!WWjj''++&&''''''XXWWWWkk''''''NNWWWW
WW''''''''WWWWWWMM''''MMWWMM''''''''jjWW''''''''OO''''''''''''WWWW''''''''\\NN''''pp'''''''''';;WWWWWWVV''''''''''''\\^^''''''WWWW''''''WWWW''''WW''''''''BBWWWW++''''''WWWW
WWMM''''''--WWWWWWBB''''WWWW00''''''''nn''''''##''''''''''''WWWW''''''''FFOO''''''\\''''''''RRWWWWNN''''''SSWW##''''''WW''''''MMWW''''''MMWW''''WW''''''''''WWWWWW,,''''''WW
eeWWRR''''''jjWWWWWWGG''''WWWWPP''''''''''''^^''''''&&''''MMWW''''''''KK**''''''88WWWWgg''''NNWW!!''''\\WWWWWWWW;;''''''++''''''WW&&''''::WW''''MM''''''''''''WWWWWW''''''!!
''RRWWee''''''PPWWWWWWYY''''WWWWjj'''''''''',,''''44WW;;NNWW''''''''BB''''''''WWWWWW,,'''''''';;''''MMWWWWWWWWWWUU''''''NN''''''WWWW''''''WW00''>>xx''''''''''''WWWWWW''''''
''''MMWWrr''''''00WWWWWW!!''!!WWWW''''''''II''''rrWWrr''II''''''''MM''''''!!WWWW00''''''''''##'''''';;WWWWWWHH''''''''''''yy'''';;WW))''''NNWW''''WW''''''''''''>>WWWWWW''''
''''''WWWW''''''''MMWWWWWW''''YYMM''''''FF''''''WWTT''''''''''''&&''''''OOWWWW!!''''''''\\rr''''''''''''''''''''''''''''''gg''''''WWWW''''''WW''''WW''''''''--''''33WWWWBBYY
''''''''WWWW''''''''WWWWWWWW''''''''''''''''''WWII''''''22''''aa''''''MMWWNN''''''''''66''''''''''''''''&&&&''''''ccWW''''''22''''**WW''''''WW{{''NN''''jjWWWW''''''&&WWWWWW
'''''''''''''''''''''''''',,__''''''''''''''WWXX''''''WW##''^^''''''WWWW**''''''''II''''''''''''''''00WWWW&&''''''''MMQQ''''nn''''''WW&&''''&&WW''!!,,''''YY''''''''''''''++
''''''''''''''''''''''''''''''''''''??''''NNgg''''''WWII''''''''eeWWMM''''''''''!!''''''''''''''RRWWWWGG'''''''''''',,''''''''OO''''VVWW''''''WW''''gg'''''''''''''''''''';;
WWWWWWWWWWWWWWMMBB##PPooTTrr^^;;''cc''''GG00''''''WWrr''''WW''NNWWyy''''''''uu''''''''''''''DDWWWWoo''''''''''''11WWWWWWGG''''!!''''''WW11''''WW''''WW''''''''00WW''''''''WW
WWWWWWWWWWWWWWWWWWWWWWWWMM##ee77\\''''JJBB''''--WW''''__&&''''77''''''''rr''''''''''''''GGWWWWrr''''''''''''DDWWWWMM--''''''''''##''''KKWW''''RR00''BB''''NNWW00''''''''''99
''''''''''''''''''''''''''''''''''''''MM'''';;WW''''uuyy''''''''''''''::''''''''''''OOWWWW--''''''''''::WWWWWWYY''''''''''''''''''''''''WW''''''WW''__''''''''''''''aa''''''
''''''''''''''''''''''''__YY00WWWWdd__''''!!WW''''RR''''''''00WW''!!''''''''''''UUWWMM''''''''''''aaWWWWRR''''''''''''''''''''''''KK''''BB00''''WW''''11''''''&&WW==''''''''
''''''__YY00WWWWWWWWWWMMJJ''''''''''''''^^NN''''BB''''''''WWCC''''''''''''''aaWW&&''''''''''''NNWWMM--''''''''''''''''''''''WWNN''''''''''WW''''GGxx''MM''''''''''''''''''''
''''''WWWWWWmm;;''''''''''''''''''++WWWWMM''''%%''''''mmMM''''CCWWWW^^''IIWWGG''''''''''++WWWWYY''''''''''''''''''''&&MM''''RRWW''''hh''''MM11''''WW''00''''''''''''''QQWWKK
''''''''''''''''''''''''''^^MMWWWWWWWW__'''',,''''''WW^^''::WWWWWW''''''__''''''''''RRWWRR''''''''''''''''''''''MM**''WW''''''WW66''''''''''WW''''WW''''''''''--NNWWWW==''^^
WW''''''''''''''''__BBWWWWWWWWWWdd''''''''HH''''kkDD''''MMWWWW''''''''''MM'''';;WWMM--''''''''''''''''''''''''''''''''WW00''''MMWW''''77''''WW''''kk''''''''''NN''''''''JJWW
WWoo''''''''RRWWWWWWWWWWWWWW;;'''''''''';;WWWW00''''PPWWWW''''''''!!WWGG''''''''''''''''''''''''++WWWWWW&&''''''''''KKWWWW''''''WWrr''''''''__00''''&&''kk''''''''EEWWWWWWWW
''''''''''''WWWWWWWWWWbb''''''''''''''''''''''''''WWWW::''''''ttWW^^''''''''11WWWW!!''''''''''''''''33WWWWWWWW66''''WWWWMMyy''''WWWW'''';;''''WW''''BB''WW''''WWWWWWWW44''rr
''''RR''''''**WWWW;;''''''''''WWWWWW;;'''''''''''';;''''''44&&''''''''''NNWWWWWWWWWWWWWW>>''''''''''''''''RRWWWWWWWWWWWW__''''''((WW''''''''''MMWW''''WWWW''''BBjj'''''''',,
WWII''''''''''''''''''''jj''''''mmWWWWBB''''''''44''''RRYY''''''''SSWWWWWWWWWWWWWWWWWWWWWWWWNN''''''''''''''''''MMWWWWWW''''''''''WWMM''''''''WWWW''''WWWW''''''''''''''KKWW
''''''''''''''''''''''''MMWW''''''''WWWWWWMMWWWWWWWW!!''''''11WWWWWWWWWWMM''''''NNWWWWWWWWWWWWWWWWgg''''''''''''''''DDMM''''''''''ddWW''''''''NNWW&&'',,WWaa''''''BBWWhh''rr
''==WWWWWWff''__''''''''''xxWWKK''''''UUWWWWWWWWCC''''''NNWWdd''''BBWW11''''''''''''!!WWWWWWWWWWWWWWWWWWYY''''''''''!!''''''''rr''''WWDD''''''''WWWW''''WWWW''''++''''''''!!
WWWW&&''''''''WWWW^^''''''''''MMWW''''''''>>''''''''''!!'''''';;WWNN''''''''KKMM;;''''''''YYWWWWWWWWWWWWWWWWWW;;''''''''''''''WW''''NNWW''''''''WWWW22''xxWW''''''''''!!MMWW
'''''''''''''';;WWWWNN''''''''''11WWRR''''''''''''ggWWWW''''&&WW^^''''''''WWWWWWWWWWBB''''''''''bbWWWWWWWWWWWWWWWW&&aa''''''''MM''''''WWYY''''''!!WWWW''''WW''''--WWWWWWBBRR
''''''''NNWWWW''''33WWWW11''''''''''BBWW!!--NNWWWWMM__''''WW&&''''''''RRWWWWWW}}WWWWWWWWWWGG''''''''''BBWWWWWWWWWWWW''''''''BB--''MM''WWWW''''''''WWWW!!''$$UU''''KK''''''''
44++'''';;WWWWWW''''''WWWWMM''''''''''^^WWWWDD''''''''''''''''''''__WWWWWWNN''''''''00WWWWWWWWWWYY'''''''';;MMWWWWWW''''''''WW''''WWII!!WW--''''''aaWWWW''''WW''''''''''''pp
WWWW''''''WWWWWWWWXX''''nnWWWWxx''''''''''''''''''''''''''''''''&&WWWWWW\\''''MM''''''''''MMWWWWWWWWWW!!''''''''jjWW''''''''MM''00WW''''MMWW''''''''WWWW''''MM''''''''''''MM
&&WW''''''IIWWWWWWWWWW''''''MMWWWW''''''''''''''''''''aaWW::^^WWWWWW&&''''TTWWWW''''''''''''''>>WWWWWWWWWWNN''''''''''''''NN,,''WWWW''''WWWW''''''''&&WWNN''''WWWWWW''''''__
''WWMM''''''WWWWWWWWWWWWmm''''jjWWWWVV''''''''''00WWWWWWWWNNWWWWWW;;''''MMWWGG''''''''''''''''''''''IIWWWWWWWWWWDD''''''''WW''''WW&&''''WWWW&&''''''''WWWW''''WWWWWWMM''''''
''WWWW''''''00WWWWWWWWWWWWWW''''''NNWWWW++MMWWWWWWWWCC''''''WWRR''''FFWWWW''''''''''''''''''''''''''''''''ggWWWWWWWWxx'',,NN''NNWW''''<<WWWWWW''''''''WWWWdd''rrWWWWWW''''''
''''WWRR''''''WWWWWW''NNWWWWWWRR''''<<WWWWWWWWrr''''''''__NN''''''WWWWhh''''''''''MM''''MM''''''''''''''''''''''NNWWOO''MM''''WWWW''''WWWWWW**LL''''''--WWWW''''WWWWWWgg''''
''''WWWW''''''MMWWWW''''^^WWWWWWWW!!''''''''''''''++WWWWWWuu''aaWWWW''''''''''hhWWWW'''';;00''''''''''''''''''''''''__''WW'';;WWRR''''WWWWWW''''''''''''WWWW++''66WWWWWW''''
''''iiWWFF''''''WWWW00''''''&&WWWWWWBB''''''UUWWWWWWWWWWWWNNWWWWoo''''''''''WWRRrrWWRR''''WW'''''''''''''''''''''''''';;NN''WWWW''''11WWWWWW''WW^^''''''xxWWWW''''WWWWWWTT''
''''''WWWW''''''WWWWWW''''''''__WWWWWWWWWWWWWWWWWWWWWWNN,,;;MM''''''''''ddWW''''''WWWW''''VVnn''''''''YYWW^^''''''''''MM''''WWWW''''WWWWWWWWWWWWWW''''''''WWWW''''NNWWWWWWdd
''''''ggWW;;''''LLWWWWWWFF''''''''QQWWWWWWWWWWWWGG''''''''''''''''''''WWmm''''''''HHWWYY''''WW''''''''''WWWWWWNN''''''DD''((WWgg''''WWWWWWWWWWWWWW$$''''''DDWWMM''''WWWWWWWW
**''''''WWWW''''''WWWWWWWWWW''''''''''WWWWYY''''''''''''''''''''''DDWW''''''==WW''''WWWW''''&&__''''''''''''00WWWWWWRR00''WWWW''''jj''''''''''''ssWW11''''''WWWW''''WWWWWWWW
WW''''''MMWW''''''KKWWWWMMNNWWhh''''''''''''''''''''''VV''''''::WWqq''''''NNWWWWMM''NNWW,,''''WW'''''''''''''''',,MMWW''''WWWW''''''''''''''''''''aaWW''''''MMWWRR'';;WWWWWW
WW''''''''WWBB''''''WWWWWW''!!WWWW''''''''''''''RRWWWWMM''''00WW''''''))WWWW##''WW''''WWWW''''WW''''''''''''''''''''''''IIWWOO''''''''''''''''''''''ddWW''''''WWWW''''WWWWWW
WWMM''''''WWWW''''''MMWWWW''''''00WWbb'';;MMWWWWWW22''''!!WWZZ''''''MMWWWW''''''00RR''WWWW''''--&&''''''''''WWTT''''''''WWWW''''@@WWWWWWWWWWWW__''''''88NN''''WWWWnn''IIWWWW
WWWW''''''>>WWPP''''''WWWWNN''''''::WWWWWWWW11''''''''&&WW''''''YYWWWWOO''''''''''WW''\\WW00''''WW''''''''''WWWWWWWW;;;;WWWW''WWWWWWWWWWWWWWWWWW''''''''&&%%''rrWWWW''''WWWW
WWWWRR''''''WWWW''''''WWWWWWBB''''''''''''''''''''''nnff''''''MMWWWW''''''''''''''WWYY''WWWW''''yyee''''''''jjWWWWWWWWWWWWpp!!''''''''''''''^^WWWW''''''''NN__''WWWW__''00WW
WWWWWW''''''PPWW<<''''\\WWWWWWWW<<''''''''''''''VVMM''''''IIWWWWaa'''''''';;MM'''',,WW''44WWII''''WW''''''''''''kkWWWWWWbb''''''''''''''''''''**WWWW''''''''MM''EEWWWW''''WW
WWWWWWff''''''WWWW''''''WWWWWWWWWWNN''''''RRWWWWWW''''''WWWWWW''''''''''&&''NN''''''WW,,''WWWW''''RR!!''''''''''''''''00''''''''''''''''''''''''YYWWWW''''''''MM==WWWW''''WW
BBWWWWWW''''''BBWW''''''33WWWWWWWWWWWWWWWWWWWWWWWW++PPWWWWFF''''''''\\WWWW''''RR''''YYWW''BBWW;;''''WW'''''''''''''''''''''',,<<FF88WWWWWW''''''''ZZWWWW''''''''''WWWWBB'';;
''WWWWWW__''''''WWMM''''''WWWWWW''BBWWWWWW&&rrWWWWWWWWMM''''''''''NNWWWWWW''''WW''''''WW''''WWWW''''MM''''__''''''''''GGWWWWWWWWWWWWWWWWWWWW''''''''OOWWWW''''''''MMBBWW''''
''WWWWWWWW''''''WWWW''''''BBWWWW''''''''''''''''WWWWWW''''''''**WWWWMM''WWBB''!!YY''''RR00''WWWW''''''NN''''''''''''''WWWWWWWWWWWWWWWWWWWWWWWW''''''''$$WWWWBB''((11''WW44''
''::WWWWWW'''''';;WW##''''''WWWW&&''''''''''''''jjWWWW{{''''MMWWWWii''''^^WW''''WW''''''WW'';;WWBB''''WW''''!!''''WWWWWWWWWWWWWWWWWWWWWWWWWWWWWW''''''''''WW^^''MM''''''WW&&
''''WWWWWWBB''''''WWWW''''''WWWWWW''''!!WW00''''''GGWWWW00WWWWMM''''''''''WWkk''ee,,''''MMII''WWWW''''LLXX''''''''''''''''''''''''''''''00WWWWWWWW''''''''WW''''WW''''''WWWW
VV''YYWWWWWW''''''FFWWcc''''__WWWW''++WWWWWWpp''''''NNWWWWWW11''''''BB''''hhWW''''WW''''''WW''VVWW33''''WW''''--''''''''''''''''''''--''''NNWWWWWWNN''''XXWW''''WW''''''WWWW
''''''WWWWWWww''''''WWWW''''''OO''''''RRWWWWWWYY''''''WWWW&&''''''''WW''''''WW\\''&&''''''WW;;''WWWW''''gg<<''''''WWWWWWWWWWWWWWWWWWWW##''''MMWWWW++''''WWWW''''BB''''JJWWYY
''!!''QQWWWWWW''''''00WW''''''''''''''''DDWWWWWW^^''''''WWWW''''''''WW%%''''BBWW''''00''''jjWW''MMWWJJ''aaWWppMMWWWWWWWWWWWWWWWWWWWWWWWWpp''''MMWW''''''WW00''tt\\''''MM&&''
;;WW''''WWWWWW\\''''''WW00wwWWWW''''''''''KKWWWWWW''''''--WWWW''''''BBWW''''''WW::''WW==<<00WWWWWWWWWWWWWWWWWWWW&&%%**__''''''''''''IIWWWWCC''''WW''''''WW;;''MM''''''WW^^''
88WWff''MMWWWWWW''''''''''**WWWWWW''''''''''OOWWWWWW''''''YYWWgg''''bbWWBBMMWWWWWWWWWWWWWWWWNNII!!''''''''''''''''''''''''''''''''''''UUWWWWYY''WW''''--WW''''WW''''''WW''''
MMWW''''''WWWWWW''''WWUU''''''WWWWWW!!''''''''PPWWWWWW''''''DDWWWWWWWWWWWWRRtt__''''''''''''''''''''''''''''''''''''''''''''''''''''''''mmWWWWWWNN''''mmWW''''WW''''''WW''JJ
WWWW''''77WWNN''''''00WWMM''''''MMWWWWYY''''''''ZZWWWWWW''''''MMWW''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''00WWWW>>''''WWWW''''00''''nnWW''MM
WWWW''''MMZZ\\''''''''11WWWW''''''00WWWWHH''''''''IIWWWWNN''''''WW&&'''''''''''''''''''''';;ll&&WWWWWWWWWWWWBB!!ttddMMWWWWWWWWWWWW''''''''''UUWW''''''WWmm''oo;;''''WWRR''WW
WWWW''''BB''WWgg''''''''''WWWWii''''nnWWWWBB''''''''yyWWWWRR''''''WWtt''^^ZZMMWWWWWWWWWWWWWWWWWWWWWWWWNNII!!JJWWWWWWWWWWWWWWWWWWWWWW''''''''MMWW''''''WW--''WW''''''WW;;''WW
WWuu''''''''WWWW''''''''''''##WW00''''--WWWWMM''''''''TTWWWWAA'''';;WWWWWWWWWWWWWWWW00xx__''''''''''''''''''''''''''''''''''''''==WWMM''''''WWWW'''';;WW''''WW''''''WW''''WW
WW''''''''''WWWW''''''''''''''!!WWWW''''''WWWWWW''''''''vvWWWWJJ''''IIWW;;''''''''''''''''''''''''''''!!ooBB''''''''''''''''''''''jjWWMM''''WW&&''''00WW''''WW''''''WW''uuWW
WW''''MM''''WWWW''''''''''''''''''MMWW;;''''NNWWWW''''''''rrWWWW!!''''00YY''''''''''>>44MMWWWWWWWWWWWWggjj,,'''',,>>ooRRWWWWWW''''''nnWW!!''WW!!''''WWWW''''gg''''aaWW''WWWW
WW''ZZWW''''WWWW''''''''WW''''''''''ppWWUU''''PPWWWW<<''''''^^WWWW''''''MMWWWWWWWWMMXXrr''''''''''''''''''''FFWWWWWWWWWWWWWWWWWW''''''33''yyWW''''''WWXX''hh::''''WWKK''WWWW
MM''WWWW''''WWWW''''''>>WW''''''''''''::WWMM''''==WWWWII''''''!!WWWW''''''WW''''''''''''''''''''''''''''''''99WWWWWWWWWWWWWWWWWWWW''''''''WWWW''''''WW''''WW''''''WW,,''WWWW
WWWWWWWW''__WWWW''''''EEWW''''dd''''''''''MMWW''''''WWWW##''''''__WWWW''''''44''''''''''''''''''''''''==hhMM!!''''''''''''''CCWWWWWW''''''WWWW''''^^WW''''WW''''''WW''''WWWW
mmWWWWWW''YYWWRR''''''WWWW''''WWWW''''''''''%%WWTT''''MMWWNN'''''',,WWWW''''==!!''''??KKWWWWWWWWWWWWWWWWWWWW''''''''''''''''''ppWWWWWW''''WWRR''''BBWW''''WW''''''WW''ZZMMYY
NNWWWWpp''&&WWLL''''''WWWW''''WWWW##''''''''''''WW00''''$$WWWW''''''''WWNN''LLWW**WWWWWWWWBBFF;;''''''''''''''''''''''''''''''''$$WWWWMMllWW;;''''WWWW'',,99''''OOWW''WW''''
WWWWWWrr''WWWW,,''''''WWMM''''WWWW++''''''''''''''NNWW''''JJWWWW''''''''WWWWWW''''''''''''''''''''''--JJRRWW''''''''''''''''''''''00WWWWWWWW''''''WWCC''bb''''''WWPP''==''!!
WWWWWW''''WWWW''''''''WWCC''''WWWW''''''''''''''''''nnWW;;''''WWWW,,''''--WW\\''''''yyBBWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW''''''''''BBWWWWWW''''''WW''''WW''''''WW''''''''ee
WWWWWW''''WWWW''''''''WW!!''''WWWW''''''''WWLL''''''''''WWPP''''WWWW++''##KK''''''''00WWWWWWWWWWWWWWWWWWMM33hhWWWWWWWWWWWWWW''''''''''MMWWWW''''rrWW''''WW''''''WW''''''''MM
WWWWWW''''WWWW''''''''WW''''''WWWW''''''''WWWW''''''''''''BBMM''''&&WWWWMM'''''''']]WWNNFF;;''''''''''''''''''WWWWWWMMMMWWWWWW''''''''''WWGG''''NNWW''''WW''''__WW''''''''WW
WWWWWW''''WWWW''''''''WW''''^^WWWW'''''';;WWWW''''''''''''''LLWW''''GGWW''''''''--WWWWKK''''''''''''''''''''''''''''''''NNWWWWWW''''''''''''''''WWWW'';;CC''''$$WWNN''''''WW
WWWWWW''''WWWW''''''**WW''''aaWWWW''''''ffWWWW''''''''''''''''''WWyyMM;;''''''''WWWWWWrr''''''''\\22MMWWWWWWWW''''''''''''MMWWWWWW''''''''''''''WWyy''QQ''''''WWWWWW''''''WW
WWWWWW'';;WWWW''''''KKWW''''MMWWWW''''''BBWWWW''''''''''''''''''''WWXX''''''''WWWWWWii''''::WWWWWW00YYWWMM''''''''''''''''''WWWWWWWW''''''''''''WW''''WW''''''%%WWWW''''''WW
WWWWMM''ooWWKK''''''WWWW''''WWWWWW''''''IIWWWWMM''''''''<<''''''''MM''''''''MMWWWWVV''''''''''''''''''''WW''''''''''''''''''''WWWWWWMM''''''''LLWW''''WW''''''''WWWW''''''WW
WWWW33''NNWW**''''''WWWW''''WWWWMM''''''''@@WWWW00''''''''''''''WW''''''''RRWWWWXX''''''''xxII''''''''''NNxx''''XXWWgg''''''''''WWWWWWoo''WW!!MMWW''''WW''''''''WWRR''''''WW
WWWW\\''WWWW''''''''WWWW''''**WWWWRR''''''''NNWWWWww''''''''''00''''''''IIWWWWgg''''''''nnWWWW''''''''''''WW''''''''WWEE''''''''''WWWW''''WWWWWWMM''!!ll''''''''WW77''''==WW
WWWW''''WWWW''''''''IIWWjj''''33WWWW%%''''''''WWWWWW))''''''<<VV''''''!!WWWW00''''''''VVWWWWWW''''''''''''KKVV''''''''WWVV''''''''MMWW''''00WWWWLL''&&''''''''--WW,,''''44WW
WWWW''''WWWWmm''''''''##WW::''''00WWWW11''''''''WWWWFF''''''NN''''''''WWWWNN''''''''33WWWWWW''''''''''''''''WW''''''''''WWxx''''''WWWW,,''''WWWW''''WW''VV''''iiWW''''''MMWW
WWWWZZ''''WWWWnn''''''''NNWW''''''MMWWWW''''''''''NN''''''MM''''''''WWWWMM''''''''EEWWWWMM''''''tt11''''''''YYqq''''''''''WW''''''ggWWBB''''WWWW''''WWUUFF''''00WW''''''WWWW
WWWWWWrr'',,WWWW^^''''''''WWWW''''''WWWWWW''''''''''''''33''''''''WWWWMM''''''''GGWWWW00''''''ggWWMM''''''''''WW''''''''mmWW''''''''WWWW''''WWWW''''WWWW;;''''WWWW''''''__WW
WWWWWWWW**--WWWWWWrr''''''ggWWWW''''RRWWWWWW--''''''''++WW--''''BBWWWWdd''''''##WWWWWWJJ''''MMWWWWaa''''''''''MMRR'''';;WWWWMM''''rrWWWWJJ''WWWW''OOWWWW44'',,WWWWRR''''::
```