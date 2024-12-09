#Step 1: 
Create the index.html File

Create a simple **index.html** file to serve via the Nginx server.

File: index.html

## Table for Contents
<!doctype html>
<html>
 <body style="backgroud-color:rgb(49, 214, 220);"><center>
    <head>
     <title>Docker Project</title>
    </head>
    <body>
     <p>Welcome to my Docker Project!<p>
        <p>Today's Date and Time is: <span id='date-time'></span><p>
        <script>
             var dateAndTime = new Date();
             document.getElementById('date-time').innerHTML=dateAndTime.toLocaleString();
        </script>
        </body>
</html>

## Instalation
