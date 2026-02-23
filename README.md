<!DOCTYPE html>

<html lang="en">
 <head>
  <meta charset="utf-8"/>
  <meta content="width=device-width, initial-scale=1.0" name="viewport"/>
  <title>
   SK's 2026 Master – Mission Control
  </title>
  <!-- Leaflet CSS -->
  <link href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" rel="stylesheet"/>
  <link href="styles.css" rel="stylesheet"/>
 </head>
 <body>
  <!-- LOGIN SCREEN -->
  <div id="loginScreen">
   <div class="login-container">
    <h1>
     🌍 Executive Access
    </h1>
    <h3 style="text-align:center; color:#00bfff; margin-top:0;">
     SK's 2026 Master
    </h3>
    <input autocomplete="current-password" id="password" placeholder="Enter Access Code" type="password"/>
    <select id="roleSelect">
     <option value="viewer">
      Viewer Access
     </option>
     <option value="admin">
      Administrator
     </option>
    </select>
    <button onclick="login()">
     Enter Mission Control
    </button>
    <div class="error-message" id="errorMessage">
     Access Denied - Invalid Credentials
    </div>
    <p style="text-align:center; font-size:0.8em; color:#666; margin-top:20px;">
     Demo: Use password "elite2026"
    </p>
   </div>
  </div>
  <!-- DASHBOARD -->
  <div id="dashboard">
   <div class="header">
    <h1>
     🌍 SK's 2026 Master – Global Mission Control
    </h1>
    <div class="user-info">
     <span id="userRole">
      👤 Viewer
     </span>
     <button class="logout-btn" onclick="logout()">
      Logout
     </button>
    </div>
   </div>
   <div class="kpi-container">
    <div class="kpi">
     <h2>
      Total Workforce
     </h2>
     <h1 id="totalWorkforce">
      176
     </h1>
     <div class="trend">
      ↑ +8% this month
     </div>
    </div>
    <div class="kpi">
     <h2>
      Active Contracts
     </h2>
     <h1 id="activeContracts">
      7
     </h1>
     <div class="trend">
      → Stable
     </div>
    </div>
    <div class="kpi">
     <h2>
      Active Territories
     </h2>
     <h1 id="territories">
      5
     </h1>
     <div class="trend">
      ↑ +2 this quarter
     </div>
    </div>
    <div class="kpi">
     <h2>
      Monthly Revenue
     </h2>
     <h1 id="revenue">
      $2.4M
     </h1>
     <div class="trend">
      ↑ +12% vs last month
     </div>
    </div>
   </div>
   <div class="controls">
    <select id="contractFilter" onchange="filterContract()">
     <option value="all">
      All Contracts
     </option>
     <option value="Gymnation">
      Gymnation
     </option>
     <option value="Wellfit">
      Wellfit
     </option>
     <option value="Mercedes">
      Mercedes
     </option>
     <option value="Emirates">
      Emirates Facilities
     </option>
    </select>
    <button onclick="refreshData()">
     🔄 Refresh Data
    </button>
    <button onclick="toggleView()">
     🗺️ Toggle View
    </button>
   </div>
   <div class="map-container">
    <h2>
     📍 Global Operations Map
    </h2>
    <div id="map">
    </div>
   </div>
   <div class="map-container">
    <h2>
     🌐 3D Territory Visualization
    </h2>
    <div id="globe">
    </div>
   </div>
   <div class="stats-grid">
    <div class="stat-card">
     <h3>
      Top Locations
     </h3>
     <ul class="stat-list">
      <li>
       <span>
        Dubai
       </span>
       <span>
        82 staff
       </span>
      </li>
      <li>
       <span>
        Abu Dhabi
       </span>
       <span>
        58 staff
       </span>
      </li>
      <li>
       <span>
        Sharjah
       </span>
       <span>
        24 staff
       </span>
      </li>
      <li>
       <span>
        Ajman
       </span>
       <span>
        12 staff
       </span>
      </li>
     </ul>
    </div>
    <div class="stat-card">
     <h3>
      Contract Performance
     </h3>
     <ul class="stat-list">
      <li>
       <span>
        Gymnation
       </span>
       <span>
        95% ⭐
       </span>
      </li>
      <li>
       <span>
        Wellfit
       </span>
       <span>
        92% ⭐
       </span>
      </li>
      <li>
       <span>
        Mercedes
       </span>
       <span>
        98% ⭐
       </span>
      </li>
      <li>
       <span>
        Emirates
       </span>
       <span>
        89% ⭐
       </span>
      </li>
     </ul>
    </div>
   </div>
  </div>
  <!-- Scripts -->
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js">
  </script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js">
  </script>
  <script src="app.js">
  </script>
 </body>
</html>
