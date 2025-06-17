<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TRIDENT HUB</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #f0f4f8;
      color: #333;
    }
    
    .sidebar {
      width: 250px;
      position: fixed;
      top: 0;
      left: 0;
      bottom: 0;
      background-color: #1e3a8a;
      display: flex;
      flex-direction: column;
      padding: 20px;
      color: white;
    }

    .sidebar h1 {
      font-size: 20px;
      margin-bottom: 20px;
      font-weight: bold;
    }

    .sidebar-menu{
      flex-grow: 1;
    }
    
    .sidebar h1 {
      font-size: 22px;
      margin-bottom: 20px;
      letter-spacing: 0.5px;
    }
    
    .sidebar-item, .sub-tab {
      padding: 12px 16px;
      cursor: pointer;
      font-weight: 500;
      transition: background 0.3s;
    }
    
    .sidebar-item:hover {
      background: rgba(255, 255, 255, 0.1);
    }
    
    .sidebar-item-with-submenu:hover .submenu {
      max-height: 500px; /* Adjust based on submenu size */
      opacity: 1;
      margin-top: 5px;
    }

    
    .sidebar-item.active-tab {
      background: #2563eb;
      color: white;
    }

    .sidebar-footer {
      font-size: 13px;
      padding-top: 20px;
      border-top: 1px solid rgba(255, 255, 255, 0.2);
      color: #ddd;
      text-align: left;
    }
    
    .submenu {
      max-height: 0;
      opacity: 0;
      overflow: hidden;
      margin-left: 12px;
      margin-top: 0;
      padding-left: 10px;
      border-left: 2px solid rgba(255, 255, 255, 0.2);
      transition:
        max-height 0.5s ease,
        opacity 0.5s ease,
        margin-top 0.5s ease;
    }

    .sidebar-item-with-submenu:hover .submenu {
      max-height: 500px;
      opacity: 1;
      margin-top: 5px;
    }

    .sub-tab:hover {
      background-color: rgba(255, 255, 255, 0.1);
      color: white;
      transform: translateX(4px);
    }

    .sub-tab.active-tab {
      background-color: #2563eb;
      color: white;
    }

    
    .sidebar-item-with-submenu:hover .submenu {
      max-height: 1000px; /* large enough to fit the biggest submenu */
      opacity: 1;
      margin-top: 5px;
    }
    
    .main {
      margin-left: 250px;
      padding: 30px;
    }
    
    .card {
      background: #ffffff;
      padding: 30px;
      border-radius: 10px;
      margin-bottom: 30px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
    }
    
    .input-group {
      margin-bottom: 18px;
    }

    .input-group label {
      display: block;
      margin-bottom: 6px;
      color: #333;
      font-weight: 500;
    }
    
    .input-group input, .input-group select {
      width: 100%;
      padding: 10px 14px;
      border: 1px solid #ccc;
      border-radius: 6px;
      background-color: #f9fafb;
      font-size: 14px;
      transition: border 0.3s;
    }

    .input-group select {
      appearance: none;
      background-color: #f9fafb;
      padding: 10px 14px;
      height: 42px; /* Match input height */
      border-radius: 6px;
      border: 1px solid #ccc;
      font-size: 14px;
      width: 100%;
      font-family: inherit;
      line-height: 1.4;
      color: #333;
      background-image: url("data:image/svg+xml;utf8,<svg fill='gray' height='20' viewBox='0 0 24 24' width='20' xmlns='http://www.w3.org/2000/svg'><path d='M7 10l5 5 5-5z'/></svg>");
      background-repeat: no-repeat;
      background-position: right 10px center;
      background-size: 14px;
    }

    .input-group input:focus, .input-group select:focus {
      border-color: #2563eb;
      outline: none;
      background-color: #fff;
    }

    input::placeholder {
      color: #999;
      font-style: italic;
    }

    input[type="file"] {
      width: 100%;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 5px;
      font-family: inherit;
      font-size: 14px;
      background-color: white;
      box-sizing: border-box;
    }

    input[type="checkbox"] {
      margin-right: 8px;
    }

    h3, h4 {
      color: #1e3a8a;
      margin-top: 30px;
      margin-bottom: 10px;
    }

    select:invalid {
      color: #999;
      font-style: italic;
    }

    button {
      background-color: #2563eb;
      color: white;
      border: none;
      padding: 12px 20px;
      font-size: 14px;
      border-radius: 6px;
      cursor: pointer;
      transition: background 0.3s ease;
    }

    button:hover {
      background-color: #1e40af;
    }
    
    ul {
      padding-left: 20px;
    }
    
    .hidden {
      display: none;
    }
    
    .data-table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
      font-size: 14px;
      table-layout: auto;
    }

    .table-wrapper {
      overflow-x: auto;
      width: 100%;
    }

    
    .data-table th, .data-table td {
      border: 1px solid #ddd;
      padding: 10px;
      text-align: left;
      font-size: 14px;
    }
    
    .data-table th {
      background-color: #1e3a8a;
      color: white;
      position: sticky;
      top: 0;
      z-index: 1;
    }

    .data-table img {
      max-width: 60px;
      max-height: 60px;
      border-radius: 4px;
      cursor: pointer;
      margin: 3px;
      object-fit: cover;
    }
    
    .sidebar-item-with-submenu:hover .submenu {
      display: block;
    }

    .image-modal {
      display: none;
      position: fixed;
      z-index: 1000;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.8);
      justify-content: center;
      align-items: center;
    }

    .image-modal img {
      max-width: 90%;
      max-height: 90%;
      border-radius: 10px;
      box-shadow: 0 0 20px black;
      transition: transform 0.3s;
    }
    
    /* Custom checkbox */
    .checkbox-group {
      display: flex;
    align-items: center;
    gap: 10px;
    font-size: 14px;
    cursor: pointer;
    user-select: none;
    margin-bottom: 10px;
    }

    .checkbox-group input[type="checkbox"] {
      display: none;
    }

    .checkbox-custom {
      width: 18px;
      height: 18px;
      border: 2px solid #2563eb;
      border-radius: 4px;
      display: inline-block;
      position: relative;
      background-color: white;
      transition: background-color 0.3s ease, border 0.3s ease;
    }

    .checkbox-group input[type="checkbox"]:checked + .checkbox-custom {
    background-color: #2563eb;
    border-color: #2563eb;
    }

    .checkbox-group input[type="checkbox"]:checked + .checkbox-custom::after {
      content: "";
      position: absolute;
      left: 4px;
      top: 0px;
      width: 5px;
      height: 10px;
      border: solid white;
      border-width: 0 2px 2px 0;
      transform: rotate(45deg);
    }

    .checkbox-group input[type="checkbox"]:checked + .checkbox-custom::after {
      content: "";
      position: absolute;
      left: 4px;
      top: 0px;
      width: 5px;
      height: 10px;
      border: solid white;
      border-width: 0 2px 2px 0;
      transform: rotate(45deg);
    }

    .checkbox-group input[type="checkbox"]:checked + .checkbox-custom {
      background-color: #2563eb;
      border-color: #2563eb;
    }

    .checkbox-group input[type="radio"],
    .checkbox-group input[type="checkbox"] {
      display: none;
    }

    .checkbox-custom {
      width: 18px;
      height: 18px;
      border: 2px solid #2563eb;
      border-radius: 4px;
      display: inline-block;
      position: relative;
      background-color: white;
      transition: background-color 0.3s ease, border 0.3s ease;
    }

    .checkbox-group input[type="radio"]:checked + .checkbox-custom::after,
    .checkbox-group input[type="checkbox"]:checked + .checkbox-custom::after {
      content: "";
      position: absolute;
      left: 4px;
      top: 0px;
      width: 5px;
      height: 10px;
      border: solid white;
      border-width: 0 2px 2px 0;
      transform: rotate(45deg);
    }

    .checkbox-group input[type="radio"]:checked + .checkbox-custom,
    .checkbox-group input[type="checkbox"]:checked + .checkbox-custom {
      background-color: #2563eb;
      border-color: #2563eb;
    }

    /* arrow*/
    .arrow-icon {
      display: inline-block;
      margin-right: 10px;
      transition: transform 0.3s ease;
      font-size: 15px;
    }
    .arrow-rotate {
      transform: rotate(180deg);
    }

    .form-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

  </style>
