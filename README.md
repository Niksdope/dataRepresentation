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
- **" - "** denotes All levels of education
- **" 104 "** denotes First level
- **" 23 "** denotes Second level
- **" 4 "** denotes Third level
- **" X45 "** denotes Post leaving certificate courses (VPT2)


####*GET method* - requests data from a dataset using specific URLs
A URL to return a list of all years and their values for a particular level of education would look like this [https://educationapi.com/level/[level]]()

e.g. [https://educationapi.com/level/-]() and would return every year of students enrolled for all levels of education together.

The actual JSON response for this would be
```json
{
  "id" : "-",
  "year" : ["1966", "1967", "1968", "1969", "1970", "1971", "1972", "1973", "1974", "1975", "1976", "1977", "1978"...],
  "value" : ["638298","652844","670382","692860","712928","732214","750979","768789","786541","803503","828019","848025"...]
```


A URL to return a list of all different education levels for a particular year and their values [https://educationapi.com/year/[year]]()

e.g. [https://educationapi.com/year/1966]() would return every level of education students have enrolled for 1966.

JSON returned from this URL would looke like this
```json
{
  "year" : 1966,
  "id" : [ "-", "104", "23", "4", "X45" ],
  "value" : [ "638298", "481095", "138754", "18449", "0" ]
}
```


The URL to get a a single row returned from the entire dataset would have to be:
[https://educationapi.com/level/[level]/year/[year]](). Using this kind of URL would be very useful for accessing very specific information.

e.g. [https://educationapi.com/level/23/year/2015]() 

The JSON returned from this URL would be 
```json
{
  "id" : "23",
  "year" : "2015",
  "value" : "544696"
}
```

####*POST method* - submits data to be processed to the dataset using a URL


The *Post* method sends a request to the server to update or add new values to the dataset.
An example post request to the server would look like this.
```http
POST /request HTTP/1.1
Accept: application/jsonrequest
Content-Encoding: identity
Content-Length: 28
Content-Type: application/jsonrequest
Host: json.educationapi.com

{"id":"X45", "year":"1966", "value":"18372"}
```
This request will update the null value for Post-Leavingcert course enrollment for year 1966 to 18372, and will return JSON to show the update has worked.
