
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Hotel SmartNotify</title>
  <style>
    /* (your existing CSS remains unchanged) */
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #f4f6f8;
      margin: 0;
      padding: 0 20px;
    }
    h1, h2 { color: #333; }
    nav {
      background: #fff;
      padding: 10px 0;
      display: flex;
      justify-content: center;
      gap: 20px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.05);
      margin-bottom: 20px;
    }
    nav a {
      text-decoration: none;
      color: #0077cc;
      font-weight: bold;
      cursor: pointer;
    }
    section { display: none; margin-top: 20px; }
    section.active { display: block; }
    .hero {
      background: #ffffff;
      padding: 50px 20px;
      border-radius: 12px;
      text-align: center;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }
    .hero h1 { font-size: 2em; margin-bottom: 10px; }
    .hero p { font-size: 1.2em; color: #333; }
    .hero button {
      padding: 10px 20px;
      margin: 20px 10px 0;
      background-color: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
      font-size: 1em;
      border-radius: 6px;
    }
    .pricing {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 20px;
      margin-top: 40px;
    }
    .plan {
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      width: 250px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      text-align: center;
    }
    .plan h3 { margin-bottom: 10px; }
    .plan p { font-size: 0.95em; color: #444; }
    .plan .price { font-size: 1.5em; margin: 10px 0; color: #4CAF50; }
    .plan a {
      display: inline-block;
      margin-top: 10px;
      padding: 8px 15px;
      background-color: #0077cc;
      color: white;
      text-decoration: none;
      border-radius: 6px;
    }
    form, table, .summary-card {
      background: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      margin-top: 20px;
    }
    label { display: block; margin-top: 10px; }
    input, select, button {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      background-color: #4CAF50;
      color: white;
      border: none;
      margin-top: 15px;
      cursor: pointer;
    }
    button:hover { background-color: #45a049; }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    th, td {
      border: 1px solid #ddd;
      padding: 8px;
      text-align: center;
    }
    th { background-color: #4CAF50; color: white; }
    .summary-card h3 { margin: 0 0 10px; }
  </style>
</head>

<body>

<h1>Hotel SmartNotify</h1>

<nav id="nav">
  <a onclick="showSection('landing')">Home</a>
  <a onclick="showSection('login')">Login</a>
  <a onclick="showSection('register')">Register</a>
</nav>

<!-- Landing Page -->
<section id="landing" class="active">
  <div class="hero">
    <h1>Welcome to Hotel SmartNotify</h1>
    <p>Stay in Control of Your Hotel Bookings, Get Instant Email Alerts, and Monitor Every Room—Streamline Your Inventory and Boost Your Efficiency, Anytime, Anywhere </p>
    <button onclick="showSection('login')">Login</button>
    <button onclick="showSection('register')">Register</button>
  </div>

  <div class="pricing">
    <div class="plan">
      <h3>Basic</h3>
      <p>For small hotel teams just getting started.</p>
      <div class="price">N20,000/mo</div>
      <p>Room & guest tracking</p>
      <p>Email support</p>
      <p>Report& summaries</p>
      <a href="https://selar.com/la1rv3" target="_blank">Buy Now</a>
    </div>
    <div class="plan">
      <h3>Pro</h3>
      <p>For growing hotel operations.</p>
      <div class="price">N70,000/mo</div>
      <p>Advanced booking dashboard</p>
      <p>Role-based access</p>
      <p>Reports & summaries</p>
      <p>Bar and Inventory management</p>
        <p>Profit Tracking,Forecasting,Analysis</p>
       <p>video ad creation</p>
      <a href="https://selar.com/la1rv3" target="_blank">Buy Now</a>
    </div>
    <div class="plan">
      <h3>Elite</h3>
      <p>Full control for chains & franchises.</p>
      <div class="price">N250,000</div>
      <p>Everything in pro</p>
      <p>Custom integrations</p>
      <p>Up to 5 hotels</p>
      <p>Team onboarding</p>
      <a href="https://selar.com/la1rv3" target="_blank">Buy Now</a>
    </div>
  </div>
</section>

<!-- Login -->
<section id="login">
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
  document.querySelectorAll("section").forEach(s => s.classList.remove("active"));
  document.getElementById(id).classList.add("active");
}

function handleRegister(event) {
  event.preventDefault();
  const user = {
    role: document.getElementById("role").value,
    username: document.getElementById("reg-username").value,
    email: document.getElementById("reg-email").value,
    password: document.getElementById("reg-password").value,
    payment_status: "unpaid" // Add default unpaid status
  };
  fetch(sheetdbUrl, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ data: user })
  })
  .then(res => res.json())
  .then(() => {
    alert("Registration successful! Please complete your payment to login.");
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
        if (user.payment_status !== "paid") {
          alert("Payment not completed. Please complete your payment before logging in.");
          return;
        }
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
    <a onclick="showSection('landing')">Home</a>
    <a onclick="showSection('login')">Login</a>
    <a onclick="showSection('register')">Register</a>`;
  showSection("landing");
}

const form = document.getElementById('bookingForm');
const tableBody = document.querySelector('#roomTable tbody');

form?.addEventListener('submit', function (e) {
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