</head>
<body>
  <div class="sidebar">
    <div class="sidebar-menu">
    <h1>TRIDENT HUB</h1>
      <div class="sidebar-item-with-submenu">
        <div class="sidebar-item" onclick="showTab('sales')">Sales Management</div>
      </div>

      <div class="sidebar-item-with-submenu">
        <div class="sidebar-item">Project Management</div>
        <div class="submenu">
          <div class="sub-tab" onclick="showTab('installation')">New Installation</div>
          <div class="sub-tab" onclick="showTab('modernization')">Modernization</div>
        </div>
      </div>

      <div class="sidebar-item-with-submenu">
        <div class="sidebar-item">Engineering Centre</div>
        <div class="submenu">
          <div class="sub-tab" onclick="showTab('designcentre')">Design Centre</div>
          <div class="sub-tab" onclick="showTab('testingncomm')">Testing & Commissioning</div>
        </div>
      </div>
  
      <div class="sidebar-item-with-submenu">
        <div class="sidebar-item">Service Operation</div>
        <div class="submenu">
          <div class="sub-tab" onclick="showTab('contracts')">Contracts</div>
          <div class="sub-tab" onclick="showTab('clients')">Clients</div>
          <div class="sub-tab" onclick="showTab('sites')">Site Management</div>
          <div class="sub-tab" onclick="showTab('equipments')">Equipments</div>
          <div class="sub-tab" onclick="showTab('pricing')">Pricing Calculator</div>
          <div class="sub-tab" onclick="showTab('maintenance')">Maintenance</div>
          <div class="sub-tab" onclick="showTab('service')">Service</div>
          <div class="sub-tab" onclick="showTab('mnc')">Real-Time Monitoring & Callback</div>
          <div class="sub-tab" onclick="showTab('repair')">Repair Management</div>
          <div class="sub-tab" onclick="showTab('parts')">Parts Management</div>
        </div>
      </div>

      <div class="sidebar-item-with-submenu">
        <div class="sidebar-item">Compliance & Quality</div>
        <div class="submenu">
          <div class="sub-tab" onclick="showTab('newinspec')">New Insatllation Inspection</div>
          <div class="sub-tab" onclick="showTab('renewinspec')">Renewal Inspection</div>
          <div class="sub-tab" onclick="showTab('quaterinspec')">Quaterly Inspection</div>
          <div class="sub-tab" onclick="showTab('safetyaudit')">Safety Audit</div>
          <div class="sub-tab" onclick="showTab('quataudit')">Quality Audit</div>
        </div>
      </div>
  
      <div class="sidebar-item-with-submenu">
        <div class="sidebar-item">Resource Management</div>
          <div class="submenu">
            <div class="sub-tab" onclick="showTab('hr')">Human Resource</div>
            <div class="sub-tab" onclick="showTab('tm')">Tools Management</div>
            <div class="sub-tab" onclick="showTab('subcont')">Sub-Contractor Management</div>
            <div class="sub-tab" onclick="showTab('ts')">Troubleshooting Support</div>
          </div>
        </div>
      </div>
  
      <div class="sidebar-footer">
        Logged in as: <span id="user-id">USER123</span>
      </div>
    </div>
  </div>
  <div class="main">
    <div id="installation-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('installation-form', this)"><span>Add New Installation Project</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="installation-form"><h4>Customer Details</h4>
        <div class="input-group"><label></label><input id="installation-contractno" type="text" placeholder="Contract No."></div>
        <div class="input-group"><label></label><input id="installation-date" type="text" placeholder="Award Date"></div>
        <div class="input-group">
          <label></label>
          <select id="installation-type">
            <option value="">Select Contract Type</option>
            <option>Direct Contract (DC)</option>
            <option>Nominated Sub-Contract (NSC)</option>
            <option>Domestic Sub-Contract (DSC)</option>
            <option>Others</option>
          </select>
        </div>
        <div class="input-group">
          <label></label>
          <select id="installation-client">
            <option value="">Select Client Type</option>
            <option>Owner / Developer</option>
            <option>Main-Contractor</option>
            <option>Architect</option>
            <option>M&E Consultant</option>
            <option>C&S Consultant</option>
            <option>Quantity Surveyer</option>
            <option>Others</option>
          </select>
        </div>
        <h4>Customer Details</h4>
        <div class="input-group"><label></label><input id="installation-company" type="text" placeholder="Company Name"></div>
        <div class="input-group"><label></label><input id="installation-address" type="text" placeholder="Address"></div>
        <div class="input-group"><label></label><input id="installation-postcode" type="text" placeholder="Postcode"></div>
        <div class="input-group"><label></label><input id="installation-phonenumber" type="text" placeholder="Phone Number"></div>
        <div class="input-group"><label></label><input id="installation-email" type="email" placeholder="Email"></div>
        <h4>PIC (Person-In-Charge)</h4>
        <div class="input-group"><label></label><input id="installation-picname" type="text" placeholder="Name"></div>
        <div class="input-group"><label></label><input id="installation-picphonenumber" type="text" placeholder="Phone Number"></div>
        <div class="input-group"><label></label><input id="installation-picemail" type="email" placeholder="Email"></div>

        <h4>Scope of Work (Scope of Preliminaries)</h4>
        <h5>Performance Bond</h5>
        <div class="input-group">
          <label class="checkbox-group">
            <input type="radio" name="installation-bond" id="installation-bond-bank" value="Bank Guarantee">
            <span class="checkbox-custom"></span>
            Bank Guarantee
          </label>
          <label class="checkbox-group">
            <input type="radio" name="installation-bond" id="installation-bond-director" value="Director Guarantee">
            <span class="checkbox-custom"></span>
            Director Guarantee
          </label>
        </div>
        <div class="input-group"><label></label><input id="installation-se" type="text" placeholder="Start/End"></div>
        <div class="input-group"><label></label><input id="installation-value" type="text" placeholder="Value"></div>
        <h5>Insurances Type</h5>
        <div class="input-group">
          <label class="checkbox-group">
            <input type="radio" name="installation-instype" id="installation-car" value="CAR">
            <span class="checkbox-custom"></span>
            Contractor All Risks (CAR)
          </label>
          <label class="checkbox-group">
            <input type="radio" name="installation-instype" id="installation-ear" value="EAR">
            <span class="checkbox-custom"></span>
            Erection All Risks (EAR)
          </label>
          <label class="checkbox-group">
            <input type="radio" name="installation-instype" id="installation-public" value="Public Liability">
            <span class="checkbox-custom"></span>
            Public Liability
          </label>
          <label class="checkbox-group">
            <input type="radio" name="installation-instype" id="installation-workman" value="Workman Compensation">
            <span class="checkbox-custom"></span>
            Workman Compensation
          </label>
        </div>
        <h5>Insurances Provider</h5>
        <div class="input-group" id="installation-provider-group" style="display: none;">
          <label class="checkbox-group">
            <input type="radio" name="installation-provider" id="installation-main" value="Main Contractor">
            <span class="checkbox-custom"></span>
           Provided by Main Contractor
          </label>
          <label class="checkbox-group">
            <input type="radio" name="installation-provider" id="installation-trident" value="Trident">
            <span class="checkbox-custom"></span>
            Provided by Trident
          </label>
        </div>
        <h5>Liquidated Ascertained Damages</h5>
        <div class="input-group"><input id="installation-lad-amount" type="text" placeholder="Amount"></div>
        <div class="input-group"><input id="installation-lad-limit" type="text" placeholder="Limit"></div>
        <h5>Defects Liability Period</h5>
        <div class="input-group"><input id="installation-dlp-duration" type="text" placeholder="Duration"></div>
        <div class="input-group"><input id="installation-dlp-other" type="text" placeholder="Others"></div>
        <h5>Equipment Summary</h5>
        <div class="input-group"><input id="installation-equipsummary" type="text" placeholder="Summary"></div>
        <div class="input-group"><input id="installation-equipothers" type="text" placeholder="Others"></div>
        <h5>Proposed Work Schedule</h5>
        <div class="input-group"><input id="installation-commencementdate" type="text" placeholder="Commencement Date"></div>
        <div class="input-group"><input id="installation-completiondate" type="text" placeholder="Completion Date"></div>
        <h5>Contract Sum</h5>
        <div class="input-group"><input id="installation-pricesummary" type="text" placeholder="Price Summary"></div>
        <h5>Payment Terms</h5>
        <div class="input-group"><input id="installation-downpayment" type="text" placeholder="Downpayment"></div>
        <div class="input-group"><input id="installation-retention" type="text" placeholder="Retention"></div>
        <div class="input-group"><input id="installation-vo" type="text" placeholder="Variation Orders"></div>
        <button onclick="saveInstallation()">Save New Installation Project</button>
        </div>
      </div>
      <div class="card">
        <h3>New Installation List</h3>
        <input type="text" id="search-installation" placeholder="Search installation..." oninput="filterTable('installation-list', this.value)">
        <div class="table-wrapper">
        <table id="installation-list" class="data-table">
          <thead>
            <tr>
              <th>Contract No.</th>
              <th>Award Date</th>
              <th>Customer Type</th>
              <th>Client Type</th>
              <th>Company Name</th>
              <th>Address</th>
              <th>Postcode</th>
              <th>Phone Number</th>
              <th>Email</th>
              <th>PIC Name</th>
              <th>PIC Phone Number</th>
              <th>PIC Email</th>
              <th>Performance Bond</th>
              <th>Insurance Type</th>
              <th>Provided By</th>
              <th>LAD Amount</th>
              <th>LAD Limit</th>
              <th>DLP Duration</th>
              <th>DLP Others</th>
              <th>Equip Summary</th>
              <th>Equip Others</th>
              <th>Commencement Date</th>
              <th>Completion Date</th>
              <th>Price Summary</th>
              <th>Downpayment</th>
              <th>Retention</th>
              <th>Variation Orders</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>

    <div id="modernization-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('modernization-form', this)"><span>Add New Modernization Project</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="modernization-form"><h4>Customer Details</h4>
        <div class="input-group"><label></label><input id="modernization-contractno" type="text" placeholder="Contract No."></div>
        <div class="input-group"><label></label><input id="modernization-date" type="text" placeholder="Award Date"></div>
        <div class="input-group">
          <label></label>
          <select id="modernization-type">
            <option value="">Select Contract Type</option>
            <option>Direct Contract (DC)</option>
            <option>Nominated Sub-Contract (NSC)</option>
            <option>Domestic Sub-Contract (DSC)</option>
            <option>Others</option>
          </select>
        </div>
        <div class="input-group">
          <label></label>
          <select id="modernization-client">
            <option value="">Select Client Type</option>
            <option>Owner / Developer</option>
            <option>Main-Contractor</option>
            <option>Architect</option>
            <option>M&E Consultant</option>
            <option>C&S Consultant</option>
            <option>Quantity Surveyer</option>
            <option>Others</option>
          </select>
        </div>
        <h4>Customer Details</h4>
        <div class="input-group"><label></label><input id="modernization-company" type="text" placeholder="Company Name"></div>
        <div class="input-group"><label></label><input id="modernization-address" type="text" placeholder="Address"></div>
        <div class="input-group"><label></label><input id="modernization-postcode" type="text" placeholder="Postcode"></div>
        <div class="input-group"><label></label><input id="modernization-phonenumber" type="text" placeholder="Phone Number"></div>
        <div class="input-group"><label></label><input id="modernization-email" type="email" placeholder="Email"></div>
        <h4>PIC (Person-In-Charge)</h4>
        <div class="input-group"><label></label><input id="modernization-picname" type="text" placeholder="Name"></div>
        <div class="input-group"><label></label><input id="modernization-picphonenumber" type="text" placeholder="Phone Number"></div>
        <div class="input-group"><label></label><input id="modernization-picemail" type="email" placeholder="Email"></div>

        <h4>Scope of Work (Scope of Preliminaries)</h4>
        <h5>Performance Bond</h5>
        <div class="input-group">
          <label class="checkbox-group">
            <input type="radio" name="modernization-bond" id="modernization-bond-bank" value="Bank Guarantee">
            <span class="checkbox-custom"></span>
            Bank Guarantee
          </label>
          <label class="checkbox-group">
            <input type="radio" name="modernization-bond" id="modernization-bond-director" value="Director Guarantee">
            <span class="checkbox-custom"></span>
            Director Guarantee
          </label>
        </div>
        <div class="input-group"><label></label><input id="modernization-se" type="text" placeholder="Start/End"></div>
        <div class="input-group"><label></label><input id="modernization-value" type="text" placeholder="Value"></div>
        <h5>Insurances Type</h5>
        <div class="input-group">
          <label class="checkbox-group">
            <input type="radio" name="modernization-instype" id="modernization-car" value="CAR">
            <span class="checkbox-custom"></span>
            Contractor All Risks (CAR)
          </label>
          <label class="checkbox-group">
            <input type="radio" name="modernization-instype" id="modernization-ear" value="EAR">
            <span class="checkbox-custom"></span>
            Erection All Risks (EAR)
          </label>
          <label class="checkbox-group">
            <input type="radio" name="modernization-instype" id="modernization-public" value="Public Liability">
            <span class="checkbox-custom"></span>
            Public Liability
          </label>
          <label class="checkbox-group">
            <input type="radio" name="modernization-instype" id="modernization-workman" value="Workman Compensation">
            <span class="checkbox-custom"></span>
            Workman Compensation
          </label>
        </div>
        <h5>Insurances Provider</h5>
        <div class="input-group" id="modernization-provider-group" style="display: none;">
          <label class="checkbox-group">
            <input type="radio" name="modernization-provider" id="modernization-main" value="Main Contractor">
            <span class="checkbox-custom"></span>
           Provided by Main Contractor
          </label>
          <label class="checkbox-group">
            <input type="radio" name="modernization-provider" id="modernization-trident" value="Trident">
            <span class="checkbox-custom"></span>
            Provided by Trident
          </label>
        </div>
        <h5>Liquidated Ascertained Damages</h5>
        <div class="input-group"><input id="modernization-lad-amount" type="text" placeholder="Amount"></div>
        <div class="input-group"><input id="modernization-lad-limit" type="text" placeholder="Limit"></div>
        <h5>Defects Liability Period</h5>
        <div class="input-group"><input id="modernization-dlp-duration" type="text" placeholder="Duration"></div>
        <div class="input-group"><input id="modernization-dlp-other" type="text" placeholder="Others"></div>
        <h5>Equipment Summary</h5>
        <div class="input-group"><input id="modernization-equipsummary" type="text" placeholder="Summary"></div>
        <div class="input-group"><input id="modernization-equipothers" type="text" placeholder="Others"></div>
        <h5>Proposed Work Schedule</h5>
        <div class="input-group"><input id="modernization-commencementdate" type="text" placeholder="Commencement Date"></div>
        <div class="input-group"><input id="modernization-completiondate" type="text" placeholder="Completion Date"></div>
        <h5>Contract Sum</h5>
        <div class="input-group"><input id="modernization-pricesummary" type="text" placeholder="Price Summary"></div>
        <h5>Payment Terms</h5>
        <div class="input-group"><input id="modernization-downpayment" type="text" placeholder="Downpayment"></div>
        <div class="input-group"><input id="modernization-retention" type="text" placeholder="Retention"></div>
        <div class="input-group"><input id="modernization-vo" type="text" placeholder="Variation Orders"></div>
        <button onclick="saveModernization()">Save New Modernization Project</button>
        </div>
      </div>
      <div class="card">
        <h3>Modernization List</h3>
        <input type="text" id="search-modernization" placeholder="Search modernization..." oninput="filterTable('modernization-list', this.value)">
        <div class="table-wrapper">
        <table id="modernization-list" class="data-table">
          <thead>
            <tr>
              <th>Contract No.</th>
              <th>Award Date</th>
              <th>Customer Type</th>
              <th>Client Type</th>
              <th>Company Name</th>
              <th>Address</th>
              <th>Postcode</th>
              <th>Phone Number</th>
              <th>Email</th>
              <th>PIC Name</th>
              <th>PIC Phone Number</th>
              <th>PIC Email</th>
              <th>Performance Bond</th>
              <th>Insurance Type</th>
              <th>Provided By</th>
              <th>LAD Amount</th>
              <th>LAD Limit</th>
              <th>DLP Duration</th>
              <th>DLP Others</th>
              <th>Equip Summary</th>
              <th>Equip Others</th>
              <th>Commencement Date</th>
              <th>Completion Date</th>
              <th>Price Summary</th>
              <th>Downpayment</th>
              <th>Retention</th>
              <th>Variation Orders</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>

    <div id="contracts-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('contracts-form', this)"><span>Add Contract</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="contracts-form">
        <div class="input-group"><input id="contracts-no" placeholder="Contract No."></div>
        <div class="input-group"><input id="contracts-date" placeholder="Commencement Date"></div>
        <div class="input-group"><input id="contracts-expiry" placeholder="Expiry Date"></div>
        <div class="input-group">
          <label for="contracts-type"></label>
            <select id="contracts-type" required>
              <option value="" disabled selected>Select Type</option>
              <option value="Comprehensive">Comprehensive</option>
              <option value="SemiComprehensive">Semi-Comprehensive</option>
              <option value="General">General</option>
              <option value="Defects">Defects Liability Period</option>
            </select>
        </div>
        <div class="input-group"><input id="contracts-included" placeholder="Included"></div>
        <div class="input-group"><input id="contracts-excluded" placeholder="Excluded"></div>
        <div class="input-group"><input id="contracts-price" placeholder="Price"></div>
        <button onclick="saveContract()">Save Contract</button>
        </div>
      </div>
      <div class="card">
        <h3>Contract List</h3>
        <input type="text" id="search-contracts" placeholder="Search contracts..." oninput="filterTable('contracts-list', this.value)">
        <div class="table-wrapper">
        <table id="contracts-list" class="data-table">
          <thead>
            <tr>
              <th>Contract No.</th><th>Commencement Date</th><th>Expiry Date</th><th>Type of Contract</th><th>Included</th><th>Excluded</th><th>Pricing</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>

    <div id="clients-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('clients-form', this)"><span>Add Client</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="clients-form">
        <div class="input-group">
          <label></label>
          <input id="clients-name" type="text" placeholder="Enter customer name">
        </div>
        <div class="input-group">
          <label></label>
          <select id="clients-type">
            <option value="">Select Customer Role</option>
            <option>Owner</option>
            <option>Tenant</option>
            <option>Building Manager</option>
            <option>Others</option>
          </select>
        </div>
        <div class="input-group"><label></label><input id="clients-address" type="text" placeholder="Address"></div>
        <div class="input-group"><label></label><input id="clients-postcode" type="text" placeholder="Postcode"></div>
        <div class="input-group"><label></label><input id="clients-phonenumber" type="text" placeholder="Phone Number"></div>
        <div class="input-group"><label></label><input id="clients-email" type="email" placeholder="Email"></div>

        <h4>PIC (Person-In-Charge)</h4>
        <div class="input-group"><label></label><input id="clients-pic-name" type="text" placeholder="Name"></div>
        <div class="input-group"><label></label><input id="clients-pic-phonenumber" type="text" placeholder="Phone Number"></div>
        <div class="input-group"><label></label><input id="clients-pic-email" type="email" placeholder="Email"></div>

        <h3>Billing Address</h3>
        <div class="input-group">
          <label class="checkbox-group">
            <input type="checkbox" id="clients-billing-same" onchange="toggleClientsBillingAddress()">
            <span class="checkbox-custom"></span>
            Same as Contracted Customer Address
          </label>
        </div>
        <div id="clients-billing-fields">
          <div class="input-group"><label>Address</label><input type="text"></div>
          <div class="input-group"><label>Postcode</label><input type="text"></div>
          <div class="input-group"><label>Tel.</label><input type="text"></div>
          <div class="input-group"><label>Email</label><input type="email"></div>
        </div>

        <h3>Owner</h3>
        <div class="input-group">
          <label class="checkbox-group">
            <input type="checkbox" id="clients-owner-same" onchange="toggleClientsOwnerAddress()">
            <span class="checkbox-custom"></span>
            Same as Contracted Customer Address
          </label>
        </div>
        <div id="clients-owner-fields">
          <div class="input-group"><label>Address</label><input type="text"></div>
          <div class="input-group"><label>Postcode</label><input type="text"></div>
          <div class="input-group"><label>Tel.</label><input type="text"></div>
          <div class="input-group"><label>Email</label><input type="email"></div>
        </div>
        <button onclick="saveClient()">Save Client Info</button>
        </div>
      </div>
      <div class="card">
        <h3>Client List</h3>
        <input type="text" id="search-clients" placeholder="Search client..." oninput="filterTable('clients-list', this.value)">
        <div class="table-wrapper">
        <table id="clients-list" class="data-table">
          <thead>
            <tr>
              <th>Customer Name</th>
              <th>Customer Type</th>
              <th>Address</th>
              <th>Postcode</th>
              <th>Phone Number</th>
              <th>Email</th>
              <th>PIC Name</th>
              <th>PIC Phone Number</th>
              <th>PIC Email</th>
              <th>Billing Address</th>
              <th>Billing Postcode</th>
              <th>Billing Tel.</th>
              <th>Billing Email</th>
              <th>Owner Address</th>
              <th>Owner Postcode</th>
              <th>Owner Tel.</th>
              <th>Owner Email</th>
              <th>Pricing</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>

    <div id="sites-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('sites-form', this)"><span>Add Site</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="sites-form">
        <div class="input-group"><input id="site-name" placeholder="Site Name"></div>
        <div class="input-group">
          <label for="site-type"></label>
            <select id="site-type" required>
              <option value="" disabled selected>Select Type</option>
              <option value="New Installation">New Installation</option>
              <option value="Modernization">Modernization</option>
            </select>
        </div>
        <div class="input-group"><input id="site-address" placeholder="Site Address"></div>
        <div class="input-group"><input id="site-latitude" placeholder="Latitude"></div>
        <div class="input-group"><input id="site-longtitude" placeholder="Longtitude"></div>
        <button onclick="saveSites()">Save Site</button>
        </div>
      </div>
      <div class="card">
        <h3>Sites List</h3>
        <input type="text" id="search-sites" placeholder="Search sites..." oninput="filterTable('sites-list', this.value)">
        <div class="table-wrapper">
        <table id="sites-list" class="data-table">
          <thead>
            <tr>
              <th>Site Name</th><th>Site Type</th><th>Site Address</th><th>Latitude</th><th>Longtitude</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>

    <div id="pricing-tab" class="tab hidden">
      <div class="card">
        <h2>Pricing Calculator</h2>
        <table class="data-table" id="pricing-table">
          <thead>
            <tr>
              <th>Unit No.</th><th>PMA No.</th><th>Price/month (RM)</th><th>Include SST (8%)</th><th>Total with Tax (RM)</th>
              <th></th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        <button onclick="savePricingRow()">Add Unit</button>
        <br><br>
      </div>
    </div>


    <div id="equipments-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('equipments-form', this)"><span>Add Equipment</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="equipments-form">
        <div class="input-group"><input id="equip-liftnumber" placeholder="Lift Numbering as at Site"></div>
        <div class="input-group"><input id="equip-owner-name" placeholder="Owner Name"></div>
        <div class="input-group"><input id="equip-owner-workplacenumber" placeholder="Workplace Number"></div>
        <div class="input-group"><input id="equip-owner-correspondencesadd" placeholder="Correspondence Address"></div>
        <div class="input-group"><input id="equip-resident-name" placeholder="Resident Name"></div>
        <div class="input-group"><input id="equip-resident-workplacenumber" placeholder="Workplace Number"></div>
        <div class="input-group"><input id="equip-resident-correspondencesadd" placeholder="Correspondence Address"></div>
        <div class="input-group"><input id="equip-lastinspec" placeholder="Last Inspection Date"></div>
        <div class="input-group"><input id="equip-resnumber" placeholder="Resgistration Number (PMA No.)"></div>
        <div class="input-group"><input id="equip-expired" placeholder="Expiry Date"></div>
        <div class="input-group"><input id="equip-location" placeholder="Location"></div>
        <div class="input-group"><input id="equip-serialnumber" placeholder="Serial No."></div>
        <div class="input-group"><input id="equip-manufacture" placeholder="Manufacturer"></div>
        <div class="input-group"><input id="equip-rate" placeholder="Monthly Rate"></div>
        <div class="input-group">
          <label>Equipment Type:</label>
          <select id="equip-type" onchange="toggleEquipmentFields(this.value)">
            <option value="">Select Type</option>
            <option value="Elevator">Elevator</option>
            <option value="Escalator">Escalator</option>
            <option value="Travolator">Travolator</option>
            <option value="Dumbwaiter">Dumbwaiter</option>
            <option value="PlatformLift">Platform Lift</option>
            <option value="GoodsHoist">Goods Hoist</option>
            <option value="Stairlift">Stairlift</option>
            <option value="HomeLift">Home Lift</option>
          </select>
        </div>
        <div id="Elevator-fields" class="equipments-details hidden">
          <div class="input-group"><label>Brand:</label><input type="text" id="equip-brand"/></div>
          <div class="input-group"><label>Model Name:</label><input type="text" id="equip-modelname"/></div>
          <div class="input-group"><label>Capacity (kg):</label><input type="text" id="equip-capacitykg"/></div>
          <div class="input-group"><label>Capacity (persons):</label><input type="text" id="equip-capacityper"/></div>
          <div class="input-group"><label>Speed (m/m):</label><input type="text" id="equip-speed"/></div>
          <div class="input-group"><label>Rise (m):</label><input type="text" id="equip-rise"/></div>
          <div class="input-group"><label>Stops / Openings:</label><input type="text" id="equip-so"/></div>
          <div class="input-group"><label>Machine Type:</label><input type="text" id="equip-machinetype"/></div>
          <div class="input-group"><label>Motor Data:</label><input type="text" id="equip-motordata"/></div>
          <div class="input-group"><label>Controller:</label><input type="text" id="equip-controller"/></div>
          <div class="input-group"><label>Software Version:</label><input type="text" id="equip-softver"/></div>
          <div class="input-group"><label>Operation:</label><input type="text" id="equip-operation"/></div>
          <div class="input-group"><label>Roping:</label><input type="text" id="equip-roping"/></div>
          <div class="input-group"><label>Rope Diameter:</label><input type="text" id="equip-ropediameter"/></div>
          <div class="input-group"><label>Rope Construction / Made:</label><input type="text" id="equip-ropeconstruction"/></div>
        </div>

        <div id="Escalator-fields" class="equipments-details hidden">
          <div class="input-group"><label>Brand:</label><input type="text" id="equip-brand"/></div>
          <div class="input-group"><label>Model Name:</label><input type="text" id="equip-modelname"/></div>
          <div class="input-group"><label>Capacity (kg):</label><input type="text" id="equip-capacitykg"/></div>
          <div class="input-group"><label>Rise (m):</label><input type="text" id="equip-rise"/></div>
          <div class="input-group"><label>Stepwidth (mm):</label><input type="text" id="equip-stepwidth"/></div>
          <div class="input-group"><label>Inclination:</label><input type="text" id="equip-inclination"/></div>
          <div class="input-group"><label>Machine Type:</label><input type="text" id="equip-machinetype"/></div>
          <div class="input-group"><label>Motor Data:</label><input type="text" id="equip-motordata"/></div>
          <div class="input-group"><label>Controller:</label><input type="text" id="equip-controller"/></div>
          <div class="input-group"><label>Software Version:</label><input type="text" id="equip-softver"/></div>
          <div class="input-group"><label>Operation:</label><input type="text" id="equip-operation"/></div>
          <div class="input-group"><label>Rope Diameter:</label><input type="text" id="equip-ropediameter"/></div>
          <div class="input-group"><label>Rope Construction / Made:</label><input type="text" id="equip-ropeconstruction"/></div>
        </div>

        <div id="Travolator-fields" class="equipments-details hidden">
          <div class="input-group"><label>Brand:</label><input type="text" id="equip-brand"/></div>
          <div class="input-group"><label>Model Name:</label><input type="text" id="equip-modelname"/></div>
          <div class="input-group"><label>Capacity (kg):</label><input type="text" id="equip-capacitykg"/></div>
          <div class="input-group"><label>Rise (m):</label><input type="text" id="equip-rise"/></div>
          <div class="input-group"><label>Stepwidth (mm):</label><input type="text" id="equip-stepwidth"/></div>
          <div class="input-group"><label>Inclination:</label><input type="text" id="equip-inclination"/></div>
          <div class="input-group"><label>Machine Type:</label><input type="text" id="equip-machinetype"/></div>
          <div class="input-group"><label>Motor Data:</label><input type="text" id="equip-motordata"/></div>
          <div class="input-group"><label>Controller:</label><input type="text" id="equip-controller"/></div>
          <div class="input-group"><label>Software Version:</label><input type="text" id="equip-softver"/></div>
          <div class="input-group"><label>Operation:</label><input type="text" id="equip-operation"/></div>
          <div class="input-group"><label>Rope Diameter:</label><input type="text" id="equip-ropediameter"/></div>
          <div class="input-group"><label>Rope Construction / Made:</label><input type="text" id="equip-ropeconstruction"/></div>
        </div>

        <div id="Dumbwaiter-fields" class="equipments-details hidden">
          <div class="input-group"><label>Brand:</label><input type="text" id="equip-brand"/></div>
          <div class="input-group"><label>Model Name:</label><input type="text" id="equip-modelname"/></div>
          <div class="input-group"><label>Capacity (kg):</label><input type="text" id="equip-capacitykg"/></div>
          <div class="input-group"><label>Speed (m/m):</label><input type="text" id="equip-speed"/></div>
          <div class="input-group"><label>Rise (m):</label><input type="text" id="equip-rise"/></div>
          <div class="input-group"><label>Stops / Openings:</label><input type="text" id="equip-so"/></div>
          <div class="input-group"><label>Machine Type:</label><input type="text" id="equip-machinetype"/></div>
          <div class="input-group"><label>Motor Data:</label><input type="text" id="equip-motordata"/></div>
          <div class="input-group"><label>Controller:</label><input type="text" id="equip-controller"/></div>
          <div class="input-group"><label>Software Version:</label><input type="text" id="equip-softver"/></div>
          <div class="input-group"><label>Operation:</label><input type="text" id="equip-operation"/></div>
          <div class="input-group"><label>Roping:</label><input type="text" id="equip-roping"/></div>
          <div class="input-group"><label>Rope Diameter:</label><input type="text" id="equip-ropediameter"/></div>
          <div class="input-group"><label>Rope Construction / Made:</label><input type="text" id="equip-ropeconstruction"/></div>
        </div>

        <div id="PlatformLift-fields" class="equipments-details hidden">
          <div class="input-group"><label>Brand:</label><input type="text" id="equip-brand"/></div>
          <div class="input-group"><label>Model Name:</label><input type="text" id="equip-modelname"/></div>
          <div class="input-group"><label>Capacity (kg):</label><input type="text" id="equip-capacitykg"/></div>
          <div class="input-group"><label>Capacity (persons):</label><input type="text" id="equip-capacityper"/></div>
          <div class="input-group"><label>Speed (m/m):</label><input type="text" id="equip-speed"/></div>
          <div class="input-group"><label>Rise (m):</label><input type="text" id="equip-rise"/></div>
          <div class="input-group"><label>Stops / Openings:</label><input type="text" id="equip-so"/></div>
          <div class="input-group"><label>Machine Type:</label><input type="text" id="equip-machinetype"/></div>
          <div class="input-group"><label>Motor Data:</label><input type="text" id="equip-motordata"/></div>
          <div class="input-group"><label>Controller:</label><input type="text" id="equip-controller"/></div>
          <div class="input-group"><label>Software Version:</label><input type="text" id="equip-softver"/></div>
          <div class="input-group"><label>Operation:</label><input type="text" id="equip-operation"/></div>
          <div class="input-group"><label>Roping:</label><input type="text" id="equip-roping"/></div>
          <div class="input-group"><label>Rope Diameter:</label><input type="text" id="equip-ropediameter"/></div>
          <div class="input-group"><label>Rope Construction / Made:</label><input type="text" id="equip-ropeconstruction"></div>
        </div>

        <div id="GoodsHoist-fields" class="equipments-details hidden">
          <div class="input-group"><label>Brand:</label><input type="text" id="equip-brand"/></div>
          <div class="input-group"><label>Model Name:</label><input type="text" id="equip-modelname"/></div>
          <div class="input-group"><label>Capacity (kg):</label><input type="text" id="equip-capacitykg"/></div>
          <div class="input-group"><label>Speed (m/m):</label><input type="text" id="equip-speed"/></div>
          <div class="input-group"><label>Rise (m):</label><input type="text" id="equip-rise"/></div>
          <div class="input-group"><label>Stops / Openings:</label><input type="text" id="equip-so"/></div>
          <div class="input-group"><label>Machine Type:</label><input type="text" id="equip-machinetype"/></div>
          <div class="input-group"><label>Motor Data:</label><input type="text" id="equip-motordata"/></div>
          <div class="input-group"><label>Controller:</label><input type="text" id="equip-controller"/></div>
          <div class="input-group"><label>Software Version:</label><input type="text" id="equip-softver"/></div>
          <div class="input-group"><label>Operation:</label><input type="text" id="equip-operation"/></div>
          <div class="input-group"><label>Roping:</label><input type="text" id="equip-roping"/></div>
          <div class="input-group"><label>Rope Diameter:</label><input type="text" id="equip-ropediameter"/></div>
          <div class="input-group"><label>Rope Construction / Made:</label><input type="text" id="equip-ropeconstruction"/></div>
        </div>

        <div id="Stairlift-fields" class="equipments-details hidden">
          <div class="input-group"><label>Brand:</label><input type="text" id="equip-brand"/></div>
          <div class="input-group"><label>Model Name:</label><input type="text" id="equip-modelname"/></div>
          <div class="input-group"><label>Capacity (kg):</label><input type="text" id="equip-capacitykg"/></div>
          <div class="input-group"><label>Capacity (persons):</label><input type="text" id="equip-capacityper"/></div>
          <div class="input-group"><label>Speed (m/m):</label><input type="text" id="equip-speed"/></div>
          <div class="input-group"><label>Rise (m):</label><input type="text" id="equip-rise"/></div>
          <div class="input-group"><label>Machine Type:</label><input type="text" id="equip-machinetype"/></div>
          <div class="input-group"><label>Motor Data:</label><input type="text" id="equip-motordata"/></div>
          <div class="input-group"><label>Controller:</label><input type="text" id="equip-controller"/></div>
          <div class="input-group"><label>Software Version:</label><input type="text" id="equip-softver"/></div>
          <div class="input-group"><label>Operation:</label><input type="text" id="equip-operation"/></div>
          <div class="input-group"><label>Roping:</label><input type="text" id="equip-roping"/></div>
          <div class="input-group"><label>Rope Diameter:</label><input type="text" id="equip-ropediameter"/></div>
          <div class="input-group"><label>Rope Construction / Made:</label><input type="text" id="equip-ropeconstruction"/></div>
        </div>

        <div id="HomeLift-fields" class="equipments-details hidden">
          <div class="input-group"><label>Brand:</label><input type="text" id="equip-brand"/></div>
          <div class="input-group"><label>Model Name:</label><input type="text" id="equip-modelname"/></div>
          <div class="input-group"><label>Capacity (kg):</label><input type="text" id="equip-capacitykg"/></div>
          <div class="input-group"><label>Capacity (persons):</label><input type="text" id="equip-capacityper"/></div>
          <div class="input-group"><label>Speed (m/m):</label><input type="text" id="equip-speed"/></div>
          <div class="input-group"><label>Rise (m):</label><input type="text" id="equip-rise"/></div>
          <div class="input-group"><label>Stops / Openings:</label><input type="text" id="equip-so"/></div>
          <div class="input-group"><label>Machine Type:</label><input type="text" id="equip-machinetype"/></div>
          <div class="input-group"><label>Motor Data:</label><input type="text" id="equip-motordata/"></div>
          <div class="input-group"><label>Controller:</label><input type="text" id="equip-controller"/></div>
          <div class="input-group"><label>Software Version:</label><input type="text" id="equip-softver"/></div>
          <div class="input-group"><label>Operation:</label><input type="text" id="equip-operation"/></div>
          <div class="input-group"><label>Roping:</label><input type="text" id="equip-roping"/></div>
          <div class="input-group"><label>Rope Diameter:</label><input type="text" id="equip-ropediameter"/></div>
          <div class="input-group"><label>Rope Construction / Made:</label><input type="text" id="equip-ropeconstruction"/></div>
        </div>
        <button onclick="saveEquipments()">Save Equipmennts</button>
        </div>
      </div>
      <div class="card">
        <h3>Equipments List</h3>
        <input type="text" id="search-equipments" placeholder="Search equipments..." oninput="filterTable('equipments-list', this.value)">
        <div class="table-wrapper">
        <table id="equipment-list" class="data-table">
          <thead>
            <tr>
              <th>Lift Number</th>
              <th>Registration Number</th>
              <th>Expiry Date</th>
              <th>Serial Number</th>
              <th>Monthly Rate</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>

    <div id="maintenance-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('maintenance-form', this)"><span>Schedule Maintenance</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="maintenance-form">
        <div class="input-group"><input id="maintenance-date" placeholder="Date"></div>
        <div class="input-group"><input id="maintenance-freq" placeholder="Frequency"></div>
        <div class="input-group"><input id="maintenance-site" placeholder="Site"></div>
        <div class="input-group"><input id="maintenance-pma" placeholder="PMA No."></div>
        <div class="input-group"><input id="maintenance-equipno" placeholder="Equipment No."></div>
        <div class="input-group"><input id="maintenance-team" placeholder="Maintenance Team"></div>
        <button onclick="saveMaintenance()">Save Maintenance</button>
        </div>
      </div>
      <div class="card">
        <h3>Maintenance List</h3>
        <input type="text" id="search-maintenance" placeholder="Search maintenance..." oninput="filterTable('maintenance-list', this.value)">
        <div class="table-wrapper">
        <table id="maintenance-list" class="data-table">
          <thead>
            <tr>
              <th>Date</th><th>Frequency</th><th>Site</th><th>PMA No.</th><th>Equipment No.</th><th>Maintenance Team</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>   
        </div>     
      </div>
    </div>

    <div id="newinspec-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('newinspec-form', this)"><span>Add New Installation Inspection</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="newinspec-form">
        <div class="input-group"><input id="newinspec-date" placeholder="Date"></div>
        <div class="input-group"><input id="newinspec-site" placeholder="Site"></div>
        <div class="input-group"><input id="newinspec-pma" placeholder="PMA No."></div>
        <div class="input-group"><input id="newinspec-equipno" placeholder="Equipment No."></div>
        <div class="input-group"><input id="newinspec-comment" placeholder="Comment"></div>
        <div class="input-group">
          <label for="newinspec-image"></label>
          <input type="file" id="newinspec-image" accept="image/*" multiple>
        </div>
        <button onclick="saveNewinpec()">Save</button>
        </div>
      </div>
      <div class="card">
        <h3>New Installation Inspection List</h3>
        <input type="text" id="search-newinspec" placeholder="Search..." oninput="filterTable('newinspec-list', this.value)">
        <div class="table-wrapper">
        <table id="newinspec-list" class="data-table">
          <thead>
            <tr>
              <th>Date</th><th>Site</th><th>PMA No.</th><th>Equipment No.</th><th>Comment</th><th>image</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>
    <div id="image-modal" class="image-modal" onclick="closeModal()">
      <img id="modal-img" src="" alt="Zoomed Image">
    </div>
    
    <div id="renewinspec-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('renewinspec-form', this)"><span>Add New Installation Inspection</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="renewinspec-form">
        <div class="input-group"><input id="renewinspec-date" placeholder="Date"></div>
        <div class="input-group"><input id="renewinspec-site" placeholder="Site"></div>
        <div class="input-group"><input id="renewinspec-pma" placeholder="PMA No."></div>
        <div class="input-group"><input id="renewinspec-equipno" placeholder="Equipment No."></div>
        <div class="input-group"><input id="renewinspec-comment" placeholder="Comment"></div>
        <div class="input-group">
          <label for="renewinspec-image"></label>
          <input type="file" id="renewinspec-image" accept="image/*" multiple>
        </div>
        <button onclick="saveRenewinspec()">Save</button>
        </div>
      </div>
      <div class="card">
        <h3>Renewal Inspection List</h3>
        <input type="text" id="search-renewinspec" placeholder="Search..." oninput="filterTable('renewinspec-list', this.value)">
        <div class="table-wrapper">
        <table id="renewinspec-list" class="data-table">
          <thead>
            <tr>
              <th>Date</th><th>Site</th><th>PMA No.</th><th>Equipment No.</th><th>Comment</th><th>image</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>
    <div id="image-modal" class="image-modal" onclick="closeModal()">
      <img id="modal-img" src="" alt="Zoomed Image">
    </div>

    <div id="quaterinspec-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('quaterinspec-form', this)"><span>Add New Installation Inspection</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="quaterinspec-form">
        <div class="input-group"><input id="quaterinspec-date" placeholder="Date"></div>
        <div class="input-group"><input id="quaterinspec-site" placeholder="Site"></div>
        <div class="input-group"><input id="quaterinspec-pma" placeholder="PMA No."></div>
        <div class="input-group"><input id="quaterinspec-equipno" placeholder="Equipment No."></div>
        <div class="input-group"><input id="quaterinspec-comment" placeholder="Comment"></div>
        <div class="input-group">
          <label for="quaterinspec-image"></label>
          <input type="file" id="quaterinspec-image" accept="image/*" multiple>
        </div>
        <button onclick="saveQuaterinspec()">Save</button>
        </div>
      </div>
      <div class="card">
        <h3>Quaterly Inspection List</h3>
        <input type="text" id="search-quaterinspec" placeholder="Search..." oninput="filterTable('quaterinspec-list', this.value)">
        <div class="table-wrapper">
        <table id="quaterinspec-list" class="data-table">
          <thead>
            <tr>
              <th>Date</th><th>Site</th><th>PMA No.</th><th>Equipment No.</th><th>Comment</th><th>image</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>
    <div id="image-modal" class="image-modal" onclick="closeModal()">
      <img id="modal-img" src="" alt="Zoomed Image">
    </div>

    <div id="safetyaudit-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('safetyaudit-form', this)"><span>Add New Installation Inspection</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="safetyaudit-form">
        <div class="input-group"><input id="safetyaudit-date" placeholder="Date"></div>
        <div class="input-group"><input id="safetyaudit-site" placeholder="Site"></div>
        <div class="input-group"><input id="safetyaudit-pma" placeholder="PMA No."></div>
        <div class="input-group"><input id="safetyaudit-equipno" placeholder="Equipment No."></div>
        <div class="input-group"><input id="safetyaudit-comment" placeholder="Comment"></div>
        <div class="input-group">
          <label for="safetyaudit-image"></label>
          <input type="file" id="safetyaudit-image" accept="image/*" multiple>
        </div>
        <button onclick="saveSafetyaudit()">Save</button>
        </div>
      </div>
      <div class="card">
        <h3>Safety Audit List</h3>
        <input type="text" id="search-safetyaudit" placeholder="Search..." oninput="filterTable('safetyaudit-list', this.value)">
        <div class="table-wrapper">
        <table id="safetyaudit-list" class="data-table">
          <thead>
            <tr>
              <th>Date</th><th>Site</th><th>PMA No.</th><th>Equipment No.</th><th>Comment</th><th>image</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>
    <div id="image-modal" class="image-modal" onclick="closeModal()">
      <img id="modal-img" src="" alt="Zoomed Image">
    </div>

    <div id="quataudit-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('quataudit-form', this)"><span>Add New Installation Inspection</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="quataudit-form">
        <div class="input-group"><input id="quataudit-date" placeholder="Date"></div>
        <div class="input-group"><input id="quataudit-site" placeholder="Site"></div>
        <div class="input-group"><input id="quataudit-pma" placeholder="PMA No."></div>
        <div class="input-group"><input id="quataudit-equipno" placeholder="Equipment No."></div>
        <div class="input-group"><input id="quataudit-comment" placeholder="Comment"></div>
        <div class="input-group">
          <label for="quataudit-image"></label>
          <input type="file" id="newinspec-image" accept="image/*" multiple>
        </div>
        <button onclick="saveQuataudit()">Save</button>
        </div>
      </div>
      <div class="card">
        <h3>Quality List</h3>
        <input type="text" id="search-quataudit" placeholder="Search..." oninput="filterTable('quataudit-list', this.value)">
        <div class="table-wrapper">
        <table id="quataudit-list" class="data-table">
          <thead>
            <tr>
              <th>Date</th><th>Site</th><th>PMA No.</th><th>Equipment No.</th><th>Comment</th><th>image</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>
    <div id="image-modal" class="image-modal" onclick="closeModal()">
      <img id="modal-img" src="" alt="Zoomed Image">
    </div>

    <div id="service-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('service-form', this)"><span>Add Service </span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="service-form">
        <div class="input-group"><input id="service-date" placeholder="Date"></div>
        <div class="input-group"><input id="service-sonum" placeholder="S.O. Number"></div>
        <div class="input-group"><input id="service-site" placeholder="Site"></div>
        <div class="input-group"><input id="service-pma" placeholder="PMA No."></div>
        <div class="input-group"><input id="service-equipno" placeholder="Equipments No"></div>
        <div class="input-group"><input id="service-packagetype" placeholder="Package Type"></div>
        <div class="input-group"><input id="service-type" placeholder="Service Type"></div>
        <div class="input-group"><input id="service-descrip" placeholder="Description"></div>
        <div class="input-group"><input id="service-qty" placeholder="Quantity"></div>
        <div class="input-group"><input id="service-suffix" placeholder="Suffix"></div>
        <div class="input-group"><input id="service-equipstatus" placeholder="Equipments Status"></div>
        <button onclick="saveService()">Save Service</button>
        </div>
      </div>
      <div class="card">
        <h3>Service List</h3>
        <input type="text" id="search-service" placeholder="Search service..." oninput="filterTable('service-list', this.value)">
        <div class="table-wrapper">
        <table id="service-list" class="data-table">
          <thead>
            <tr>
              <th>Date</th><th>S.O. Number</th><th>Site</th><th>PMA No.</th><th>Equipments No</th><th>Package Type</th><th>Service Type</th><th>Description</th><th>Quantity</th><th>Suffix</th><th>Equipments Status</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table> 
        </div>       
      </div>
    </div>

    <div id="mnc-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('mnc-form', this)"><span>Add Callback </span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="mnc-form">
        <div class="input-group"><input id="mnc-time" placeholder="Time Reported"></div>
        <div class="input-group"><input id="mnc-site" placeholder="Site"></div>
        <div class="input-group"><input id="mnc-pma" placeholder="PMA No."></div>
        <div class="input-group"><input id="mnc-equipno" placeholder="Equipment No."></div>
        <div class="input-group"><input id="mnc-type" placeholder="Callback Type"></div>
        <div class="input-group"><input id="mnc-equipstatus" placeholder="Equipment Status"></div>
        <button onclick="saveMNC()">Save Callback</button>
        </div>
      </div>
      <div class="card">
        <h3>Callback List</h3>
        <input type="text" id="search-mnc" placeholder="Search Callback..." oninput="filterTable('mnc-list', this.value)">
        <div class="table-wrapper">
        <table id="mnc-list" class="data-table">
          <thead>
            <tr>
              <th>Time Reported</th><th>Site</th><th>PMA No.</th><th>Equipment No.</th><th>Callback Type</th><th>Equipment Status</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        </div>        
      </div>
    </div>
  
    <div id="repair-tab" class="tab hidden">
      <div class="card">
        <h2 class="form-header" onclick="toggleForm('repair-form', this)"><span>Repair List</span><span class="arrow-icon">▼</span></h2>
        <div class="hidden" id="repair-form">
        <div class="table-wrapper">
          <table class="data-table" id="repair-list">
            <thead>
              <tr>
                <th>Date</th><th>Site</th><th>PMA</th><th>Equip No</th><th>Remarks</th><th>Photos</th>
              </tr>
            </thead>
            <tbody></tbody>
          </table>
        </div>
      </div>
    </div>
  </div>

  <script>
    document.addEventListener("DOMContentLoaded", function () {
      const saveBtn = document.getElementById("save-equipment");
      if (saveBtn) {
        saveBtn.addEventListener("click", saveEquipments);
      }
    });

    function showTab(tab) {
      const tabs = document.querySelectorAll('.tab');
      tabs.forEach(t => t.classList.add('hidden'));
      const selected = document.getElementById(`${tab}-tab`);
      if (selected) selected.classList.remove('hidden');
    }

    function toggleForm(formId, header) {
      console.log("Toggling form:", formId);
      const form = document.getElementById(formId);
      const arrow = header.querySelector('.arrow-icon');
      if (form) {
        const isHidden = form.classList.toggle('hidden');
        if (arrow) {
          arrow.classList.toggle('arrow-rotate', !isHidden);
        }
      }
    }
    
    function filterTable(tableId, query) {
      const table = document.getElementById(tableId);
      const rows = table.querySelectorAll("tbody tr");
      const lowerQuery = query.toLowerCase();
    
      rows.forEach(row => {
        const text = row.textContent.toLowerCase();
        row.style.display = text.includes(lowerQuery) ? "" : "none";
      });
    }

    function saveInstallation() {
      const contractno = document.getElementById('installation-contractno').value;
      const date = document.getElementById('installation-date')?.value || ""; // fallback if missing
      const type = document.getElementById('installation-type').value;
      const client = document.getElementById('installation-client').value;
      const company = document.getElementById('installation-company').value;
      const address = document.getElementById('installation-address').value;
      const postcode = document.getElementById('installation-postcode').value;
      const phonenumber = document.getElementById('installation-phonenumber').value;
      const email = document.getElementById('installation-email').value;
      const picname = document.getElementById('installation-picname').value;
      const picphonenumber = document.getElementById('installation-picphonenumber').value;
      const picemail = document.getElementById('installation-picemail').value;
      let bond = '';
        if (document.getElementById('installation-bond-bank').checked) {
          bond = 'Bank Guarantee';
        } else if (document.getElementById('installation-bond-director').checked) {
          bond = 'Director Guarantee';
        }
      let insuranceType = '';
      let insuranceProvider = '';
        if (document.getElementById('installation-car').checked) {
          insuranceType = 'CAR';
        } else if (document.getElementById('installation-ear').checked) {
        insuranceType = 'EAR';
        } else if (document.getElementById('installation-public').checked) {
        insuranceType = 'Public Liability';
        } else if (document.getElementById('installation-workman').checked) {
        insuranceType = 'Workman Compensation';
        }
        if (insuranceType !== 'Workman Compensation') {
          if (document.getElementById('installation-main').checked) {
            insuranceProvider = 'Main Contractor';
          } else if (document.getElementById('installation-trident').checked) {
            insuranceProvider = 'Trident';
          }
        }
      const ladAmount = document.getElementById('installation-lad-amount').value;
      const ladLimit = document.getElementById('installation-lad-limit').value;
      const dlpDuration = document.getElementById('installation-dlp-duration').value;
      const dlpOthers = document.getElementById('installation-dlp-other').value;
      const equipSummary = document.getElementById('installation-equipsummary').value;
      const equipOthers = document.getElementById('installation-equipothers').value;
      const commencementdate = document.getElementById('installation-commencementdate').value;
      const completiondate = document.getElementById('installation-completiondate').value;
      const pricesummary = document.getElementById('installation-pricesummary').value;
      const downpayment = document.getElementById('installation-downpayment').value;
      const retention = document.getElementById('installation-retention').value;
      const vo = document.getElementById('installation-vo').value;
      const tableBody = document.querySelector('#installation-list tbody');
      const row = document.createElement('tr');
      row.innerHTML = `
        <td>${contractno}</td>
        <td>${date}</td>
        <td>${type}</td>
        <td>${client}</td>
        <td>${company}</td>
        <td>${address}</td>
        <td>${postcode}</td>
        <td>${phonenumber}</td>
        <td>${email}</td>
        <td>${picname}</td>
        <td>${picphonenumber}</td>
        <td>${picemail}</td>
        <td>${bond}</td>
        <td>${insuranceType}</td>
        <td>${insuranceProvider}</td>
        <td>${ladAmount}</td>
        <td>${ladLimit}</td>
        <td>${dlpDuration}</td>
        <td>${dlpOthers}</td>
        <td>${equipSummary}</td>
        <td>${equipOthers}</td>
        <td>${commencementdate}</td>
        <td>${completiondate}</td>
        <td>${pricesummary}</td>
        <td>${downpayment}</td>
        <td>${retention}</td>
        <td>${vo}</td>`;
      tableBody.appendChild(row);
    }

    document.querySelectorAll('input[name="installation-instype"]').forEach(input => {
      input.addEventListener('change', () => {
        const showProviders = ['installation-car', 'installation-ear', 'installation-public'].includes(input.id);
        document.getElementById('installation-provider-group').style.display = showProviders ? 'block' : 'none';
      });
    });

    function saveModernization() {
      const contractno = document.getElementById('modernization-contractno').value;
      const date = document.getElementById('modernization-date')?.value || ""; // fallback if missing
      const type = document.getElementById('modernization-type').value;
      const client = document.getElementById('modernization-client').value;
      const company = document.getElementById('modernization-company').value;
      const address = document.getElementById('modernization-address').value;
      const postcode = document.getElementById('modernization-postcode').value;
      const phonenumber = document.getElementById('modernization-phonenumber').value;
      const email = document.getElementById('modernization-email').value;
      const picname = document.getElementById('modernization-picname').value;
      const picphonenumber = document.getElementById('modernization-picphonenumber').value;
      const picemail = document.getElementById('modernization-picemail').value;
      let bond = '';
        if (document.getElementById('modernization-bond-bank').checked) {
          bond = 'Bank Guarantee';
        } else if (document.getElementById('modernization-bond-director').checked) {
          bond = 'Director Guarantee';
        }
      let insuranceType = '';
      let insuranceProvider = '';
        if (document.getElementById('modernization-car').checked) {
          insuranceType = 'CAR';
        } else if (document.getElementById('modernization-ear').checked) {
        insuranceType = 'EAR';
        } else if (document.getElementById('modernization-public').checked) {
        insuranceType = 'Public Liability';
        } else if (document.getElementById('modernization-workman').checked) {
        insuranceType = 'Workman Compensation';
        }
        if (insuranceType !== 'Workman Compensation') {
          if (document.getElementById('modernization-main').checked) {
            insuranceProvider = 'Main Contractor';
          } else if (document.getElementById('modernization-trident').checked) {
            insuranceProvider = 'Trident';
          }
        }
      const ladAmount = document.getElementById('modernization-lad-amount').value;
      const ladLimit = document.getElementById('modernization-lad-limit').value;
      const dlpDuration = document.getElementById('modernization-dlp-duration').value;
      const dlpOthers = document.getElementById('modernization-dlp-other').value;
      const equipSummary = document.getElementById('modernization-equipsummary').value;
      const equipOthers = document.getElementById('modernization-equipothers').value;
      const commencementdate = document.getElementById('modernization-commencementdate').value;
      const completiondate = document.getElementById('modernization-completiondate').value;
      const pricesummary = document.getElementById('modernization-pricesummary').value;
      const downpayment = document.getElementById('modernization-downpayment').value;
      const retention = document.getElementById('modernization-retention').value;
      const vo = document.getElementById('modernization-vo').value;
      const tableBody = document.querySelector('#modernization-list tbody');
      const row = document.createElement('tr');
      row.innerHTML = `
        <td>${contractno}</td>
        <td>${date}</td>
        <td>${type}</td>
        <td>${client}</td>
        <td>${company}</td>
        <td>${address}</td>
        <td>${postcode}</td>
        <td>${phonenumber}</td>
        <td>${email}</td>
        <td>${picname}</td>
        <td>${picphonenumber}</td>
        <td>${picemail}</td>
        <td>${bond}</td>
        <td>${insuranceType}</td>
        <td>${insuranceProvider}</td>
        <td>${ladAmount}</td>
        <td>${ladLimit}</td>
        <td>${dlpDuration}</td>
        <td>${dlpOthers}</td>
        <td>${equipSummary}</td>
        <td>${equipOthers}</td>
        <td>${commencementdate}</td>
        <td>${completiondate}</td>
        <td>${pricesummary}</td>
        <td>${downpayment}</td>
        <td>${retention}</td>
        <td>${vo}</td>`;
      tableBody.appendChild(row);
    }

    document.querySelectorAll('input[name="modernization-instype"]').forEach(input => {
      input.addEventListener('change', () => {
        const showProviders = ['modernization-car', 'modernization-ear', 'modernization-public'].includes(input.id);
        document.getElementById('modernization-provider-group').style.display = showProviders ? 'block' : 'none';
      });
    });
    
    function saveContract() {
      const no = document.getElementById('contracts-no').value;
      const date = document.getElementById('contracts-date').value;
      const expiry = document.getElementById('contracts-expiry').value;
      const type = document.getElementById('contracts-type').value;
      const included = document.getElementById('contracts-included').value;
      const excluded = document.getElementById('contracts-excluded').value;
      const price = document.getElementById('contracts-price').value;
      
      const tableBody = document.querySelector('#contracts-list tbody');
      const row = document.createElement('tr');
      row.innerHTML = `
      <td>${no}</td><td>${date}</td><td>${expiry}</td><td>${type}</td><td>${included}</td><td>${excluded}</td><td>${price}</td>`;
      tableBody.appendChild(row);
    }

    function saveClient() {
      const clientsname = document.getElementById('clients-name').value;
      const clientsrole = document.getElementById('clients-type').value;
      const clientsaddress = document.getElementById('clients-address').value;
      const clientspostcode = document.getElementById('clients-postcode').value;
      const clientsphonenumber = document.getElementById('clients-phonenumber').value;
      const clientsemail = document.getElementById('clients-email').value;
      const clientspicname = document.getElementById('clients-pic-name').value;
      const clientspicphonenumber = document.getElementById('clients-pic-phonenumber').value;
      const clientspicemail = document.getElementById('clients-pic-email').value;
      const billingInputs = document.querySelectorAll('#clients-billing-fields input');
      const clientsbillingAddress = billingInputs[0].value;
      const clientsbillingPostcode = billingInputs[1].value;
      const clientsbillingTel = billingInputs[2].value;
      const clientsbillingEmail = billingInputs[3].value;
      const ownerInputs = document.querySelectorAll('#clients-owner-fields input');
      const clientsownerAddress = ownerInputs[0].value;
      const clientsownerPostcode = ownerInputs[1].value;
      const clientsownerTel = ownerInputs[2].value;
      const clientsownerEmail = ownerInputs[3].value;
      const pricing = ""; 
      const tableBody = document.querySelector('#clients-list tbody');
      const row = document.createElement('tr');
      row.innerHTML = `
        <td>${clientsname}</td>
        <td>${clientsrole}</td>
        <td>${clientsaddress}</td>
        <td>${clientspostcode}</td>
        <td>${clientsphonenumber}</td>
        <td>${clientsemail}</td>
        <td>${clientspicname}</td>
        <td>${clientspicphonenumber}</td>
        <td>${clientspicemail}</td>
        <td>${clientsbillingAddress}</td>
        <td>${clientsbillingPostcode}</td>
        <td>${clientsbillingTel}</td>
        <td>${clientsbillingEmail}</td>
        <td>${clientsownerAddress}</td>
        <td>${clientsownerPostcode}</td>
        <td>${clientsownerTel}</td>
        <td>${clientsownerEmail}</td>
        <td>${pricing}</td>`;
      tableBody.appendChild(row);
    }

    function toggleClientsBillingAddress() {
      const checkbox = document.getElementById("clients-billing-same");
      const section = document.getElementById("clients-billing-fields");
      const customerAddress = document.getElementById("clients-address").value;
      const customerPostcode = document.getElementById("clients-postcode").value;
      const customerPhone = document.getElementById("clients-phonenumber").value;
      const customerEmail = document.getElementById("clients-email").value;
      const inputs = section.querySelectorAll("input");
      if (checkbox.checked) {
        inputs[0].value = customerAddress;
        inputs[1].value = customerPostcode;
        inputs[2].value = customerPhone;
        inputs[3].value = customerEmail;
        section.style.display = "none";
      } else {
        section.style.display = "block";
        inputs.forEach(input => input.value = "");
      }
    }

    function toggleClientsOwnerAddress() {
      const checkbox = document.getElementById("clients-owner-same");
      const section = document.getElementById("clients-owner-fields");
      const customerAddress = document.getElementById("clients-address").value;
      const customerPostcode = document.getElementById("clients-postcode").value;
      const customerPhone = document.getElementById("clients-phonenumber").value;
      const customerEmail = document.getElementById("clients-email").value;
      const inputs = section.querySelectorAll("input");
      if (checkbox.checked) {
        inputs[0].value = customerAddress;
        inputs[1].value = customerPostcode;
        inputs[2].value = customerPhone;
        inputs[3].value = customerEmail;
        section.style.display = "none";
      } else {
        section.style.display = "block";
        inputs.forEach(input => input.value = "");
      }
    }

    function saveSites() {
      const name = document.getElementById('site-name').value;
      const type = document.getElementById('site-type').value;
      const address = document.getElementById('site-address').value;
      const latitude = document.getElementById('site-latitude').value;
      const longtitude = document.getElementById('site-longtitude').value;

      const tableBody = document.querySelector('#sites-list tbody');
      const row = document.createElement('tr');
      row.innerHTML = `
      <td>${name}</td><td>${type}</td><td>${address}</td><td>${latitude}</td><td>${longtitude}</td>`;
      tableBody.appendChild(row);
    }

    function savePricingRow() {
      const table = document.querySelector("#pricing-table tbody");
      const row = document.createElement("tr");
      row.innerHTML = `
        <td><input type="text" placeholder="Unit No."></td>
        <td><input type="text" placeholder="PMA No."></td>
        <td><input type="number" value="0" step="0.01" onchange="calculateRow(this)"></td>
        <td style="text-align:center;">
          <input type="checkbox" onchange="calculateRow(this)">
        </td>
        <td class="row-total">0.00</td>
        <td><button onclick="this.parentElement.parentElement.remove(); updateGrandTotal();">🗑</button></td>
      `;
      table.appendChild(row);
      calculateRow(row.querySelector("input[type='number']")); // auto-calc new row
    }

    function calculateRow(input) {
      const row = input.closest("tr");
      const price = parseFloat(row.cells[2].querySelector("input").value) || 0;
      const includeSST = row.cells[3].querySelector("input").checked;
      const total = includeSST ? price * 1.08 : price;

      row.querySelector(".row-total").textContent = total.toFixed(2);
      updateGrandTotal();
      syncPricingToContracts();
    }

    function syncPricingToContracts() {
      const pricingRows = document.querySelectorAll("th");
      const pricingMap = {};

      pricingRows.forEach(row => {
        const pma = row.cells[1].querySelector("input").value.trim();
        const total = row.querySelector(".row-total").textContent.trim();
        if (pma) pricingMap[pma] = total;
      });

      const contractRows = document.querySelectorAll("#contracts-list tbody tr");
      contractRows.forEach(row => {
        const pmaCell = row.cells[8]; // adjust index to match PMA No. column
        const priceCell = row.cells[row.cells.length - 1]; // assuming last col = Monthly Price
        const pma = pmaCell?.textContent?.trim();
        if (pricingMap[pma]) {
          priceCell.textContent = pricingMap[pma];
        } else {
          priceCell.textContent = "–";
        }
      });
    }

    function saveEquipments() {
      const liftnumber = document.getElementById('equip-liftnumber').value;
      const oname = document.getElementById('equip-owner-name').value;
      const oworkplacenumber = document.getElementById('equip-owner-workplacenumber').value;
      const ocorrespondencesadd = document.getElementById('equip-owner-correspondencesadd').value;
      const rname = document.getElementById('equip-resident-name').value;
      const rworkplacenumber = document.getElementById('equip-resident-workplacenumber').value;
      const rcorrespondencesadd = document.getElementById('equip-resident-correspondencesadd').value;
      const lastinspec = document.getElementById('equip-lastinspec').value;
      const resnumber = document.getElementById('equip-resnumber').value;
      const expired = document.getElementById('equip-expired').value;
      const location = document.getElementById('equip-location').value;
      const serialnumber = document.getElementById('equip-serialnumber').value;
      const manufacture = document.getElementById('equip-manufacture').value;
      const rate = document.getElementById('equip-rate').value;
      const type = document.getElementById('equip-type').value;
      const brand = document.getElementById('equip-brand')?.value || '';
      const modelname = document.getElementById('equip-modelname')?.value || '';
      const capacitykg = document.getElementById('equip-capacitykg')?.value || '';
      const capacityper = document.getElementById('equip-capacityper')?.value || '';
      const speed = document.getElementById('equip-speed')?.value || '';
      const rise = document.getElementById('equip-rise')?.value || '';
      const stepwidth = document.getElementById('equip-stepwidth')?.value || '';
      const inclination = document.getElementById('equip-inclination')?.value || '';
      const so = document.getElementById('equip-so')?.value || '';
      const machinetype = document.getElementById('equip-machinetype')?.value || '';
      const motordata = document.getElementById('equip-motordata')?.value || '';
      const controller = document.getElementById('equip-controller')?.value || '';
      const softver = document.getElementById('equip-softver')?.value || '';
      const operation = document.getElementById('equip-operation')?.value || '';
      const roping = document.getElementById('equip-roping')?.value || '';
      const ropediameter = document.getElementById('equip-ropediameter')?.value || '';
      const ropeconstruction = document.getElementById('equip-ropeconstruction')?.value || '';
      const tableBody = document.querySelector('#equipment-list tbody');
      const row = document.createElement('tr');
      row.innerHTML = `
        <td>${liftnumber}</td>
        <td>${resnumber}</td>
        <td>${expired}</td>
        <td>${serialnumber}</td>
        <td>${rate}</td>`;
      tableBody.appendChild(row);
    }

    function toggleEquipmentFields(type) {
      const allSections = document.querySelectorAll('.equipment-details');
      allSections.forEach(section => section.classList.add('hidden'));
      if (type) {
        const section = document.getElementById(`${type}-fields`);
        if (section) section.classList.remove('hidden');
      }
    }

    function saveMaintenance() {
      const date = document.getElementById('maintenance-date').value;
      const freq = document.getElementById('maintenance-freq').value;
      const site = document.getElementById('maintenance-site').value;
      const pma = document.getElementById('maintenance-pma').value;
      const equipno = document.getElementById('maintenance-equipno').value;
      const team = document.getElementById('maintenance-team').value;
 
      const tableBody = document.querySelector('#maintenance-list tbody');
      const row = document.createElement('tr');
      row.innerHTML = `
      <td>${date}</td><td>${freq}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${team}</td>`;
      tableBody.appendChild(row);
    }

    function saveNewinpec() {
      const date = document.getElementById('newinspec-date').value;
      const site = document.getElementById('newinspec-site').value;
      const pma = document.getElementById('newinspec-pma').value;
      const equipno = document.getElementById('newinspec-equipno').value;
      const comment = document.getElementById('newinspec-comment').value;
      const files = Array.from(document.getElementById('newinspec-image').files);
      const tableBody = document.querySelector('#newinspec-list tbody');
      const row = document.createElement('tr');

      if (files.length === 0) {
        row.innerHTML = `
          <td>${date}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${comment}</td><td>No image</td>`;
        tableBody.appendChild(row);
        return;
      }

      Promise.all(files.map(file => {
        return new Promise(resolve => {
          const reader = new FileReader();
          reader.onload = e => {
            const imgTag = `<img src="${e.target.result}" alt="Photo" onclick="zoomImage(this)">`;
            resolve(imgTag);
          };
          reader.readAsDataURL(file);
        });
      })).then(images => {
        row.innerHTML = `
          <td>${date}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${comment}</td><td>${images.join(' ')}</td>`;
        tableBody.appendChild(row);

      if (comment.trim() !== '') {
        const repairTable = document.querySelector('#repair-list tbody');
        const repairRow = document.createElement('tr');
        repairRow.innerHTML = `
          <td>${date}</td>
          <td>${site}</td>
          <td>${pma}</td>
          <td>${equipno}</td>
          <td>${comment}</td>
          <td>${images.join(' ')}</td>`;
        repairTable.appendChild(repairRow);
      }
      });
    }

    function saveRenewinspec() {
      const date = document.getElementById('renewinspec-date').value;
      const site = document.getElementById('renewinspec-site').value;
      const pma = document.getElementById('renewinspec-pma').value;
      const equipno = document.getElementById('renewinspec-equipno').value;
      const comment = document.getElementById('renewinspec-comment').value;
      const files = Array.from(document.getElementById('renewinspec-image').files);
      const tableBody = document.querySelector('#renewinspec-list tbody');
      const row = document.createElement('tr');

      if (files.length === 0) {
        row.innerHTML = `
          <td>${date}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${comment}</td><td>No image</td>`;
        tableBody.appendChild(row);
        return;
      }

      Promise.all(files.map(file => {
        return new Promise(resolve => {
          const reader = new FileReader();
          reader.onload = e => {
            const imgTag = `<img src="${e.target.result}" alt="Photo" onclick="zoomImage(this)">`;
            resolve(imgTag);
          };
          reader.readAsDataURL(file);
        });
      })).then(images => {
        row.innerHTML = `
          <td>${date}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${comment}</td><td>${images.join(' ')}</td>`;
        tableBody.appendChild(row);

      if (comment.trim() !== '') {
        const repairTable = document.querySelector('#repair-list tbody');
        const repairRow = document.createElement('tr');
        repairRow.innerHTML = `
          <td>${date}</td>
          <td>${site}</td>
          <td>${pma}</td>
          <td>${equipno}</td>
          <td>${comment}</td>
          <td>${images.join(' ')}</td>`;
        repairTable.appendChild(repairRow);
      }
      });
    }

    function saveQuaterinspec() {
      const date = document.getElementById('quaterinspec-date').value;
      const site = document.getElementById('quaterinspec-site').value;
      const pma = document.getElementById('quaterinspec-pma').value;
      const equipno = document.getElementById('quaterinspec-equipno').value;
      const comment = document.getElementById('quaterinspec-comment').value;
      const files = Array.from(document.getElementById('quaterinspec-image').files);

      const tableBody = document.querySelector('#quaterinspec-list tbody');
      const row = document.createElement('tr');

      if (files.length === 0) {
        row.innerHTML = `
          <td>${date}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${comment}</td><td>No image</td>`;
        tableBody.appendChild(row);
        return;
      }

      Promise.all(files.map(file => {
        return new Promise(resolve => {
          const reader = new FileReader();
          reader.onload = e => {
            const imgTag = `<img src="${e.target.result}" alt="Photo" onclick="zoomImage(this)">`;
            resolve(imgTag);
          };
          reader.readAsDataURL(file);
        });
      })).then(images => {
        row.innerHTML = `
          <td>${date}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${comment}</td><td>${images.join(' ')}</td>`;
        tableBody.appendChild(row);

      if (comment.trim() !== '') {
        const repairTable = document.querySelector('#repair-list tbody');
        const repairRow = document.createElement('tr');
        repairRow.innerHTML = `
          <td>${date}</td>
          <td>${site}</td>
          <td>${pma}</td>
          <td>${equipno}</td>
          <td>${comment}</td>
          <td>${images.join(' ')}</td>`;
        repairTable.appendChild(repairRow);
      }
      });
    }

    function saveSafetyaudit() {
      const date = document.getElementById('safetyaudit-date').value;
      const site = document.getElementById('safetyaudit-site').value;
      const pma = document.getElementById('safetyaudit-pma').value;
      const equipno = document.getElementById('safetyaudit-equipno').value;
      const comment = document.getElementById('safetyaudit-comment').value;
      const files = Array.from(document.getElementById('safetyaudit-image').files);

      const tableBody = document.querySelector('#safetyaudit-list tbody');
      const row = document.createElement('tr');

      if (files.length === 0) {
        row.innerHTML = `
          <td>${date}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${comment}</td><td>No image</td>`;
        tableBody.appendChild(row);
        return;
      }

      Promise.all(files.map(file => {
        return new Promise(resolve => {
          const reader = new FileReader();
          reader.onload = e => {
            const imgTag = `<img src="${e.target.result}" alt="Photo" onclick="zoomImage(this)">`;
            resolve(imgTag);
          };
          reader.readAsDataURL(file);
        });
      })).then(images => {
        row.innerHTML = `
          <td>${date}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${comment}</td><td>${images.join(' ')}</td>`;
        tableBody.appendChild(row);

      if (comment.trim() !== '') {
        const repairTable = document.querySelector('#repair-list tbody');
        const repairRow = document.createElement('tr');
        repairRow.innerHTML = `
          <td>${date}</td>
          <td>${type}</td>
          <td>${site}</td>
          <td>${pma}</td>
          <td>${equipno}</td>
          <td>${comment}</td>
          <td>${images.join(' ')}</td>`;
        repairTable.appendChild(repairRow);
      }
      });
    }

    function saveQuataudit() {
      const date = document.getElementById('quataudit-date').value;
      const site = document.getElementById('quataudit-site').value;
      const pma = document.getElementById('quataudit-pma').value;
      const equipno = document.getElementById('quataudit-equipno').value;
      const comment = document.getElementById('quataudit-comment').value;
      const files = Array.from(document.getElementById('quataudit-image').files);

      const tableBody = document.querySelector('#quataudit-list tbody');
      const row = document.createElement('tr');

      if (files.length === 0) {
        row.innerHTML = `
          <td>${date}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${comment}</td><td>No image</td>`;
        tableBody.appendChild(row);
        return;
      }

      Promise.all(files.map(file => {
        return new Promise(resolve => {
          const reader = new FileReader();
          reader.onload = e => {
            const imgTag = `<img src="${e.target.result}" alt="Photo" onclick="zoomImage(this)">`;
            resolve(imgTag);
          };
          reader.readAsDataURL(file);
        });
      })).then(images => {
        row.innerHTML = `
          <td>${date}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${comment}</td><td>${images.join(' ')}</td>`;
        tableBody.appendChild(row);

      if (comment.trim() !== '') {
        const repairTable = document.querySelector('#repair-list tbody');
        const repairRow = document.createElement('tr');
        repairRow.innerHTML = `
          <td>${date}</td>
          <td>${site}</td>
          <td>${pma}</td>
          <td>${equipno}</td>
          <td>${comment}</td>
          <td>${images.join(' ')}</td>`;
        repairTable.appendChild(repairRow);
      }
      });
    }

    function zoomImage(img) {
      const modal = document.getElementById('image-modal');
      const modalImg = document.getElementById('modal-img');
      modalImg.src = img.src;
      modal.style.display = 'flex';
    }

    function closeModal() {
      document.getElementById('image-modal').style.display = 'none';
    }

    function saveService() {
      const date = document.getElementById('service-date').value;
      const sonum = document.getElementById('service-sonum').value;
      const site = document.getElementById('service-site').value;
      const pma = document.getElementById('service-pma').value;
      const equipno = document.getElementById('service-region').value;
      const packagetype = document.getElementById('service-packagetype').value;
      const type = document.getElementById('service-type').value;
      const descrip = document.getElementById('service-descrip').value;
      const qty = document.getElementById('service-qty').value;
      const suffix = document.getElementById('service-suffix').value;
      const equipstatus = document.getElementById('service-equipstatus').value;
 
      const tableBody = document.querySelector('#service-list tbody');
      const row = document.createElement('tr');
      row.innerHTML = `
      <td>${date}</td><td>${sonum}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${packagetype}</td><td>${type}</td><td>${descrip}</td><td>${qty}</td><td>${suffix}</td><td>${equipstatus}</td>`;
      tableBody.appendChild(row);
    }

    function saveMNC() {
      const time = document.getElementById('mnc-time').value;
      const site = document.getElementById('mnc-site').value;
      const pma = document.getElementById('mnc-pma').value;
      const equipno = document.getElementById('mnc-equipno').value;
      const type = document.getElementById('mnc-type').value;
      const equipstatus = document.getElementById('mnc-equipstatus').value;
 
      const tableBody = document.querySelector('#mnc-list tbody');
      const row = document.createElement('tr');
      row.innerHTML = `
      <td>${time}</td><td>${site}</td><td>${pma}</td><td>${equipno}</td><td>${type}</td><td>${equipstatus}</td>`;
      tableBody.appendChild(row);
    }
  </script>
</body>
</html>
