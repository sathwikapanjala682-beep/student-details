<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>CSE Student Information</title>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            background-color: #f4f7fb;
            color: #333;
        }

        header {
            background: #1e3a8a;
            color: white;
            padding: 25px;
            text-align: center;
        }

        header h1 {
            margin-bottom: 8px;
        }

        header p {
            font-size: 16px;
        }

        .container {
            width: 90%;
            max-width: 1100px;
            margin: 30px auto;
        }

        .form-box {
            background: white;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            margin-bottom: 25px;
        }

        .form-box h2 {
            margin-bottom: 20px;
            color: #1e3a8a;
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }

        input, select {
            width: 100%;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 6px;
            font-size: 15px;
        }

        button {
            background: #1e3a8a;
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 15px;
            margin-top: 15px;
        }

        button:hover {
            background: #162d6b;
        }

        .search-box {
            background: white;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 25px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }

        .search-box input {
            width: 100%;
        }

        .table-box {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            overflow-x: auto;
        }

        .table-box h2 {
            color: #1e3a8a;
            margin-bottom: 20px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 750px;
        }

        th {
            background: #1e3a8a;
            color: white;
            padding: 13px;
            text-align: left;
        }

        td {
            padding: 12px;
            border-bottom: 1px solid #ddd;
        }

        tr:hover {
            background-color: #f1f5ff;
        }

        .delete-btn {
            background: #dc2626;
            padding: 7px 12px;
            margin: 0;
        }

        .delete-btn:hover {
            background: #b91c1c;
        }

        footer {
            margin-top: 40px;
            background: #1e3a8a;
            color: white;
            text-align: center;
            padding: 18px;
        }

        @media (max-width: 700px) {
            .form-grid {
                grid-template-columns: 1fr;
            }

            .container {
                width: 95%;
            }
        }
    </style>
</head>

<body>

    <header>
        <h1>CSE Student Information System</h1>
        <p>Computer Science and Engineering Department</p>
    </header>

    <div class="container">

        <!-- Add Student Form -->
        <div class="form-box">
            <h2>Add Student</h2>

            <form id="studentForm">

                <div class="form-grid">

                    <input
                        type="text"
                        id="studentName"
                        placeholder="Student Name"
                        required
                    >

                    <input
                        type="text"
                        id="rollNo"
                        placeholder="Roll Number"
                        required
                    >

                    <input
                        type="text"
                        id="course"
                        placeholder="Course"
                        value="B.E / B.Tech CSE"
                        required
                    >

                    <input
                        type="text"
                        id="village"
                        placeholder="Village"
                        required
                    >

                    <input
                        type="text"
                        id="college"
                        placeholder="College Name"
                        required
                    >

                    <select id="year" required>
                        <option value="">Select Year</option>
                        <option value="1st Year">1st Year</option>
                        <option value="2nd Year">2nd Year</option>
                        <option value="3rd Year">3rd Year</option>
                        <option value="4th Year">4th Year</option>
                    </select>

                </div>

                <button type="submit">Add Student</button>

            </form>
        </div>


        <!-- Search -->
        <div class="search-box">
            <input
                type="text"
                id="searchInput"
                placeholder="Search by name, roll number, village or college..."
            >
        </div>


        <!-- Student Table -->
        <div class="table-box">

            <h2>Student Details</h2>

            <table>

                <thead>
                    <tr>
                        <th>S.No</th>
                        <th>Student Name</th>
                        <th>Roll No</th>
                        <th>Course</th>
                        <th>Village</th>
                        <th>College</th>
                        <th>Year</th>
                        <th>Action</th>
                    </tr>
                </thead>

                <tbody id="studentTable">
                    <!-- Students will appear here -->
                </tbody>

            </table>

        </div>

    </div>


    <footer>
        <p>© 2026 CSE Student Information System</p>
    </footer>


    <script>

        // Student data
        let students = [
            {
                name: "Rahul Kumar",
                rollNo: "CSE001",
                course: "B.E / B.Tech CSE",
                village: "Bengaluru",
                college: "ABC Engineering College",
                year: "3rd Year"
            },
            {
                name: "Priya Sharma",
                rollNo: "CSE002",
                course: "B.E / B.Tech CSE",
                village: "Mysuru",
                college: "XYZ Engineering College",
                year: "2nd Year"
            }
        ];


        // Display students
        function displayStudents(studentList = students) {

            const table = document.getElementById("studentTable");

            table.innerHTML = "";

            if (studentList.length === 0) {

                table.innerHTML = `
                    <tr>
                        <td colspan="8" style="text-align:center;">
                            No students found
                        </td>
                    </tr>
                `;

                return;
            }


            studentList.forEach((student, index) => {

                const row = document.createElement("tr");

                row.innerHTML = `
                    <td>${index + 1}</td>
                    <td>${student.name}</td>
                    <td>${student.rollNo}</td>
                    <td>${student.course}</td>
                    <td>${student.village}</td>
                    <td>${student.college}</td>
                    <td>${student.year}</td>

                    <td>
                        <button
                            class="delete-btn"
                            onclick="deleteStudent('${student.rollNo}')">
                            Delete
                        </button>
                    </td>
                `;

                table.appendChild(row);

            });
        }


        // Add student
        document.getElementById("studentForm").addEventListener(
            "submit",
            function(event) {

                event.preventDefault();

                const student = {

                    name: document.getElementById("studentName").value,

                    rollNo: document.getElementById("rollNo").value,

                    course: document.getElementById("course").value,

                    village: document.getElementById("village").value,

                    college: document.getElementById("college").value,

                    year: document.getElementById("year").value

                };


                // Check duplicate roll number
                const exists = students.some(
                    s => s.rollNo.toLowerCase() ===
                         student.rollNo.toLowerCase()
                );


                if (exists) {

                    alert("Roll number already exists!");

                    return;
                }


                students.push(student);

                displayStudents();

                document.getElementById("studentForm").reset();

                document.getElementById("course").value =
                    "B.E / B.Tech CSE";

            }
        );


        // Delete student
        function deleteStudent(rollNo) {

            const confirmation = confirm(
                "Are you sure you want to delete this student?"
            );

            if (!confirmation) {
                return;
            }

            students = students.filter(
                student => student.rollNo !== rollNo
            );

            displayStudents();
        }


        // Search students
        document.getElementById("searchInput").addEventListener(
            "input",
            function() {

                const searchText =
                    this.value.toLowerCase().trim();


                const filteredStudents = students.filter(student =>

                    student.name.toLowerCase().includes(searchText) ||

                    student.rollNo.toLowerCase().includes(searchText) ||

                    student.course.toLowerCase().includes(searchText) ||

                    student.village.toLowerCase().includes(searchText) ||

                    student.college.toLowerCase().includes(searchText) ||

                    student.year.toLowerCase().includes(searchText)

                );


                displayStudents(filteredStudents);

            }
        );


        // Initial display
        displayStudents();

    </script>

</body>
</html># student-details
