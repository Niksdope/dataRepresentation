## Project for Data Representation and Querying 2015
### Overview
This is an API created for Apps4gaps using their dataset regarding the number of students enrolled in first/second/third year education from 1966 up until 2015. Below is a pdf and json page regarding the data.

**[PDF](http://www.cso.ie/webserviceclient/JSON-stattotable.aspx?tableid=EDA37)**
**[JSON](http://www.cso.ie/StatbankServices/StatbankServices.svc/jsonservice/responseinstance/EDA37)**

### The dataset

The dataset is divided into four columns; Level of Education, Year, Statistic and Value. Let's take a look at 4 random rows from the dataset:

Level of Education | Year | Statistic | Value
-------------------|------|-----------|------ 
All levels of education | 2015 | Enrolments of Full-Time Students (No.) | 1090641
First level | 1982 | Enrolments of Full-Time Students (No.) | 556034
Second level | 1993 | Enrolments of Full-Time Students (No.) | 337289
Third level | 2004 | Enrolments of Full-Time Students (No.) | 133887


Analysis of these rows shows that **Level of Education** does what it says, states whether the data is about First level education, Second, Third or All levels together (total). The **Year** column shows what year the data is talking about. **Statistic** is more of a filler column, making the dataset more easily readable and finally the **Value** column regards how many students were enroled in the specific level of education that year.

### Niks Gurins G00315379 October 19/2015

```c
int i;
for(i = 0; i < 10; i++)
{
  printf("well  %d", i);
}
```
