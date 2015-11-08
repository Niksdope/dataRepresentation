## Project for Data Representation and Querying 2015
### Overview
This is an API created for the request from Apps4gaps, using their dataset regarding the number of students enrolled in full-time first/second/third year education as well as post leaving-cert courses from 1966 up until 2015. Below is a pdf and json page of the data.

- **[PDF](http://www.cso.ie/webserviceclient/JSON-stattotable.aspx?tableid=EDA37)**
- **[JSON](http://www.cso.ie/StatbankServices/StatbankServices.svc/jsonservice/responseinstance/EDA37)**


### Data
The dataset is divided into four columns; Level of Education, Year, Statistic and Value. Let's take a look at 5 random rows from the dataset:

Level of Education | Year | Statistic | Value
-------------------|------|-----------|------ 
All levels of education | 2015 | Enrolments of Full-Time Students (No.) | 1090641
First level | 1982 | Enrolments of Full-Time Students (No.) | 556034
Second level | 1993 | Enrolments of Full-Time Students (No.) | 337289
Third level | 2004 | Enrolments of Full-Time Students (No.) | 133887
Post leaving certificate courses (VPT2) | 2000 | Enrolments of Full-Time Students (No.) | 24337


The first row of the dataset is a *header row* with the names for each field. Analysis of the other rows shows that

1. **Level of Education** states whether the data concerns the sudents in First level education, Second, Third, Post leaving-cert or All levels together (total).

1. **Year** shows what year the data is talking about. 

1. **Statistic** is more of a filler column, making the dataset more easily readable and finally the 

1. **Value** column regards how many students were enrolled in the specific level of education that year.


### Design
The aim of this API is to provide efficent access of the data provided by the dataset. This will be achieved by a number of carefully thought out *URLs* that allow any part of the data to be accessed. In the JSON file of the dataset, it is visible that all the levels of education and years have unique indexes to uniquely identify every piece of data.


The levels of education are indexed as follows:
- " - " denotes All levels of education
- " 104 " denotes First level
- " 23 " denotes Second level
- " 4 " denotes Third level
- " X45 " denotes Post leaving certificate courses (VPT2)


A URL to return a list of all years and their values for a particular level of education would look like this [https://educationapi.com/level/[level]]()

and would return a list of JSON (JavaScript Object Notation) objects
```json
{
  "level" : "First level",
  "year" : 1982,
  "value" : 556034
}
```
