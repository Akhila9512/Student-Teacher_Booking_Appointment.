# Student-Teacher_Booking_Appointment.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fast Loading Booking System</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body { padding: 20px; font-family: Arial, sans-serif; }
        #app { max-width: 800px; margin: 0 auto; }
        .hidden { display: none; }
    </style>
</head>
<body>
    <div id="app">
        <h1 class="text-center mb-4">Booking System</h1>
        
        <!-- Login Section (Visible by default) -->
        <div id="loginSection">
            <div class="card">
                <div class="card-body">
                    <h3 class="card-title">Login</h3>
                    <form id="loginForm">
                        <div class="mb-3">
                            <label for="email" class="form-label">Email</label>
                            <input type="email" class="form-control" id="email" required>
                        </div>
                        <div class="mb-3">
                            <label for="password" class="form-label">Password</label>
                            <input type="password" class="form-control" id="password" required>
                        </div>
                        <button type="submit" class="btn btn-primary">Login</button>
                    </form>
                    <button id="showDemo" class="btn btn-secondary mt-3">ShowDemo</button>
                </div>
            </div>
        </div>

        <!-- Demo Content (Hidden by default) -->
        <div id="demoContent" class="hidden">
            <div class="card">
                <div class="card-body">
                    <h3 class="card-title">Available Teachers</h3>
                    <ul id="teacherList" class="list-group">
                        <!-- Teachers will appear here -->
                    </ul>
                </div>
            </div>
            
            <div class="card mt-4">
                <div class="card-body">
                    <h3 class="card-title">Book Appointment</h3>
                    <form id="bookingForm">
                        <div class="mb-3">
                            <label class="form-label">Teacher</label>
                            <select class="form-select" id="teacherSelect" required>
                                <option value="">Select a teacher</option>
                            </select>
                        </div>
                        <div class="mb-3">
                            <label class="form-label">Date</label>
                            <input type="date" class="form-control" id="appointmentDate" required>
                        </div>
                        <div class="mb-3">
                            <label class="form-label">Time</label>
                            <input type="time" class="form-control" id="appointmentTime" required>
                        </div>
                        <button type="submit" class="btn btn-primary">Book Now</button>
                    </form>
                </div>
            </div>
        </div>
    </div>

    <script>
        // DEMO DATA - This replaces Firebase for quick demonstration
        const demoData = {
            teachers: [
                { id: 1, name: "Dr. Smith", department: "Computer Science" },
                { id: 2, name: "Prof. Johnson", department: "Mathematics" },
                { id: 3, name: "Dr. Williams", department: "Physics" }
            ]
        };

        // DOM Elements
        const loginSection = document.getElementById('loginSection');
        const demoContent = document.getElementById('demoContent');
        const teacherList = document.getElementById('teacherList');
        const teacherSelect = document.getElementById('teacherSelect');
        const showDemoBtn = document.getElementById('showDemo');
        const loginForm = document.getElementById('loginForm');
        const bookingForm = document.getElementById('bookingForm');

        // Show demo content without authentication
        showDemoBtn.addEventListener('click', () => {
            loginSection.classList.add('hidden');
            demoContent.classList.remove('hidden');
            loadDemoData();
        });

        // Simulate login
        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            loginSection.classList.add('hidden');
            demoContent.classList.remove('hidden');
            loadDemoData();
        });

        // Simulate booking
        bookingForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const teacherId = teacherSelect.value;
            const date = document.getElementById('appointmentDate').value;
            const time = document.getElementById('appointmentTime').value;
            
            alert(`Appointment booked!\nTeacher: ${teacherSelect.options[teacherSelect.selectedIndex].text}\nDate: ${date}\nTime: ${time}`);
            
            // Reset form
            bookingForm.reset();
        });

        // Load demo data
        function loadDemoData() {
            // Clear existing lists
            teacherList.innerHTML = '';
            teacherSelect.innerHTML = '<option value="">Select a teacher</option>';
            
            // Populate teachers
            demoData.teachers.forEach(teacher => {
                // Add to teacher list
                const li = document.createElement('li');
                li.className = 'list-group-item';
                li.textContent = `${teacher.name} (${teacher.department})`;
                teacherList.appendChild(li);
                
                // Add to dropdown
                const option = document.createElement('option');
                option.value = teacher.id;
                option.textContent = `${teacher.name} (${teacher.department})`;
                teacherSelect.appendChild(option);
            });
        }

        // Set default date to tomorrow
        document.getElementById('appointmentDate').valueAsDate = new Date(Date.now() + 86400000);
    </script>
</body>
</html>
