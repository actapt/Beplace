# Beplace

<!DOCTYPE html>

<html lang="en">

<head>

  <meta charset="UTF-8" />

  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>

  <title>Hotel Role-Based Dashboard</title>

  <style>

    body {

      font-family: Arial, sans-serif;

      background: #f2f2f2;

      margin: 20px;

    }

    nav a {

      margin-right: 20px;

      text-decoration: none;

      color: blue;

      font-weight: bold;

      cursor: pointer;

    }

    section {

      display: none;

      margin-top: 20px;

    }

    section.active {

      display: block;

    }

    form, table, .summary-card {

      background: #fff;

      padding: 20px;

      border-radius: 8px;

      box-shadow: 0 2px 8px rgba(0,0,0,0.1);

      margin-top: 20px;

    }

    label {

      display: block;

      margin-top: 10px;

    }

    input, select, button {

      width: 100%;

      padding: 8px;

      margin-top: 5px;

    }

    button {

      margin-top: 15px;

      padding: 10px;

      background-color: #4CAF50;

      color: white;

      border: none;

      cursor: pointer;

    }

    button:hover {

      background-color: #45a049;

    }

    table {

      width: 100%;

      border-collapse: collapse;

    }

    th, td {

      border: 1px solid #ddd;

      padding: 8px;

      text-align: center;

    }

    th {

      background-color: #4CAF50;

      color: white;

    }

    .summary-card h3 {

      margin: 0 0 10px;

    }

  </style>

</head>

