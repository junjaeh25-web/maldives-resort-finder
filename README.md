<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Maldives Resort Finder</title>
  <style>
    body { font-family: Arial, sans-serif; text-align: center; background-color: #e0f7fa; color: #006064; }
    h1 { margin-top: 30px; font-size: 2.5em; }
    button { margin: 5px; padding: 10px 20px; font-size: 1em; cursor: pointer; border: none; border-radius: 5px; background-color: #00838f; color: white; }
    button:hover { background-color: #006064; }
    #resort-card img { border-radius: 10px; margin: 5px; }
  </style>
</head>
<body>
  <h1>Maldives Resort Finder</h1>
  <p>Answer 4 questions to find your perfect Maldives resort.</p>
  <button id="start-btn">Start</button>

  <div id="app" style="display:none;">
    <div id="questions">
      <p>1️⃣ Travel Purpose:</p>
      <button onclick="select('purpose','Honeymoon')">Honeymoon</button>
      <button onclick="select('purpose','Family')">Family</button>
      <button onclick="select('purpose','Relaxation')">Relaxation</button>
      <button onclick="select('purpose','Solo')">Solo</button>

      <p>2️⃣ Budget Level:</p>
      <button onclick="select('budget','Budget')">Budget</button>
      <button onclick="select('budget','Mid-range')">Mid-range</button>
      <button onclick="select('budget','Luxury')">Luxury</button>
      <button onclick="select('budget','High-end')">High-end</button>

      <p>3️⃣ Main Highlight:</p>
      <button onclick="select('strength','House reef')">House reef</button>
      <button onclick="select('strength','Room quality')">Room quality</button>
      <button onclick="select('strength','Food & Dining')">Food & Dining</button>
      <button onclick="select('strength','Privacy')">Privacy</button>

      <p>4️⃣ Accessibility:</p>
      <button onclick="select('accessibility','Very important')">Very important</button>
      <button onclick="select('accessibility','Moderate')">Moderate</button>
      <button onclick="select('accessibility','Not important')">Not important</button>
    </div>

    <div id="result">
      <h2>Recommended Resort:</h2>
      <div id="resort-card"></div>
    </div>
  </div>

  <script>
    const resorts = [
      {
        name: "One&Only Reethi Rah",
        atoll: "North Malé Atoll",
        purpose: ["Honeymoon","Relaxation"],
        budget: "High-end",
        strength: "Privacy",
        accessibility: "Very important",
        images: [
          "https://source.unsplash.com/200x150/?maldives,resort1",
          "https://source.unsplash.com/200x150/?maldives,resort2",
          "https://source.unsplash.com/200x150/?maldives,resort3"
        ],
        description: "Luxury resort offering ultimate privacy, stunning villas, and world-class dining.",
        links: {
          homepage: "https://www.oneandonly.com/reehi-rah",
          booking: "https://www.booking.com/oneandonly-reehi-rah",
          agoda: "https://www.agoda.com/oneandonly-reehi-rah",
          hotels: "https://www.hotels.com/oneandonly-reehi-rah",
          trip: "https://www.trip.com/oneandonly-reehi-rah"
        }
      },
      {
        name: "Baros Maldives",
        atoll: "North Malé Atoll",
        purpose: ["Honeymoon"],
        budget: "Luxury",
        strength: "House reef",
        accessibility: "Very important",
        images: [
          "https://source.unsplash.com/200x150/?maldives,resort4",
          "https://source.unsplash.com/200x150/?maldives,resort5",
          "https://source.unsplash.com/200x150/?maldives,resort6"
        ],
        description: "Romantic luxury resort with beautiful villas, amazing snorkeling, and excellent dining.",
        links: {
          homepage: "https://www.baros.com/",
          booking: "https://www.booking.com/baros-maldives",
          agoda: "https://www.agoda.com/baros-maldives",
          hotels: "https://www.hotels.com/baros-maldives",
          trip: "https://www.trip.com/baros-maldives"
        }
      }
    ];

    let userChoices = {};

    function select(category, value){
      userChoices[category] = value;
      recommend();
    }

    function recommend(){
      const resortCard = document.getElementById('resort-card');
      if(!userChoices.purpose || !userChoices.budget || !userChoices.strength || !userChoices.accessibility){
        resortCard.innerHTML = "<p>Please answer all questions!</p>";
        return;
      }

      const result = resorts.find(r =>
        r.purpose.includes(userChoices.purpose) &&
        r.budget === userChoices.budget &&
        r.strength === userChoices.strength &&
        r.accessibility === userChoices.accessibility
      );

      if(result){
        resortCard.innerHTML = `
          <h3>${result.name}</h3>
          <p>Atoll: ${result.atoll}</p>
          <p>${result.description}</p>
          <div>${result.images.map(img => `<img src="${img}" width="200"/>`).join('')}</div>
          <p>
            <a href="${result.links.homepage}" target="_blank">Homepage</a> |
            <a href="${result.links.booking}" target="_blank">Booking.com</a> |
            <a href="${result.links.agoda}" target="_blank">Agoda</a> |
            <a href="${result.links.hotels}" target="_blank">Hotels.com</a> |
            <a href="${result.links.trip}" target="_blank">Trip.com</a>
          </p>
        `;
      } else {
        resortCard.innerHTML = "<p>No matching resort found!</p>";
      }
    }

    document.getElementById('start-btn').onclick = function() {
      document.getElementById('start-btn').style.display = "none";
      document.getElementById('app').style.display = "block";
    };
  </script>
</body>
</html>
