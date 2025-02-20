# 123<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Marksheet Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }

        table {
            width: 50%;
            margin: auto;
            border-collapse: collapse;
        }

        th,
        td {
            border: 1px solid black;
            padding: 10px;
        }

        .container {
            margin-top: 20px;
        }
    </style>
</head>

<body>
    <h2>Student Marksheet Generator</h2>
    <div class="container">
        <label>Student Name: <input type="text" id="studentName"></label><br><br>
        <label>Math: <input type="number" id="math"></label><br><br>
        <label>Science: <input type="number" id="science"></label><br><br>
        <label>English: <input type="number" id="english"></label><br><br>
        <button onclick="saveData()">Save Marksheet</button>
        <button onclick="displayData()">Show Marksheet</button>
        <button onclick="clearData()">Clear Marksheet</button>
    </div>
    <div id="marksheet"></div>

    <script>
        function saveData() {
            let studentName = document.getElementById('studentName').value;
            let math = document.getElementById('math').value;
            let science = document.getElementById('science').value;
            let english = document.getElementById('english').value;

            if (!studentName || !math || !science || !english) {
                alert("Please fill all fields.");
                return;
            }

            let studentData = { studentName, math, science, english };
            sessionStorage.setItem("marksheet", JSON.stringify(studentData));
            alert("Marksheet saved successfully!");
        }

        function displayData() {
            let data = sessionStorage.getItem("marksheet");
            if (!data) {
                document.getElementById("marksheet").innerHTML = "<p>No marksheet found.</p>";
                return;
            }

            let { studentName, math, science, english } = JSON.parse(data);
            let total = Number(math) + Number(science) + Number(english);
            let percentage = (total / 300 * 100).toFixed(2);

            document.getElementById("marksheet").innerHTML = `
                <h3>Marksheet</h3>
                <table>
                    <tr><th>Name</th><td>${studentName}</td></tr>
                    <tr><th>Math</th><td>${math}</td></tr>
                    <tr><th>Science</th><td>${science}</td></tr>
                    <tr><th>English</th><td>${english}</td></tr>
                    <tr><th>Total Marks</th><td>${total}/300</td></tr>
                    <tr><th>Percentage</th><td>${percentage}%</td></tr>
                </table>
            `;
        }

        function clearData() {
            sessionStorage.removeItem("marksheet");
            document.getElementById("marksheet").innerHTML = "";
            document.getElementById('studentName').value = "";
            document.getElementById('math').value = "";
            document.getElementById('science').value = "";
            document.getElementById('english').value = "";
            alert("Marksheet cleared.");
        }


        // const my = "44"
        // console.log(Number(my));
        // console.log("33" + "33" + "44");

        // const myTwo = 22.232323;
        // console.log(myTwo.toFixed(2));


    </script>
</body>
