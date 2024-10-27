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
<div class="container">
<h2>STUDENT TABLE</h2>
<form id="stdForm" method="post">
<div class="form-group">
<span><label for="stdRoll">RollNo:</label> <label id="stdRollMsg">
</label></span>
<input type="text" class="form-control" name="stdRoll" id="stdRoll"
placeholder="Enter Student Roll Number" required>
</div>
<div class="form-group">
<label for="stdName">Student Name:</label>
<input type="text" class="form-control" id="stdName"
placeholder="Enter Student Name" name="stdName">
</div>
<div class="form-group">
<label for="stdClass">Class:</label>
<input type="text" class="form-control" id="stdClass"
placeholder="Enter Student Class" name="stdClass">
</div>
    <div class="form-group">
<label for="stdDOB">DOB:</label>
<input type="date" class="form-control" id="stdDOB"
placeholder="Enter Student Date of Birth" name="stdDOB">
</div>
    <div class="form-group">
<label for="stdAddress">Address:</label>
<input type="text" class="form-control" id="stdAddress"
placeholder="Enter Student Address" name="sstdAddress">
</div>
       <div class="form-group">
<label for="stdEnrollment">Enrollment-Date:</label>
<input type="date" class="form-control" id="stdEnrollment"
placeholder="Enter Student Enrollment Date " name="stdEnrollment">
</div>
<input type="button" class="btn btn-primary" id="stdSave" value="Save"
onclick="saveStudent();">
<input type="button" class="btn btn-primary" id="stdupdate" value="update"
onclick="updateStudent();">
<input type="button" class="btn btn-primary" id="stdSave" value="Reset"
onclick="resetStudent();">
</form>
</div>
<script>
$("stdRoll").focus();
function validateAndGetFormData() {
var stdRollVar = $("#stdRoll").val();
if (stdRollVar === "") {
alert("Student Roll Number Required");
$("#stdRoll").focus();
return "";
}
var stdNameVar = $("#stdName").val();
if (stdNameVar === "") {
alert("Student Name is Required Value");
$("#stdName").focus();
return "";
}
var stdClassVar = $("#stdClass").val();
if (stdClassVar === "") {
alert("Employee Class is Required Value");
$("#stdClass").focus();
return "";
}
var stdDOBVar = $("#stdDOB").val();
if (stdDOBVar === "") {
alert("Employee Date of Birth  is Required Value");
$("#stdDOB").focus();
return "";
}
var stdAddressVar = $("#stdAddress").val();
if (stdAddressVar === "") {
alert("Employee Address is Required Value");
$("#stdAddress").focus();
return "";
}
var stdEnrollmentVar = $("#stdEnrollment").val();
if (stdEnrollmentVar === "") {
alert("Employee Enrollment Date  is Required Value");
$("#stdEnrollment").focus();
return "";
}
var jsonStrObj = {
stdRoll: stdRollVar,
stdName: stdNameVar,
stdClass: stdClassVar,
stdDOB: stdDOBVar,
stdAddress: stdAddressVar,
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
$("#stdRoll").val("");
$("#stdName").val("");
$("#stdClass").val("");
$("#stdDOB").val("");
$("#stdAddress").val("");
$("#stdEnrollment").val("");
$("#stdRoll").focus();
}
function saveStudent() {
var jsonStr = validateAndGetFormData();
if (jsonStr === "") {
return;
}
var putReqStr = createPUTRequest("90934477|-31949224290170022|90962714",
jsonStr, "Student", "Std-REL");
alert(putReqStr);
jQuery.ajaxSetup({async: false});
var resultObj = executeCommand(putReqStr,
"http://api.login2explore.com:5577", "/api/iml");
alert(JSON.stringify(resultObj));
jQuery.ajaxSetup({async: true});
resetForm();
$("#stdRoll").focus();
}
function updateStudent() {
var jsonStr = validateAndGetFormData();
if (jsonStr === "") {
return;
}
var updateRequest = createUPDATERecordRequest("90934477|-31949224290170022|90962714",
jsonStr, "Student", "Std-REL");
alert(updateReqStr);
jQuery.ajaxSetup({async: false});
var resultObj = executeCommand(updateReqStr,
"http://api.login2explore.com:5577", "/api/iml");
alert(JSON.stringify(resultObj));
jQuery.ajaxSetup({async: true});
resetForm();
$("#stdRoll").focus();
}
function resetStudent() {
var jsonStr = validateAndGetFormData();
if (jsonStr === "") {
return;
}
var getReqStr = createGETRequest("90934477|-31949224290170022|90962714",
jsonStr, "Student", "Std-REL");
alert(getReqStr);
jQuery.ajaxSetup({async: false});
var resultObj = executeCommand(putReqStr,
"http://api.login2explore.com:5577", "/api/iml");
alert(JSON.stringify(resultObj));
jQuery.ajaxSetup({async: true});
resetForm();
$("#stdRoll").focus();
}
</script>
</body>
</html>
