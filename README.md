<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Crown Essence</title>

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">

  <!-- Icons -->
  <script src="https://unpkg.com/feather-icons"></script>

  <!-- Stripe.js for payments -->
  <script src="https://js.stripe.com/v3/"></script>

  <style>
    * { box-sizing: border-box; }
    html, body { scroll-behavior: smooth; }
    body {
      font-family: 'Poppins', sans-serif;
      margin: 0;
      background: linear-gradient(to right, #0a0a0a, #1a1a1a);
      color: #f0f0f0;
      transition: background 0.4s ease, color 0.4s ease;
    }
    body.light-theme {
      background: #ffffff;
      color: #000000;
    }
    header {
      background: linear-gradient(135deg, #8a2be2, #3498db);
      color: white;
      padding: 60px 20px;
      text-align: center;
      clip-path: ellipse(75% 100% at 50% 0%);
    }
    header h1 { font-size: 3em; margin: 0; }
    header p { font-size: 1.2em; margin-top: 10px; }

    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 20px;
      padding: 40px 20px;
    }
    .style {
      background: #2f2f4f;
      border-radius: 16px;
      overflow: hidden;
      box-shadow: 0 10px 20px rgba(0,0,0,0.5);
      text-align: center;
      transition: transform 0.3s ease, background 0.3s ease;
      position: relative;
    }
    .style:hover {
      transform: scale(1.05);
      background: #3a3a5f;
    }
    .style img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      display: block;
      border-bottom: 1px solid #444;
    }
    .style p {
      padding: 12px;
      font-weight: 500;
    }

    .booking-form {
      max-width: 700px;
      margin: 40px auto;
      background: #2f2f4f;
      padding: 30px;
      border-radius: 16px;
      box-shadow: 0 10px 20px rgba(0,0,0,0.4);
    }
    .booking-form h2 {
      text-align: center;
      color: #ffffff;
      margin-bottom: 20px;
    }
    .booking-form label {
      display: block;
      margin-top: 10px;
      font-weight: 500;
    }
    .booking-form input,
    .booking-form select,
    .booking-form textarea {
      width: 100%;
      padding: 12px;
      margin-top: 5px;
      border-radius: 8px;
      border: none;
      font-size: 1em;
    }
    .booking-form button {
      margin-top: 20px;
      width: 100%;
      padding: 14px;
      background-color: #8a2be2;
      color: white;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    .booking-form button:hover {
      background-color: #732d91;
    }
    .dark-toggle {
      position: fixed;
      top: 20px;
      right: 20px;
      background: #2c2c54;
      color: white;
      padding: 10px 14px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      z-index: 1000;
    }
    footer {
      background-color: #1f1f3b;
      color: white;
      text-align: center;
      padding: 30px;
    }
    .instagram-section {
      text-align: center;
      padding: 20px;
    }
    .instagram-section a {
      color: #8a2be2;
      font-weight: bold;
      text-decoration: none;
    }
  </style>
</head>
<body>

<button class="dark-toggle" onclick="toggleTheme()" title="Switch Theme"><i data-feather="sun"></i></button>

<header>
  <h1>Crown Essence</h1>
  <p>Royal Styles for Kings & Queens – Book Your Crown Today!</p>
</header>

<section class="gallery"></section>

<section class="booking-form">
  <h2>Book Your Appointment</h2>
  <form id="bookingForm">
    <label for="name">Full Name:</label>
    <input type="text" id="name" name="name" required>

    <label for="gender">Gender:</label>
    <select id="gender" name="gender" required>
      <option value="">Select Gender</option>
      <option value="Female">Female</option>
      <option value="Male">Male</option>
      <option value="Other">Other</option>
    </select>

    <label for="style">Select Style:</label>
    <select id="style" name="style" required></select>

    <label for="duration">Duration:</label>
    <select id="duration" name="duration" required>
      <option value="">Select Duration</option>
      <option value="1 hour">1 Hour</option>
      <option value="2 hours">2 Hours</option>
      <option value="3+ hours">3+ Hours</option>
    </select>

    <label for="date">Select Date:</label>
    <input type="date" id="date" name="date" required>

    <label for="time">Select Time:</label>
    <input type="time" id="time" name="time" required>

    <label for="deposit">Deposit Amount ($):</label>
    <input type="number" id="deposit" name="deposit" min="10" step="0.01" placeholder="Minimum $10" required>

    <label for="notes">Additional Notes (optional):</label>
    <textarea id="notes" name="notes" rows="3" placeholder="Tell us anything else we should know..."></textarea>

    <button type="submit">Confirm Booking</button>
  </form>
</section>

<section class="instagram-section">
  <h2>Follow Us on Instagram</h2>
  <p><a href="https://www.instagram.com/crownessence.vi/" target="_blank">@crownessence.vi</a></p>
  <img src="https://i.imgur.com/4M34hi2.png" alt="Instagram Preview" style="width:90%;max-width:400px;border-radius:16px;box-shadow:0 8px 16px rgba(0,0,0,0.3);margin-top:10px;">
</section>

<footer>
  <p><i data-feather="phone"></i> (123) 456-7890 | <i data-feather="mail"></i> info@crownessence.com</p>
  <p><i data-feather="map-pin"></i> 123 Queen's Way, Royal City</p>
</footer>

<script>
  feather.replace();

  const hairstyles = [
    { name: 'Box Braids', img: 'https://images.unsplash.com/photo-1590080876216-2f950c417cb9' },
    { name: 'Cornrows', img: 'https://images.unsplash.com/photo-1620819638426-8d129d3a63ee' },
    { name: 'Twist Out', img: 'https://images.unsplash.com/photo-1610805228010-c3ee6bc33db4' },
    { name: 'High Bun', img: 'https://images.unsplash.com/photo-1525072124605-497df6a9623f' },
    { name: 'Fulani Braids', img: 'https://images.unsplash.com/photo-1627497304541-0cb37b87806e' },
    { name: 'Passion Twists', img: 'https://images.unsplash.com/photo-1600185368184-bc10ef8a23b2' },
    { name: 'Braided Bun', img: 'https://images.unsplash.com/photo-1591183799321-5e1376716d1b' },
    { name: "Fade with Braids (Men)", img: "https://images.unsplash.com/photo-1531259683007-016a7b628fc6" }
  ];

  const gallery = document.querySelector('.gallery');
  const styleDropdown = document.getElementById('style');
  hairstyles.forEach(style => {
    const card = document.createElement('div');
    card.className = 'style';
    card.innerHTML = `<img src="${style.img}" alt="${style.name}" /><p>${style.name}</p>`;
    gallery.appendChild(card);

    const option = document.createElement('option');
    option.value = style.name;
    option.textContent = style.name;
    styleDropdown.appendChild(option);
  });

  function toggleTheme() {
    document.body.classList.toggle('light-theme');
  }

  document.getElementById('bookingForm').addEventListener('submit', function(event) {
    event.preventDefault();
    const deposit = parseFloat(document.getElementById('deposit').value);
    if (isNaN(deposit) || deposit < 10) {
      alert('A minimum deposit of $10 is required to book.');
      return;
    }
    alert('Thank you! Your appointment and deposit are confirmed.');
    this.reset();
  });
</script>

</body>
</html>
