# my-website
bgmi item sales
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BGMI Offers</title>
  <style>
    body{font-family:sans-serif;background:#0f1724;color:#fff;margin:0;padding:0;}
    .container{max-width:1000px;margin:auto;padding:20px;}
    h1{text-align:center;}
    .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px;margin-top:20px;}
    .card{background:#1e293b;padding:15px;border-radius:10px;text-align:center;}
    .card button{padding:10px 15px;background:#4ade80;color:#000;border:none;border-radius:6px;cursor:pointer;margin-top:10px;}
    .modal-back{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.6);display:none;align-items:center;justify-content:center;}
    .modal{background:#0f1724;padding:20px;border-radius:10px;width:90%;max-width:400px;}
    .modal input{width:100%;padding:8px;margin:6px 0;border-radius:6px;border:1px solid #94a3b8;background:transparent;color:#fff;}
    .modal button{margin-top:10px;width:100%;}
  </style>
</head>
<body>
  <div class="container">
    <h1>BGMI Offers</h1>
    <div class="grid">
      <div class="card">
        <h3>X Suit — Ultimate Set</h3>
        <button onclick="openRedeem('X Suit')">Redeem</button>
      </div>
      <div class="card">
        <h3>Latest Outfit — Aurora</h3>
        <button onclick="openRedeem('Aurora Outfit')">Redeem</button>
      </div>
      <div class="card">
        <h3>Upgradeable Gun Skins</h3>
        <button onclick="openRedeem('Gun Skins')">Redeem</button>
      </div>
    </div>
  </div>

  <!-- Redeem Modal -->
  <div class="modal-back" id="modalBack" onclick="closeModal(event)">
    <div class="modal" onclick="event.stopPropagation()">
      <h2 id="modalTitle">Redeem</h2>
      <input id="bgmiId" placeholder="Enter BGMI ID">
      <input id="phone" placeholder="Phone (optional)">
      <input id="email" placeholder="Email (optional)">
      <button onclick="submitRedeem()">Submit</button>
      <button onclick="closeModal()">Cancel</button>
    </div>
  </div>

  <script>
    let currentOffer = '';
    function openRedeem(offer){
      currentOffer = offer;
      document.getElementById('modalTitle').innerText = 'Redeem: ' + offer;
      document.getElementById('modalBack').style.display='flex';
    }
    function closeModal(e){
      if(e && e.target.id !== 'modalBack') return;
      document.getElementById('modalBack').style.display='none';
      document.getElementById('bgmiId').value='';
      document.getElementById('phone').value='';
      document.getElementById('email').value='';
    }
    function submitRedeem(){
      const bgmi = document.getElementById('bgmiId').value.trim();
      const phone = document.getElementById('phone').value.trim();
      const email = document.getElementById('email').value.trim();
      if(!bgmi){alert('BGMI ID daal bhai'); return;}
      const payload = {offer:currentOffer,bgmiId:bgmi,phone:phone,email:email,time:new Date().toISOString()};
      const list = JSON.parse(localStorage.getItem('redeems_demo')||'[]'); list.push(payload); localStorage.setItem('redeems_demo',JSON.stringify(list));
      alert('Request saved (demo). Admin check kar ke redeem kar dega.');
      closeModal();
    }
  </script>
</body>
</html>
