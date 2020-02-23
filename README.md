# THINK-I_SmartBot
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1" charset="UTF-8">
<style>
body {font-family: Arial, Helvetica, sans-serif;}
* {box-sizing: border-box;}
/* Button used to open the chat form - fixed at the bottom of the page */
.open-button {
  background-color: #EA91F1;
  color: black;
  padding: 16px 20px;
  border: none;
  cursor: pointer;
  opacity: 0.8;
  position: fixed;
  bottom: 23px;
  right: 28px;
  width: 280px;
   display: inline-block;
 font-size: 25px;
  margin: 4px 2px; 
}
/* The popup chat - hidden by default */
.chat-popup {
  display: none;
  position: fixed;
  bottom: 0;
  right: 15px;
  border: 3px solid #f1f1f1;
  z-index: 9;
}
/* Add styles to the form container */
.form-container {
  max-width: 500px;
  padding: 20px;
  background-color: white;
}
/* Full-width textarea */
.form-container textarea {
  width: 100%;
  padding: 15px;
  margin: 5px 0 12px 0;
  border: none;
  background: #f1f1f1;
  resize: none;
  min-height: 125px;
}
.form-container .ta{
  width: 75%;
  padding: 15px;
  margin: 10px 10px 10px 120px;
  border: none;
  background: #f1f1f1;
  resize: none;
  min-height: 75px;
  background-color: #ddd;
  outline: none;
} 
.form-container .ta2{
  width: 75%;
  padding: 15px;
  margin: 11px 10px 10px 10px;
  border: none;
  background: #f1f1f1;
  resize: none;
  min-height: 75px;
  background-color: #ddd;
  outline: none;
}
/* When the textarea gets focus, do something */
.form-container textarea:focus {
  background-color: #ddd;
  outline: none;
}
/* Set a style for the submit/send button */
.form-container .btn {
  background-color: #4CAF50;
  color: white;
  padding: 16px 20px;
  border: none;
  cursor: pointer;
  width: 100%;
  margin-bottom:10px;
  opacity: 08;
}
.form-container .clear{
  background-color: yellow;
  color:teal
}
/* Add a red background color to the cancel button */
.form-container .cancel {
  background-color: red;
}
/* Add some hover effects to buttons */
.form-container .btn:hover, .open-button:hover {
  opacity: 1;
}
</style>
</head>
<body
    style="font-family: Arial,Helvetica,sans-serif ;
text-align:center;
background-image : url('newpic1.jpg');
background-repeat: no-repeat;
background-size:1538px 750px;
box-sizing: border-box">
<h1 style="color:white;font-family:Comic Sans Ms,cursive" ><font size="7">SMART BOT</font></h1>
<button class="open-button" onclick="openForm()" style="border-radius: 20px">Chat</button>
<div class="chat-popup" id="myForm">
  <div class="form-container">
    <h1>Chat</h1>
    <label for="msg"><b>Message</b></label>
    <textarea placeholder="Type message.." class="ta" id="a1" name="msg" required></textarea>
    <textarea placeholder="Wait for the response..." class="ta2" id="a2" name="msg" readonly></textarea>
    <textarea placeholder="history"  name="msg" id="1stone" readonly></textarea>
    <button type="submit" class="btn" onclick="makecall()">Send</button>
    <button type="Clear Question" class="btn clear" onclick="erasetext()">Next Question</button>
    <button type="button" class="btn cancel" onclick="closeForm()">Close</button>
  </div>
</div>
<script>
    var i=0;
function openForm() {
  document.getElementById("myForm").style.display = "block";
}
function erasetext() {
    {
       document.getElementById("1stone").value+="user:"+document.getElementById("a1").value+"\n";
       document.getElementById("1stone").value+="admin:"+document.getElementById("a2").value+"\n";
      }  
  document.getElementById("a1").value="";
  document.getElementById("a2").value="";
}
function closeForm() {
  document.getElementById("myForm").style.display = "none";
  document.getElementById("a1").value="";
  document.getElementById("a2").value="";
  document.getElementById("1stone").value="";
}
function makecall()
{
var que=document.getElementById("a1").value;   
var myHeaders = new Headers();
myHeaders.append("organizationId", "f19ff4ff-2db1-45e4-bdb2-8a48decfcc90");
myHeaders.append("Content-Type", "application/json");
myHeaders.append("Authorization", "Bearer HwYOMVfYFPPcuWBWU0X4AhvKlG19l10nqHWflHxcgo06tNlOi2JFU3MUVe7LQu3WfQqHpT0EBKr2Y4FNJa9cZw");
var raw = JSON.stringify({"query":que,"pageSize":1,"pageNumber":1,"languageCode":"en-US","documentType":"Faq","searchOnDraftDocuments":"True"});
var requestOptions = {
method: 'POST',
headers: myHeaders,
body: raw,
redirect: 'follow'
};
fetch("https://api.mypurecloud.com/api/v2/knowledge/knowledgebases/fc6f7458-0284-4189-ad69-85556da1be9c/search", requestOptions)
  .then(response => {
   data = response.json().then(text =>{
    data =text.results[0].faq.answer
    document.getElementById("a2").value=data;
    })
    } )
 .catch(error => {
  console.log('error', error)});

