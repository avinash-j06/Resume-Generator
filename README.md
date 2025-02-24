# Resume-Generator
This Resume Generator is a web application that allows users to create professional resumes by entering personal, academic, and work details. It provides a real-time preview and the option to print the generated resume. Built using HTML, CSS, and JavaScript, the app features a responsive design for various devices.

#Code:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Resume Generator</title>
    <style>
        /* Overall page layout */
        body {
            font-family: 'Arial', sans-serif;
            background: #f4f7fb;
            margin: 0;
            padding: 0;
        }
        .main-container {
            display: flex;
            flex-direction: row;
            max-width: 1200px;
            margin: 20px auto;
        }
        .container {
            width: 50%;
            padding: 20px;
            box-sizing: border-box;
        }
        .form-container {
            background: #ffffff;
            border-radius: 8px;
            box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.1);
        }
        .resume-container {
            background: #ffffff;
            border-radius: 8px;
            box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.1);
            padding: 20px;
            height: fit-content;
            margin-left: 20px;
            overflow: auto;
        }
        /* Styles for the form */
        .form-container h1, .form-container h2 {
            color: #4CAF50; /* Green color for the form */
            text-align: center;
        }
        .form-container h2 {
            margin-top: 30px;
        }
        .form-group {
            margin-bottom: 15px;
            display: flex;
            flex-direction: column;
        }
        .form-control {
            width: 100%;
            padding: 10px;
            margin-top: 8px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 4px;
            transition: border-color 0.3s;
            resize: vertical;
        }
        .form-control:focus {
            border-color: #4CAF50; /* Green border on focus */
            outline: none;
        }
        .btn {
            background-color: #4CAF50; /* Green button for the form */
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 20px;
            width: 100%;
            font-size: 1.2em;
        }
        .btn:hover {
            background-color: #45a049;
        }
        /* Styles for the generated CV */
        .resume-container h1, .resume-container h2 {
            color: #000080; /* Dark navy blue for the CV */
            text-align: center;
        }
        .resume-container h2 {
            margin-top: 30px;
        }
        .resume-section h2 {
            color: #000080; /* Dark navy blue for section headings */
            border-bottom: 1px solid #ddd;
            padding-bottom: 5px;
        }
        /* Button in the CV */
        .btn-print {
            background-color: #000080; /* Dark navy blue button in the CV */
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 20px;
            width: 100%;
            font-size: 1.2em;
        }
        .btn-print:hover {
            background-color: #000066; /* Slightly darker navy blue on hover */
        }
        .resume-content p {
            white-space: pre-wrap;
            line-height: 1.5;
            margin-bottom: 10px;
        }
        /* Print styles */
        @media print {
            body {
                background: white;
            }
            .main-container {
                flex-direction: column;
            }
            .form-container {
                display: none;
            }
            .resume-container {
                width: 100%;
                margin: 0 auto;
            }
        }
    </style>
