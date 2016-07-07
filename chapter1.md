---
title       : Tidy Data in Python
description : It is often said that data scientists spend only 20% of their time analyzing their data, and 80% of time cleaning it. Indeed, maintaining a tidy, easy-to-use dataset is crucial in our age of big data. In the paper Tidy Data, veteran statistician Hadley Wickham gives definitions of tidy and messy data so that all data scientists can keep their work organized. In this mini-course, you'll learn to transform messy datasets to tidy datasets using the pandas package in python. Let's get started!

attachments :

--- type:MultipleChoiceExercise lang:python xp:50 skills:1 key:7ad68bd87f
## Tidy Data and Messy Data

What exactly marks the difference between *tidy* data and *messy* data? It is not only how organized and intuitive the datasets look in our human eyes, but also how easily and efficiently they can be processed by computers. In his seminal paper [Tidy Data](https://www.jstatsoft.org/article/view/v059i10), Hadley Wickham proposed three standards for tidy data:

1. Each variable forms a column
2. Each observation forms a row
3. Each type of observation forms a unit.

In this course, we'll focus on the first two rules and show you how we can use the Python package [pandas](http://pandas.pydata.org/) to deal with datasets violating them. To get started, execute `messy` in the IPython shell. This dataset, which appears in Wickham's paper, shows the number of people who choose either of two treatments in a hospital. Observe its struture in comparison with Wickham's rules. This dataset is *messy* because it violates rule #2: it combines Treatment A and Treatment B, two distinct observations, in a single row. 

Now let's look at two more datasets. Execute `df1` and `df2` in your IPython shell to check out two other preloaded datasets, both featured in DataCamp's [*Cleaning Data in R*](https://campus.datacamp.com/courses/cleaning-data-in-r) course. The former shows the type and number of pets owned by three co-workers, and the latter shows the average BMI in three countries over several years. Which one of these datasets is messy, and why?

*** =instructions
- df1 is messy because it violates rule #1.
- df1 is messy because it violates rule #2.
- df2 is messy because it violates rule #2.
 
*** =hint
What are the observations and variables in these two datasets?

*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace.
import pandas as pd
url1 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/df1.csv'
url2 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/df2.csv'
url3 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/messy.csv'

df1 = pd.read_csv(url1, sep = ',')
df2 = pd.read_csv(url2, sep = ',')
messy = pd.read_csv(url3, sep=',')
```

*** =sct
```{r}
# SCT written with pythonwhat: https://github.com/datacamp/pythonwhat/wiki

msg_1 = "In `df1`, `dogs`, `cats`, `birds` are each a variable."
msg_2 = "The three people in `df1` represent three different observations."
msg_3 = "Exactly! See deatailed explanation in next exercise."
test_mc(3, [msg_1, msg_2, msg_3])
```

--- type:NormalExercise lang:python xp:100 skills:1 key:431ad8bd98
## Using Melt to Tidy Data

In `df2`, the years `1980`, `1981`, `1982`, and `1983` mark the years when BMI is observed. Thus, they represent three different observations and should be seperated in three rows. A great tool to achieve this is the melt function in the pandas package. Its basic syntax is `pd.melt(df, id_vars=l)`, where `df` is the name of the dataframe we're dealing with and `l` is a list of all the columns that we want to keep as columns. All the other columns will be "molten" together in different rows. To get a more concrete idea, try `melt` yourself to *tidy* the dataset `df2`!

*** =instructions
- Import `pandas` using the alias `pd`.
- Melt `df2`! We want to maintain the `Country` column and melt all the rest.
- Click "Submit" to print out the new *tidy* DataFrame.

*** =hint
- To import package x with the alias y, use the command `import x as y`.
- `id_vars` should be `['Country']`.
- You don't need to change the code we provided for you.

*** =pre_exercise_code
```{python}
import pandas as pd
url2 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/df2.csv'
df2 = pd.read_csv(url2, sep = ',')
```

*** =sample_code
```{python}
# Import pandas as pd


# Melt df2 into new dataframe: df2_tidy
df2_tidy = ____

# print df2_tidy
print(df2_tidy)

```

*** =solution
```{python}
# Import pandas as pd
import pandas as pd

# Melt df2 into new dataframe: df2_tidy
df2_tidy = pd.melt(df2, id_vars=['Country'])

# print df2_tidy
print(df2_tidy)

```

*** =sct
```{python}
test_import("pandas")
test_correct(
    lambda: test_object("df2_tidy"),
    lambda: test_function("pandas.melt")
)
success_msg("Great job!")
```

--- type:NormalExercise lang:python xp:100 skills:1 key:3be71779cd
## Renaming Columns

Did you see how easy it was? In one command you already tidied up your dataset! Now we just need a bit further fine-tuning. Change the column names with pandas' rename function. Its syntax is `df.rename(columns = d, inplace = True)`, where `d` is a dictionary where the keys are the columns you want to change, and the values are the new names for these columns. The code `inplace = True` means the result would be stored in the original DataFrame instead of a new one.


*** =instructions
- Rename the `variable` of df2_tidy to `Year` and `value` to `Income`.
- Click "Submit Answer" to print out the new DataFrame.

*** =hint
- Here `d` should be `{'variable':'Year','value':'Income'}`.
- You don't need to change the code we provided for you.

*** =pre_exercise_code
```{python}
#import pandas
import pandas as pd
url2 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/df2.csv'
df2 = pd.read_csv(url2, sep = ',')
df2_tidy = pd.melt(df2, id_vars=['Country'])
```

*** =sample_code
```{python}
# Import pandas
import pandas as pd

# Rename the columns of df2_tidy


# Print out df2_tidy again
print(df2_tidy)

```

*** =solution
```{python}
# Import pandas
import pandas as pd

# Rename the columns of df2_tidy
df2_tidy.rename(columns={'variable': 'Year', 'value': 'Income'}, inplace=True)

# Print out df2_tidy again
print(df2_tidy)
```

*** =sct
```{python}
test_import("pandas")
test_correct(
    lambda: test_object("df2_tidy"),
    lambda: test_function("df2_tidy.rename")
)
success_msg("Great job!")
```



--- type:MultipleChoiceExercise lang:python xp:50 skills:1 key:d40684ea0d
## More messiness

Great job! Now that you're familiar with messy and tidy data, take a look at another dataset. Exectue `eyes` in your shell to print a dataset that featured in DataCamp's [Cleaning Data in R course](https://campus.datacamp.com/courses/cleaning-data-in-r). This dataset is about the eye colors of three women and whether they wear glasses. What problem does this dataset have?

*** =instructions
- It violates rule #1 of tidy data: there are several columns that represent the same variable.
- It violates rule #1 of tidy data: there are several variables represented in the same column.
- It violates rule #2 of tidy data: there are several rows that represent the same observation.
- It violates rule #2 of tidy data: there are several observations represented in the same row.

*** =hint
Think about what the chart wants to show and how the columns relate to it!

*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

import pandas as pd
url4 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/eyes.csv'
eyes = pd.read_csv(url4,sep=',')

```

*** =sct
```{r}
# SCT written with pythonwhat: https://github.com/datacamp/pythonwhat/wikif

msg_2 = "The columns do not represent more than one variable"
msg_3 = "Each person is one observation and is correctly charted as one observation"
msg_success = "Exactly!"
test_mc(1, [msg_success, msg_2, msg_3, msg_3])
```

--- type:NormalExercise lang:python xp:100 skills:1 key:5d0f6f3efd
## Deal with it!

The three columns, `Black`, `Blue`, and `Brown`, essentially represent the same variable: eye color. It would make much more sense to merge them into one column. Use `melt` to do it!

*** =instructions
- Use `Melt` to leave `Names` and `Wear_Glasses` intact and combine everything else.
- Rename the `variable` column to `Eye_Color`.
- Hit "Submit Answer" to print out the resulting dataframe.

*** =hint
- The basic syntax for melt is `df.melt(df, id_vars=l)`. Here `l` should be `['Name', 'Wear_Glasses']`.
- The basic syntax for rename is  `df.rename(columns = l, inplace = True)`.
- You don't need to change the code we provided for you.


*** =pre_exercise_code
```{python}
import pandas as pd
url4 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/eyes.csv'
eyes = pd.read_csv(url4,sep=',')
```

*** =sample_code
```{python}
# Import pandas
import pandas as pd

# Melt the Black, Blue, and Brown columns of eyes and save it to new dataframe: eyes_tidy
eyes_tidy = ____

# Rename the variable column


# print out eye_color_tidy
print(eyes_tidy)

```

*** =solution
```{python}
# Import pandas
import pandas as pd

# Melt the Black, Blue, and Brown columns of eyes and save it to new dataframe: eyes_tidy
eyes_tidy = pd.melt(eyes, id_vars=['Name', 'Wear_Glasses'])

# Rename the `variable` column
eyes_tidy.rename(columns={'variable': 'Eye_Color'}, inplace=True)

# print out eye_color_tidy
print(eyes_tidy)

```

*** =sct
```{python}
test_import("pandas")
test_correct(
    labmda: test_object("eyes_tidy"),
    lambda: test_or(
       lambda: test_function(pandas.melt),
       lambda: test_function(rename)
    )
)
success_msg("Great job!")
```

--- type:NormalExercise lang:python xp:100 skills:1 key:99639b8387
## Further Cleaning

What did you notice? While the three columns melt into one, the dataset still has some problems. First of all, when we know Elizabeth has brown eyes, it's redundant to keep record that she doesn't have blue or black eyes. Therefore, what we want to do is to get rid of all rows whose value in the `value` column is 0. It is very easy to do so in pandas, just use the following command:

`df = df[df.column == value]`

where `column` is the name of the column we are examining and `value` is the value we want to keep. This step will give us one row for each girl that tells us only her correct eye color. Now the `value` column is no longer necessary and let's delete it:

`df.drop(l, axis=1)`

Here `l` is a list of the columns we want to get rid of, and `axis=1` specifies that we want to drop columns instead of rows.


*** =instructions
- Filter the dataset to keep only the rows where `value` is 1. 
- Delete the `value` column.

*** =hint
- To filter the dataset, you should have `df.column == 1`.
- To drop the `value` column, you should have the argument `(['value'], axis=1)`.

*** =pre_exercise_code
```{python}
import pandas as pd
url4 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/eyes.csv'
eyes = pd.read_csv(url4,sep=',')
eyes_tidy = pd.melt(eyes, id_vars = ['Name', 'Wear_Glasses'])
eyes_tidy.rename(columns = {'variable':'Eye_Color'}, inplace = True)
```

*** =sample_code
```{python}
#import pandas
import pandas as pd

# Filter eye_color_tidy 
eyes_tidy = ____

# Delete the `value` column
eyes_tidy = ____

# print eyes_tidy again
print(eyes_tidy)
```

*** =solution
```{python}
#import pandas
import pandas as pd

# Filter eyes_tidy 
eyes_tidy = eyes_tidy[eyes_tidy.value == 1]

# Delete the `value` column
eyes_tidy = eyes_tidy.drop(['value'], axis=1)

# print eye_color_tidy again
print(eyes_tidy)
```

*** =sct
```{python}
test_import("pandas")
#test_function("drop")
test_data_frame("eyes_tidy", columns = ["Name", "Eye_Color"])
#test_object("eyes_tidy.shape")
success_msg("Great job!")
```

