<!DOCTYPE html>
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->
<html lang="en">
<head>
<title>Bootstrap Example</title>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="stylesheet"
href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
<script
src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script
src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
</head>
<body>
<center>
    <div class="container">
<h2 >STUDENT-TABLE</h2>
<form id="empForm" method="post">
<div class="form-group">
<span><label for="stdroll">Student Roll-No:</label> <label id="stdroll">
</label></span>
<input type="text" class="form-control" name="stdroll" id="stdroll"
placeholder="Enter Student Roll Number" required>
</div>
<div class="form-group">
    <span><label for="stdname">Student Name:</label> <label id="stdName">
</label></span>
<input type="text" class="form-control" id="stdName"
placeholder="Enter Student Name" name="stdName">
</div>
<div class="form-group">
    <span><label for="stdclass">Class:</label> <label id="stdClass">
</label></span>
<input type="text" class="form-control" id="stdClass"
placeholder="Enter Student Class" name="stdClass">
</div>
    <div class="form-group">
        <span><label for="stdDOB">Student Date of :</label> <label id="stdroll">
</label></span>
<label for="stdDOB">Birth-Date:</label>
<input type="date" class="form-control" id="stdDOB"
placeholder="Enter Student DOB" name="stdBD">
</div>
    <div class="form-group">
<label for="stdAddress">Address:</label>
<input type="text" class="form-control" id="stdAddress"
placeholder="Enter Student Address" name="stdAddress">
</div>
    <div class="form-group">
        <label for="stdEnrollment">Enrollment-Date:</label>
<input type="date" class="form-control" id="stdED"
placeholder="Enter Student Enrollment-Date" name="stdEnrollment">
</div>
<input type="button" class="btn btn-primary" id="stdSave" value="Save"
onclick="saveStudent();">
<input type="button" class="btn btn-primary" id="stdupdate" value="Update"
onclick="updateStudent();">
<input type="button" class="btn btn-primary" id="stdrest" value="Reset"
onclick="resetStudent();">
</form>
</div>
   <script>
$("#stdroll").focus();
function validateAndGetFormData() {
var stdrollVar = $("#stdroll").val();
if (stdrollVar === "") {
alert("Student Roll Number Required Value");
$("#stdroll").focus();
return "";
}
var stdNameVar = $("#stdName").val();
if (stdNameVar === "") {
alert("Employee Name is Required ");
$("#stdName").focus();
return "";
}
var stdClassVar = $("#stdclass").val();
if (stdClassVar === "") {
alert("Student Class is Required ");
$("#stdClass").focus();
return "";
}
var stdDOBVar = $("#stdDOB").val();
if (stdDOBVar === "") {
alert("Student Date of Birth is Required ");
$("#stdDOB").focus();
return "";
}
var stdAddressVar = $("#stdAddress").val();
if (stdAddressVar === "") {
alert("Student Address is Required ");
$("#stdAddress").focus();
return "";
}
var stdEnrollmentVar = $("#stdED").val();
if (stdEnrollmentVar === "") {
alert("Student Enrollment-Date is Required ");
$("#stdED").focus();
return "";
}
var jsonStrObj = {
stdroll: stdrollVar,
stdName: stdNameVar,
stdClass: stdClassVar,
stdDOB: stdDOBVar,
stdAddress:  stdAddressvar,
stdEnrollment: stdEnrollmentVar
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
$("#stdroll").val("");
$("#stdName").val("");
$("#stdClass").val("");
$("#stdDOB").val("");
$("#stdAddress").val("");
$("#stdEnrollment").val("");
$("#stdroll").focus();
}
function saveEmployee() {
var jsonStr = validateAndGetFormData();
if (jsonStr === "") {
return;
}
function updateEmployee() {
var jsonStr = validateAndGetFormData();
if (jsonStr === "") {
return;
}
var putReqStr = createPUTRequest("90934477|-31949224290170022|90962714",
jsonStr, "SAMPLE", "EMP-REL");
alert(putReqStr);
jQuery.ajaxSetup({async: false});
var resultObj = executeCommand(putReqStr,
"http://api.login2explore.com:5577", "/api/iml");
alert(JSON.stringify(resultObj));
jQuery.ajaxSetup({async: true});
resetForm();
}
}
</script>
</center>
</body>
</html>
