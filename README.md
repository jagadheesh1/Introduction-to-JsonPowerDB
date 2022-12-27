	 <!DOCTYPE html>
	 <html lang="en">
	 <head>
	 <title>Student Enrollment Form</title>
	 <meta charset="utf-8">
	 <meta name="viewport" content="width=device-width, initial-scale=1">
	 <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
	 <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script><script
	 src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
	 <script src="http://login2explore.com/jpdb/resources/js/0.0.3/jpdb.commons.js"></script><script	

	 </head>
	 <body>
	 <div class="container">
	 <h2>Vertical (basic) form</h2>
	 <form id="studentForm" method="post">
	 <div class="form-group">
	 <span><label for="RollNo">Roll-No:</label> <label id="RollNoMsg">
	 </label></span>
	 <input type="text" class="form-control" name="RollNo" id="RollNo"
	 placeholder="Enter Roll No" required>
	 </div>
	 <div class="form-group">
	 <label for="fullname">Full-Name:</label>
	 <input type="text" class="form-control" id="fullname"
	 placeholder="Enter Full Name" name="fullname">
	 </div>
	 <div class="form-group">
	 <label for="birth">Birth-Date:</label>
	 <input type="date" class="form-control" id="birth"
	 placeholder="Enter Birth Date" name="birth">
	 </div>
	 <div class="form-group">
	 <label for="address">Address:</label>
	 <input type="text" class="form-control" id="address"
	 placeholder="Enter Address" name="address">
	 </div>
	 <div class="form-group">
	 <label for="enroll">Enrollment-Date:</label>
	 <input type="date" class="form-control" id="enroll" placeholder="Enter Enrollment-Date" name="enroll">
	 </div>

	 <input type="button" class="btn btn-primary" id="save" value="Save"
	 onclick="saveStudent();">
	 <input type="button" class="btn btn-primary" id="update" value="Update"
	 onclick="update();">
	 <input type="button" class="btn btn-primary" id="reset" value="Reset"
	 onclick="resetForm()">
	 </form>
	 </div>
	 <script>
	 $("#RollNo").focus();
	 function validateAndGetFormData() {
	 var RollNoVar = $("#RollNo").val();
	 if (RollNoVar === "") {
	 alert("Roll No Required Value");
	 $("#RollNo").focus();
	 return "";
	 }
	 var fullnameVar = $("#fullname").val();
	 if (fullname === "") {
	 alert("Full Name is Required Value");
	 $("#fullname").focus();
	 return "";
	 }
	 var birthVar = $("#birth").val();
	 if (birthVar === "") {
	 alert("Birth Date is Required Value");
	 $("#birth").focus();
	 return "";
	 }
	 var addressVar = $("#address").val();
	 if (addressVar === "") {
	 alert("Address is Required Value");
	 $("#address").focus();
	 return "";
	 }
	 var enrollVar = $("#enroll").val();
	 if (enrollVar === "") {
	 alert("Enrollment Date is Required Value");
	 $("#enroll").focus();
	 return "";
	 }
	 var jsonStrObj = {
	 RollNo: RollNoVar,
	 fullname: fullnameVar,
	 birth: birthVar,
	 address: addressVar,
	 enroll: enrollVar
	 };
	 return JSON.stringify(jsonStrObj);
	 }
	 // This method is used to create PUT Json request.
	 function createPUTRequest(connToken, jsonObj, dbName, relName) {
	 var putRequest = "{\n"
	 + "\"token\" : \""
	 + connToken
	 + "\","
	 + "\"dbName\": \""
	 + dbName
	 + "\",\n" + "\"cmd\" : \"PUT\",\n"
	 + "\"rel\" : \""
	 + relName + "\","
	 + "\"jsonStr\": \n"
	 + jsonObj
	 + "\n"
	 + "}";
	 return putRequest;
	 }
	 function executeCommand(reqString, dbBaseUrl, apiEndPointUrl) {
	 var url = dbBaseUrl + apiEndPointUrl;
	 var jsonObj;
	 $.post(url, reqString, function (result) {
	 jsonObj = JSON.parse(result);
	 }).fail(function (result) {
	 var dataJsonObj = result.responseText;
	 jsonObj = JSON.parse(dataJsonObj);
	 });
	 return jsonObj;
	 }
	 function resetForm() {
	 $("#RollNo").val("")
	 $("#fullname").val("");
	 $("#birth").val("");
	 $("#address").val("");
	 $("#enroll").val("");
	 $("#RollNo").prop("disabled",false)
	 $("#save").prop("disabled",true)
	 $("#update").prop("disabled",true)
	 $("#reset").prop("disabled",true)
	 $("#RollNo").focus();

	 }

	  saveStudent() {
	 var jsonStr = validateAndGetFormData();	
	 if (jsonStr === "") {
	 return;
	 }
	 var putReqStr = createPUTRequest("90936861|-31948784479254024|90932362", jsonStr, "SAMPLE","EMP-REL");
	 alert(putReqStr);
	 jQuery.ajaxSetup({async: false});
	 var resultObj = executeCommandAtGiverBaseUrl(putReqStr,"http://api.login2explore.com:5577", "/api/iml");
	 jQuery.ajaxSetup({async: true});
	 alert(JSON.stringify(resultObj));
	 resetForm();
	 }
	 </script>
	 </body>
	 </html>