<body>


  <h1>Hotel Booking Management</h1>

  <nav id="nav">

    <a onclick="showSection('login')">Login</a>

    <a onclick="showSection('register')">Register</a>

  </nav>


  <!-- Login -->

  <section id="login" class="active">

    <h2>Login</h2>

    <form onsubmit="handleLogin(event)">

      <label>Email:</label>

      <input type="email" id="login-email" required>

      <label>Password:</label>

      <input type="password" id="login-password" required>

      <button type="submit">Login</button>

    </form>

  </section>


  <!-- Register -->

  <section id="register">

    <h2>Register</h2>

    <form onsubmit="handleRegister(event)">

      <label>Role:</label>

      <select id="role" required>

        <option value="business_owner">Business Owner</option>

        <option value="staff">Staff</option>

      </select>

      <label>Username:</label>

      <input type="text" id="reg-username" required>

      <label>Email:</label>

      <input type="email" id="reg-email" required>

      <label>Password:</label>

      <input type="password" id="reg-password" required>

      <button type="submit">Register</button>

    </form>

  </section>


  <!-- Staff Dashboard -->

  <section id="staff-dashboard">

    <h2>Room & Guest Management</h2>

    <form id="bookingForm">

      <label>Room Number:</label>

      <input type="text" id="room" required>

      <label>Status:</label>

      <select id="status">

        <option value="available">Available</option>

        <option value="booked">Booked</option>

        <option value="cleaned">Cleaned</option>

      </select>

      <label>Guest Name:</label>

      <input type="text" id="name" required>

      <label>Guest ID:</label>

      <input type="text" id="id" required>

      <label>Phone Number:</label>

      <input type="text" id="phone" required>

      <label>Check-in:</label>

      <input type="date" id="checkin" required>

      <label>Check-out:</label>

      <input type="date" id="checkout" required>

      <button type="submit">Submit Booking</button>

    </form>


    <table id="roomTable">

      <thead>

        <tr>

          <th>Room Number</th>

          <th>Status</th>

          <th>Guest Name</th>

          <th>ID</th>

          <th>Phone Number</th>

          <th>Check-in</th>

          <th>Check-out</th>

        </tr>

      </thead>

      <tbody></tbody>

    </table>

  </section>


  <!-- Business Owner Dashboard -->

  <section id="owner-dashboard">

    <h2>Booking Summary Dashboard</h2>

    <div class="summary-card">

      <h3>Total Bookings Today: <span id="totalBookings">0</span></h3>

      <h3>Available Rooms: <span id="availableRooms">0</span></h3>

      <h3>Cleaned Rooms: <span id="cleanedRooms">0</span></h3>

      <h3>Currently Booked: <span id="bookedRooms">0</span></h3>

    </div>

  </section>


  <script>

    const sheetdbUrl = 'https://sheetdb.io/api/v1/mtznundhcu9nm';


    function showSection(id) {

      document.querySelectorAll("section").forEach(section => section.classList.remove("active"));

      document.getElementById(id).classList.add("active");

    }


    function handleRegister(event) {

      event.preventDefault();

      const user = {

        role: document.getElementById("role").value,

        username: document.getElementById("reg-username").value,

        email: document.getElementById("reg-email").value,

        password: document.getElementById("reg-password").value

      };


      fetch(sheetdbUrl, {

        method: 'POST',

        headers: { 'Content-Type': 'application/json' },

        body: JSON.stringify({ data: user })

      })

      .then(res => res.json())

      .then(() => {

        alert("Registration successful! Please log in.");

        showSection("login");

      })

      .catch(err => {

        alert("Error registering. Please try again.");

        console.error(err);

      });

    }


    function handleLogin(event) {

      event.preventDefault();

      const email = document.getElementById("login-email").value;

      const password = document.getElementById("login-password").value;


      fetch(`${sheetdbUrl}/search?email=${email}&password=${password}`)

        .then(res => res.json())

        .then(data => {

          if (data.length > 0) {

            const user = data[0];

            localStorage.setItem("isLoggedIn", "true");

            localStorage.setItem("userRole", user.role);

            document.getElementById("nav").innerHTML = `<a onclick="logout()">Logout</a>`;


            if (user.role === "business_owner") {

              showSection("owner-dashboard");

              updateSummary();

            } else {

              showSection("staff-dashboard");

            }

          } else {

            alert("Invalid credentials.");

          }

        })

        .catch(err => {

          alert("Login failed.");

          console.error(err);

        });

    }


    function logout() {

      localStorage.clear();

      document.getElementById("nav").innerHTML = `

        <a onclick="showSection('login')">Login</a>

        <a onclick="showSection('register')">Register</a>`;

      showSection("login");

    }


    const form = document.getElementById('bookingForm');

    const tableBody = document.querySelector('#roomTable tbody');


    form.addEventListener('submit', function (e) {

      e.preventDefault();

      const formData = {

        "Room Number": document.getElementById('room').value,

        "Status": document.getElementById('status').value,

        "Guest Name": document.getElementById('name').value,

        "ID": document.getElementById('id').value,

        "Phone Number": document.getElementById('phone').value,

        "Check-in": document.getElementById('checkin').value,

        "Check-out": document.getElementById('checkout').value

      };


      addRowToTable(formData);

      storeBooking(formData);

      form.reset();


      fetch('https://sheetdb.io/api/v1/9aftey8lyyydz', {

        method: 'POST',

        headers: { 'Content-Type': 'application/json' },

        body: JSON.stringify({ data: formData })

      });


      fetch("https://formspree.io/f/meogjyqe", {

        method: "POST",

        headers: { 'Content-Type': 'application/json' },

        body: JSON.stringify(formData)

      });

    });


    function addRowToTable(data) {

      const row = document.createElement('tr');

      row.innerHTML = `

        <td>${data["Room Number"]}</td>

        <td>${data["Status"]}</td>

        <td>${data["Guest Name"]}</td>

        <td>${data["ID"]}</td>

        <td>${data["Phone Number"]}</td>

        <td>${data["Check-in"]}</td>

        <td>${data["Check-out"]}</td>

      `;

      tableBody.appendChild(row);

    }


    function storeBooking(data) {

      let bookings = JSON.parse(localStorage.getItem("bookings") || "[]");

      bookings.push(data);

      localStorage.setItem("bookings", JSON.stringify(bookings));

    }


    function updateSummary() {

      let bookings = JSON.parse(localStorage.getItem("bookings") || "[]");

      const today = new Date().toISOString().split('T')[0];


      const todaysBookings = bookings.filter(b => b["Check-in"] === today);

      const available = bookings.filter(b => b["Status"] === "available").length;

      const booked = bookings.filter(b => b["Status"] === "booked").length;

      const cleaned = bookings.filter(b => b["Status"] === "cleaned").length;


      document.getElementById("totalBookings").textContent = todaysBookings.length;

      document.getElementById("availableRooms").textContent = available;

      document.getElementById("bookedRooms").textContent = booked;

      document.getElementById("cleanedRooms").textContent = cleaned;

    }


    window.onload = () => {

      const loggedIn = localStorage.getItem("isLoggedIn");

      const role = localStorage.getItem("userRole");

      if (loggedIn === "true") {

        document.getElementById("nav").innerHTML = `<a onclick="logout()">Logout</a>`;

        if (role === "business_owner") {

          showSection("owner-dashboard");

          updateSummary();

        } else {

          showSection("staff-dashboard");

        }

      }

    };

  </script>

</body>

</html>


