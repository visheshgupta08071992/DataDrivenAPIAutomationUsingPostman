### Some of the generic validation used in above framework against below response

**Response**

```js

{
        "id":439,
        "first_name": "Monu",
        "jobs":["Tester1","Trainer1"],
        "favFoods":{
            "breakfast":"poha",
            "dinner":["Chapati1","Milk1"]
        }
}

```

**Example to retreive data from above TestData file**

```js

var first_name = pm.variables.get("first_name");
var breakfast = pm.variables.get("breakfast");
var jobs=pm.variables.get("jobs");
var dinner=pm.variables.get("dinner");

```

**Example Tests to compare data of Test Data file with Json response**

```js

//Storing the response body
var jsonData = pm.response.json();

//Retrieve data of Test data file in a variable
var first_name = pm.variables.get("first_name");
var breakfast = pm.variables.get("breakfast");
var jobs=pm.variables.get("jobs");
var dinner=pm.variables.get("dinner");

pm.test("Status code is 200" , function(){
    pm.response.to.have.status(200);
});

pm.test("Check first_name " +first_name, function () {
    pm.expect(jsonData.first_name).to.eql(first_name);
});
 
pm.test("Check breakfast " +breakfast, function () {
    pm.expect(jsonData.favFoods.breakfast).to.eql(breakfast);
});

pm.test("Check Jobs " +jobs, function () {
    /*
    Here jsonData.jobs is an array while we  retrieve jobs as String from data file.
    Hence coverting  jsonData.jobs array into string with JSON.stringify function so that it can be compared with jobs field from data file.
    */
    pm.expect(JSON.stringify(jsonData.jobs)).to.eql(jobs);
});



pm.test("Check dinner " +dinner, function () {
     /*
    Here jsonData.favFoods.dinner is an array while we retrieve dinner as String from data file.
    Hence coverting  jsonData.favFoods.dinner array into string with JSON.stringify function so that it can be compared with dinner field from data file.
    */

    pm.expect(JSON.stringify(jsonData.favFoods.dinner)).to.eql(dinner);
});


```
