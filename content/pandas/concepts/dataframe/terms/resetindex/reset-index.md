---
Title: '.reset_index()'
Description: 'This article is about how the .reset_index() is used in pandas dataframes.'
Subjects: 
  - 'Data Science'
  - 'Pandas'
Tags:
  - 'Methods'
  - 'Pandas'
  - 'Data Science'
CatalogContent:
  - 'learn-python'
  - 'paths/data-science'
---
This article is about how the **.reset_index()** is used in pandas dataframes.


## Syntax
```py
import pandas as pd
df.read_csv('some_csv.csv', index_col = 'Account Number')
df.reset_index()
```


### What Is .reset_index() 
Sometimes there is a need to modify a dataframe object to better meet a certain use case. When these modifications are applied they often leave smaller dataframes with indexes that are messy and not continuous.
Resetting the index with .reset_index() fixes these issues.


### Actions Which Cause Indexing Issues 
Common examples include but are not limited to:

- Changing the order of columns.
- Using a column or multiple columns of the database as an index instead of the default index pandas provides and then later needing a numbered index.
- Filtering out certain rows of the dataframe based on the value of a column of data.
- Changing the order of rows of data by sorting those rows by the values of a certain column of data such as Date or Employee ID Number.
- Adding columns and or rows of data to the dataframe that were not present in the original dataframe.


### .reset_index() Parameters
The .reset_index() method provides many parameters which allow for more precision when resetting a dataframe index. The following parameters will be used in the examples later in this article.

- *drop:* The drop parameter can be set to True or False and is set to False by default. When this parameter is set to True it replaces the previous dataframe index with the new index provided by .reset_index() otherwise it sets the new index in front of the old index.
- *inplace:* The inplace parameter can be set to True or False and is set to False by default. When this parameter is set to True it applies all changes .reset_index() makes to the current instance of the dataframe otherwise it creates a new dataframe instance with the changes applied to that dataframe.


## Examples
In the following examples imagine working on a project about dogs and wanting to use data from an animal shelter about dogs in that shelter but the data in the .csv file has data about cats and dogs.
To follow along a copy of the [Austin_Animal_Center_intakes.csv](https://www.kaggle.com/datasets/jackdaoud/animal-shelter-analytics) can be downloaded from Kaggle.

## Example Of The Original Dataframe
```py
import pandas as pd

df = pd.read_csv('Austin_Animal_Center_intakes.csv').head()
pd.set_option('display.max_columns', None)
print(df)
```

## Output
```shell

  Animal ID          Name                DateTime     MonthYear  \
0   A786884        *Brock  01/03/2019 04:19:00 PM  January 2019   
1   A706918         Belle  07/05/2015 12:59:00 PM     July 2015   
2   A724273       Runster  04/14/2016 06:43:00 PM    April 2016   
3   A857105  Johnny Ringo  05/12/2022 12:23:00 AM      May 2022   
4   A682524           Rio  06/29/2014 10:38:00 AM     June 2014   

                        Found Location    Intake Type Intake Condition  \
0  2501 Magin Meadow Dr in Austin (TX)          Stray           Normal   
1     9409 Bluegrass Dr in Austin (TX)          Stray           Normal   
2   2818 Palomino Trail in Austin (TX)          Stray           Normal   
3   4404 Sarasota Drive in Austin (TX)  Public Assist           Normal   
4        800 Grove Blvd in Austin (TX)          Stray           Normal   

  Animal Type Sex upon Intake Age upon Intake  \
0         Dog   Neutered Male         2 years   
1         Dog   Spayed Female         8 years   
2         Dog     Intact Male       11 months   
3         Cat   Neutered Male         2 years   
4         Dog   Neutered Male         4 years   

                                   Breed         Color  
0                             Beagle Mix      Tricolor  
1               English Springer Spaniel   White/Liver  
2                            Basenji Mix   Sable/White  
3                     Domestic Shorthair  Orange Tabby  
4  Doberman Pinsch/Australian Cattle Dog      Tan/Gray
```

## Example Removing Cats From Dataframe

```py
import pandas as pd

df = pd.read_csv('Austin_Animal_Center_intakes.csv').head()
pd.set_option('display.max_columns', None)

#this section of code removes the furball from our dog dataframe
df = df[df['Animal Type'] != 'Cat']

#uncommenting the line below this line will remove the index of the original dataframe and reset the order
#df.reset_index(inplace = True, drop = True)
print(df)
```

## Output without df.reset_index(inplace = True, drop = True)
```shell

  Animal ID     Name                DateTime     MonthYear  \
0   A786884   *Brock  01/03/2019 04:19:00 PM  January 2019   
1   A706918    Belle  07/05/2015 12:59:00 PM     July 2015   
2   A724273  Runster  04/14/2016 06:43:00 PM    April 2016   
4   A682524      Rio  06/29/2014 10:38:00 AM     June 2014   

                        Found Location Intake Type Intake Condition  \
0  2501 Magin Meadow Dr in Austin (TX)       Stray           Normal   
1     9409 Bluegrass Dr in Austin (TX)       Stray           Normal   
2   2818 Palomino Trail in Austin (TX)       Stray           Normal   
4        800 Grove Blvd in Austin (TX)       Stray           Normal   

  Animal Type Sex upon Intake Age upon Intake  \
0         Dog   Neutered Male         2 years   
1         Dog   Spayed Female         8 years   
2         Dog     Intact Male       11 months   
4         Dog   Neutered Male         4 years   

                                   Breed        Color  
0                             Beagle Mix     Tricolor  
1               English Springer Spaniel  White/Liver  
2                            Basenji Mix  Sable/White  
4  Doberman Pinsch/Australian Cattle Dog     Tan/Gray
```

The indexing now jumps from two to four after the row containing the cat is removed. This can become very messy when dealing with large dataframes containing hundreds or even thousands of rows.


## Output With df.reset_index(inplace = True, drop = True)
```
  Animal ID     Name                DateTime     MonthYear  \
0   A786884   *Brock  01/03/2019 04:19:00 PM  January 2019   
1   A706918    Belle  07/05/2015 12:59:00 PM     July 2015   
2   A724273  Runster  04/14/2016 06:43:00 PM    April 2016   
3   A682524      Rio  06/29/2014 10:38:00 AM     June 2014   

                        Found Location Intake Type Intake Condition  \
0  2501 Magin Meadow Dr in Austin (TX)       Stray           Normal   
1     9409 Bluegrass Dr in Austin (TX)       Stray           Normal   
2   2818 Palomino Trail in Austin (TX)       Stray           Normal   
3        800 Grove Blvd in Austin (TX)       Stray           Normal   

  Animal Type Sex upon Intake Age upon Intake  \
0         Dog   Neutered Male         2 years   
1         Dog   Spayed Female         8 years   
2         Dog     Intact Male       11 months   
3         Dog   Neutered Male         4 years   

                                   Breed        Color  
0                             Beagle Mix     Tricolor  
1               English Springer Spaniel  White/Liver  
2                            Basenji Mix  Sable/White  
3  Doberman Pinsch/Australian Cattle Dog     Tan/Gray
```

After applying df.reset_index(inplace = True, drop = True) the dataframe index order is now neat and continuous for easy indexing.
Sorry, Johnny Ringo dogs are just cooler than cats!