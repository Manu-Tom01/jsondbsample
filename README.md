#About JsonPowerDB:
#JsonPowerDB is a Real-time, High Performance, Lightweight and Simple to Use, Rest API based Multi-mode DBMS. JsonPowerDB has ready to #use API for Json document DB, RDBMS, Key-value DB, GeoSpatial DB and Time Series DB functionality. JPDB supports and advocates for #true serverless and pluggable API development.
#Benefits of using JsonPowerDB
#1 Simplest way to retrieve data in a JSON format.
#2 Schema-free, Simple to use, Nimble and In-Memory database.
#3 It is built on top of one of the fastest and real-time data indexing engine - PowerIndeX.
#4 It is low level (raw) form of data and is also human readable.
#5 It helps developers in faster coding, in-turn reduces development cost.

#code
<!DOCTYPE html>
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->
<html lang="en">
    <head>
        <title>manu form</title>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet"
              href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
        <script
        src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
        <script
        src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
        <script
        src="https://login2explore.com/jpdb/resources/js/0.0.3/jpdb-commons.js"></script>
    </head>
    <body>
        <div class="container">
            <h2>Student Details</h2>
            <form id="studForm" method="post">
                <div class="form-group">
                    <span><label for="studId">Student ID:</label> <label id="studIdMsg">
                        </label></span>
                    <input type="text" class="form-control" name="studId" id="studId"
                           placeholder="Enter Student ID" required>
                </div>
                <div class="form-group">
                    <label for="studName">Student Name:</label>
                    <input type="text" class="form-control" id="studName"
                           placeholder="Enter Student Name" name="studName">
                </div>
                <div class="form-group">
                    <label for="studEmail">Email:</label>
                    <input type="email" class="form-control" id="studEmail"
                           placeholder="Enter Student Email" name="studEmail">
                </div>
                <input type="button" class="btn btn-primary" id="empSave" value="Save"
                       onclick="saveStudent();">
            </form>
        </div>
        <script>
            $("#studId").focus();
            function validateAndGetFormData() {
                var studIdVar = $("#studId").val();
                if (studIdVar === "") {
                    alert("Student ID Required Value");
                    $("#studId").focus();
                    return "";
                }
                var studNameVar = $("#studName").val();
                if (studNameVar === "") {
                    alert("Student Name is Required Value");
                    $("#studName").focus();
                    return "";
                }
                var studEmailVar = $("#studEmail").val();
                if (studEmailVar === "") {
                    alert("Student Email is Required Value");
                    $("#studEmail").focus();
                    return "";
                }
                var jsonStrObj = {
                    studId: studIdVar,
                    studName: studNameVar,
                    studEmail: studEmailVar,
                }
                ;
                return JSON.stringify(jsonStrObj);
            }
            function resetForm() {
                $("#studId").val("")
                $("#studName").val("");
                $("#studEmail").val("");
                $("#studId").focus();
            }
            function saveStudent() {
                var jsonStr = validateAndGetFormData();
                if (jsonStr === "") {
                    return;
                }
                var putReqStr = createPUTRequest("90935900|-31948845230531937|90944920",
                        jsonStr, "Student", "STUD-REL");
                alert(putReqStr);
                jQuery.ajaxSetup({async: false});
                var resultObj = executeCommand(putReqStr,
                        "http://api.login2explore.com:5577", "/api/iml");
                alert(JSON.stringify(resultObj));
                jQuery.ajaxSetup({async: true});
                resetForm();
            }
        </script>
    </body>
</html>
