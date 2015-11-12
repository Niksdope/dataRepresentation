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
The aim of this API is to provide efficent access of the data provided by the dataset. This will be achieved by a number of carefully thought out *URLs* that allow any part of the data to be accessed. I imagine the the dataset being used mostly by economists so access to every single piece of data is key. As an economist you might also want useful functions to be used on the data and so JS functions will also be written to refine the data. In the JSON file of the dataset, it is visible that all the levels of education and years have unique indexes to uniquely identify every piece of data.


The levels of education are indexed as follows:
- **" - "** denotes All levels of education
- **" 104 "** denotes First level
- **" 23 "** denotes Second level
- **" 4 "** denotes Third level
- **" X45 "** denotes Post leaving certificate courses (VPT2)


####*GET request* - retrieves data from a web server by specifying parameters in the URL portion of the request
A URL to return a list of all years and their values for a particular level of education would look like this [https://educationapi.com/level/[level]]()

e.g. [https://educationapi.com/level/-]() and would return every year of students enrolled for all levels of education together.

* The data returned will be in JSON format and will include
  - "id":  for the level of education being returned
  - "year": for every year 1966-2015 specific to the education level specified
  - "value": for each value specific to each year
```json
{
  "id" : "-",
  "year" : ["1966", "1967", "1968", "1969", "1970", "1971", "1972", "1973", "1974", "1975", "1976", "1977", "1978"...],
  "value" : ["638298","652844","670382","692860","712928","732214","750979","768789","786541","803503","828019","848025"...]
}
```


A URL to return a list of all different education levels for a particular year and their values [https://educationapi.com/year/[year]]()

e.g. [https://educationapi.com/year/1966]() would return every level of education students have enrolled for 1966.

* The data returned will be in JSON format and will include
  - "year": for the specific year in the url
  - "id": for all different levels of education
  - "value": for every value for the speified year under every education level
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

* The data returned will be in JSON format and will include
  - "id":  for the level of education specified
  - "year": for the year specified
  - "value": for the specified level of education and year
```json
{
  "id" : "23",
  "year" : "2015",
  "value" : "544696"
}
```


####*POST request* - used when you want to send some data to the server, for example, file update, form data, etc.
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


####*JS functions* - used to further refine data returned from a dataset. (inside the HTML file)
The API I'm creating will have JS methods for the users, which will do the following:
* Printing the JSON objects returned in a easy to read format (print.pretty)
* Calculating the difference in students enrolling into a specific education level from one year to another
* Use D3.js to draw graphs to represent the data in the dataset

The function to compare the years would just be a combo box for all different education levels, two textboxes in the html file with a button called compare and the function would be an event listener to check if the button has been clicked.

It will then use change all the values entered into JSON, find the *"value"* for both years and take the one with a higher year away from the one with a lower year.

```js
document.getElementById("compareBtn").addEventListener("click", compare);

function compare() {
  // get the json variable and put them into local variables
  var difference = 0;
  if(year1 > year2)
  {
    difference = year1-year2;
  }
  else if (year2 > year1)
  {
    difference = year2-year1;
  }
  
  document.getElementById("pForResult").innerHTML = difference;
}
```


### The Future
In the future the API will have many newer versions each with added functionality 

1. The API could make use of more http methods such as *DELETE* and *PUT* to further update the data on the server
2. Add a more refined look to the html to display the responses sent from the server
3. Make querying the dataset much easier by making a web page to query it for you in the background and all the users would have to do is input data like education level or year into their designated fields on the html page
4. Add more functions for the use of economists to make sense of the data with more ease


### Summary
This API was designed for Apps4gaps to provide simple and efficent access to their dataset concerning "**Enrolments of Full-Time Students by Level of Education and Year**". I hope that the dataset will be of use to not only Apps4gaps but also any user that might want to query the Irish dataset for enrolled students through out the years since 1966. Thanks for reading.
