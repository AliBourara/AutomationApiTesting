# AutomationApiTesting

Simple tutorial how to use Postman For automation Api testing

//! First Api Tests

1-Use the tests options and help your self by the snippets(right of postman) to write simple tests

2-Test Results option can show you is the test fail or pass

3-See test result in the console :
const response = pm.response.json();
console.log(response.status);
console.log(response['status']);

4-another whay to verify status and display it in the console log
pm.test("Status should be ok",()=> {
pm.expect(response.status).to.eq("OK");
});

//! Postman Variables
How to add variables:
Click on the "Environement quick look"(the eye on the left up corner of postman)
click on add Global variable and add the variable

//! Extracting Data from the response
in the test option :

const response = pm.response.json();

//------------->exemple<------->
const nonFictionBooks = response.filter((book) => book.available === true);

console.log(nonFictionBooks[0])

to set that variable you can use the postman snippet Set Global Variable
pm.globals.set("bookId", nonFictionBooks[0].id);

const book = nonFictionBooks[0];

pm.test("Book found",()=> {
pm.expect(book).to.be.an('object');
pm.expect(book.available).to.be.true;
pm.expect(book.available).to.eql(true)  
});

//! Collection Runner
Click on Runner
Drag and drop the CRUD or all the functions
put the authorization first
check the needed option and start the test

//! request execusion order
postman.setNextRequest("List of Books") // next request
postman.setNextRequest(null) // stop execution

//! Postman Monitor
Create specified Monitor on postman
basic trouble shouting => if an error occurs check if there is a missing variable or something had not been propererly set
