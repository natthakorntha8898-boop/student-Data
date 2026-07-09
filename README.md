<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ระบบตรวจสอบการเข้าเรียน</title>

<style>
body{
    font-family: Arial, sans-serif;
    background:#f2f5f9;
    margin:0;
}
header{
    background:#1565c0;
    color:white;
    padding:15px;
    text-align:center;
}
.container{
    width:90%;
    max-width:900px;
    margin:auto;
    margin-top:20px;
}
.card{
    background:white;
    padding:20px;
    border-radius:10px;
    box-shadow:0 0 10px rgba(0,0,0,.15);
}
input,select,button{
    padding:10px;
    margin:5px;
}
button{
    background:#1565c0;
    color:white;
    border:none;
    cursor:pointer;
}
table{
    width:100%;
    border-collapse:collapse;
    margin-top:20px;
}
table,th,td{
    border:1px solid #ccc;
}
th{
    background:#1565c0;
    color:white;
}
th,td{
    padding:10px;
    text-align:center;
}
.hidden{
    display:none;
}
</style>
</head>

<body>

<header>
<h2>ระบบตรวจเช็คการเข้าเรียนและผลการเรียน</h2>
</header>

<div class="container">

<div class="card" id="login">

<h3>เข้าสู่ระบบ</h3>

<select id="role">
<option value="teacher">คุณครู</option>
<option value="student">นักเรียน</option>
</select>

<input type="text" id="username" placeholder="ชื่อ">

<button onclick="login()">เข้าสู่ระบบ</button>

</div>

<div class="card hidden" id="teacherPage">

<h2>หน้าคุณครู</h2>

<input type="text" id="studentName" placeholder="ชื่อนักเรียน">

<select id="attendance">
<option>มาเรียน</option>
<option>ขาด</option>
<option>ลา</option>
<option>สาย</option>
</select>

<select id="grade">
<option>ปกติ</option>
<option>0</option>
<option>ร</option>
<option>มส.</option>
<option>มผ.</option>
</select>

<button onclick="saveData()">บันทึก</button>

<table>

<thead>

<tr>

<th>ชื่อ</th>

<th>การเข้าเรียน</th>

<th>ผลการเรียน</th>

</tr>

</thead>

<tbody id="teacherTable">

</tbody>

</table>

</div>

<div class="card hidden" id="studentPage">

<h2>ข้อมูลนักเรียน</h2>

<p id="showName"></p>

<table>

<thead>

<tr>

<th>ชื่อ</th>

<th>การเข้าเรียน</th>

<th>ผลการเรียน</th>

</tr>

</thead>

<tbody id="studentTable">

</tbody>

</table>

</div>

</div>

<script>

let students = JSON.parse(localStorage.getItem("students")) || [];

function login(){

let role=document.getElementById("role").value;
let user=document.getElementById("username").value;

document.getElementById("login").classList.add("hidden");

if(role=="teacher"){

document.getElementById("teacherPage").classList.remove("hidden");

showTeacher();

}else{

document.getElementById("studentPage").classList.remove("hidden");

document.getElementById("showName").innerHTML="ชื่อ : "+user;

showStudent(user);

}

}

function saveData(){

let name=document.getElementById("studentName").value;

let attend=document.getElementById("attendance").value;

let grade=document.getElementById("grade").value;

students.push({

name:name,

attendance:attend,

grade:grade

});

localStorage.setItem("students",JSON.stringify(students));

showTeacher();

alert("บันทึกข้อมูลเรียบร้อย");

}

function showTeacher(){

let html="";

students.forEach(s=>{

html+=`

<tr>

<td>${s.name}</td>

<td>${s.attendance}</td>

<td>${s.grade}</td>

</tr>

`;

});

document.getElementById("teacherTable").innerHTML=html;

}

function showStudent(user){

let html="";

students.forEach(s=>{

if(s.name==user){

html+=`

<tr>

<td>${s.name}</td>

<td>${s.attendance}</td>

<td>${s.grade}</td>

</tr>

`;

}

});

document.getElementById("studentTable").innerHTML=html;

}

</script>

</body>
</html>