</head>
<body>
    <div class="main-container">
        <!-- Input Form -->
        <div class="container form-container">
            <h1>Resume Generator</h1>
            <p style="text-align:center;">by Avinash Jaiswal</p>
            <h2>Enter Your Information Below</h2>

            <!-- Name and Contact Section -->
            <div class="form-group">
                <label for="namefield">Your Name:</label>
                <input type="text" id="namefield" class="form-control" placeholder="Enter your name">
            </div>
            <div class="form-group">
                <label for="contactfield">Contact No:</label>
                <input type="text" id="contactfield" class="form-control" placeholder="Enter your contact number">
            </div>
            <div class="form-group">
                <label for="emailfield">Email-ID:</label>
                <input type="email" id="emailfield" class="form-control" placeholder="Enter your Email-ID">
            </div>
            <div class="form-group">
                <label for="addressfield">Your Address:</label>
                <textarea id="addressfield" class="form-control" placeholder="Enter your address"></textarea>
            </div>

            <!-- Social Media Links -->
            <h2>Important Links</h2>
            <div class="form-group">
                <label for="linkedinfield">LinkedIn:</label>
                <input type="url" id="linkedinfield" class="form-control" placeholder="Paste LinkedIn link">
            </div>
            <div class="form-group">
                <label for="igfield">Instagram:</label>
                <input type="url" id="igfield" class="form-control" placeholder="Paste Instagram link">
            </div>
            <div class="form-group">
                <label for="gitfield">GitHub:</label>
                <input type="url" id="gitfield" class="form-control" placeholder="Paste GitHub link">
            </div>

            <!-- Professional Information -->
            <h2>Professional Information</h2>
            <div class="form-group">
                <label for="academicfield">Academic Qualifications:</label>
                <textarea id="academicfield" class="form-control" placeholder="Write your academic qualifications"></textarea>
            </div>
            <div class="form-group">
                <label for="workfield">Work Experience:</label>
                <textarea id="workfield" class="form-control" placeholder="Write your work experience"></textarea>
            </div>
            <div class="form-group">
                <label for="projectfield">Projects:</label>
                <textarea id="projectfield" class="form-control" placeholder="Write about your projects"></textarea>
            </div>

            <button onclick="generateCV()" class="btn">Generate CV</button>
        </div>

        <!-- Generated Resume -->
        <div class="container resume-container" id="resumeContainer">
            <h1 id="resumeName"></h1>
            <div class="resume-section">
                <h2>Contact Information</h2>
                <div class="resume-content">
                    <p id="resumeContact"></p>
                    <p id="resumeEmail"></p>
                    <p id="resumeAddress"></p>
                </div>
            </div>
            <div class="resume-section">
                <h2>Important Links</h2>
                <div class="resume-content">
                    <p id="resumeLinkedIn"></p>
                    <p id="resumeInstagram"></p>
                    <p id="resumeGitHub"></p>
                </div>
            </div>
            <div class="resume-section">
                <h2>Academic Qualifications</h2>
                <div class="resume-content">
                    <p id="resumeAcademics"></p>
                </div>
            </div>
            <div class="resume-section">
                <h2>Work Experience</h2>
                <div class="resume-content">
                    <p id="resumeWork"></p>
                </div>
            </div>
            <div class="resume-section">
                <h2>Projects</h2>
                <div class="resume-content">
                    <p id="resumeProjects"></p>
                </div>
            </div>
            <div style="text-align: center; margin-top: 20px;">
                <button onclick="window.print()" class="btn-print">Print Resume</button>
            </div>
        </div>
    </div>

    <script>
        function generateCV() {
            // Collect user input
            var name = document.getElementById('namefield').value;
            var contact = document.getElementById('contactfield').value;
            var email = document.getElementById('emailfield').value;
            var address = document.getElementById('addressfield').value;
            var linkedin = document.getElementById('linkedinfield').value;
            var instagram = document.getElementById('igfield').value;
            var github = document.getElementById('gitfield').value;
            var academics = document.getElementById('academicfield').value;
            var work = document.getElementById('workfield').value;
            var projects = document.getElementById('projectfield').value;

            // Handle new lines in text areas
            academics = academics.replace(/\n/g, '\n');
            work = work.replace(/\n/g, '\n');
            projects = projects.replace(/\n/g, '\n');

            // Display resume
            document.getElementById('resumeName').textContent = name;
            document.getElementById('resumeContact').textContent = "Contact No: " + contact;
            document.getElementById('resumeEmail').textContent = "Email: " + email;
            document.getElementById('resumeAddress').textContent = "Address: " + address;
            document.getElementById('resumeLinkedIn').textContent = "LinkedIn: " + linkedin;
            document.getElementById('resumeInstagram').textContent = "Instagram: " + instagram;
            document.getElementById('resumeGitHub').textContent = "GitHub: " + github;
            document.getElementById('resumeAcademics').textContent = academics;
            document.getElementById('resumeWork').textContent = work;
            document.getElementById('resumeProjects').textContent = projects;

            // Show the resume section
            document.getElementById('resumeContainer').style.display = 'block';

            // Scroll to the top of the resume
            window.scrollTo(0, 0);
        }
    </script>
</body>
</html>

