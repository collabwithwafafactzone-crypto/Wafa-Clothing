<!doctype html>
<html lang="hi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Reality Probe Clothing — Shop</title>
  <meta name="description" content="Buy stylish clothes — simple demo store" />
  <style>
    :root{--bg:#071009;--panel:#0b1a12;--accent:#00ff66;--muted:#9fdcb1;--card:#07130d}
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter, system-ui, Arial, sans-serif;background:linear-gradient(180deg,#000,#071009);color:var(--muted)}
    header{padding:20px;text-align:center;border-bottom:1px solid rgba(0,255,102,0.06)}
    .brand{font-size:22px;color:var(--accent);font-weight:700;letter-spacing:1px}
    .tag{color:#88f6b8;font-size:13px}
    .wrap{max-width:1100px;margin:28px auto;padding:0 18px}
    .hero{display:flex;gap:20px;align-items:center;justify-content:space-between}
    .hero .left{max-width:640px}
    h1{color:var(--accent);margin:6px 0;font-size:36px}
    p.lead{color:#9fdcb1;line-height:1.5}
    .btn{display:inline-block;background:var(--accent);color:#00210b;padding:10px 14px;border-radius:8px;text-decoration:none;font-weight:700}

    /* products */
    .grid{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;margin-top:22px}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(0,0,0,0.06));padding:12px;border-radius:10px;border:1px solid rgba(0,255,102,0.04)}
    .img{height:220px;border-radius:8px;background:#07130d;display:flex;align-items:center;justify-content:center;color:#062b1a;font-weight:700}
    .title{margin:10px 0 4px;font-weight:700;color:#dfffe7}
    .price{color:var(--accent);font-weight:800}
    .small{font-size:13px;color:#9fdcb1}
    .flex{display:flex;gap:8px;align-items:center}

    /* cart */
    .cart-btn{position:fixed;right:18px;bottom:18px;background:var(--panel);padding:12px;border-radius:999px;border:1px solid rgba(0,255,102,0.08);cursor:pointer}
    .cart-count{background:var(--accent);color:#00210b;padding:4px 8px;border-radius:12px;margin-left:8px;font-weight:700}
    .cart-panel{position:fixed;right:18px;bottom:80px;width:360px;max-height:70vh;overflow:auto;background:var(--panel);padding:18px;border-radius:12px;border:1px solid rgba(0,255,102,0.06)}
    .cart-item{display:flex;gap:10px;align-items:center;padding:8px 0;border-bottom:1px solid rgba(0,255,102,0.03)}
    .cart-item:last-child{border-bottom:none}
    .qty{display:inline-block;padding:6px 8px;background:#062512;border-radius:6px}

    /* checkout form */
    .checkout{margin-top:12px;background:linear-gradient(180deg,#081712, #07110b);padding:12px;border-radius:8px}
    label{display:block;font-size:13px;color:#bfffd3;margin-top:8px}
    input,textarea,select{width:100%;padding:8px;border-radius:6px;border:1px solid rgba(0,255,102,0.06);background:transparent;color:var(--muted)}

    footer{text-align:center;padding:20px;color:#6fbf99;font-size:13px;margin-top:40px}

    /* responsive */
    @media(max-width:900px){.grid{grid-template-columns:repeat(2,1fr)}.hero{flex-direction:column;align-items:flex-start}.img{height:180px}}
    @media(max-width:560px){.grid{grid-template-columns:1fr}.cart-panel{width:92vw;right:4vw}}
  </style>
</head>
<body>
  <header>
    <div class="brand">Reality Probe Clothing</div>
    <div class="tag">Stylish • Affordable • Fast</div>
  </header>

  <main class="wrap">
    <section class="hero">
      <div class="left">
        <h1>Kapde becho — simple store</h1>
        <p class="lead">Yeh store main tumhare liye customize kar diya hai — products, cart aur demo checkout sab ready. Images ki jagah placeholder use kiye hain; asli product images add karne ke liye unki URLs bhej do ya main unsplash images laga dun (free).</p>
        <a class="btn" id="shop-now">Shop Now</a>
        <div style="margin-top:10px;font-size:13px;color:#9fdcb1">Contact: +91 9XXXXXXXXX • Email: shop@realityprobe.com</div>
      </div>
      <div class="right">
        <div style="width:220px;height:220px;border-radius:12px;background:linear-gradient(135deg,#001a08,#0b2b17);display:flex;align-items:center;justify-content:center;box-shadow:0 8px 30px rgba(0,255,102,0.06)">
          <div style="text-align:center;color:var(--accent)"><div style="font-size:18px;font-weight:800">Reality Probe</div><div style="font-size:12px;color:#9fdcb1">Clothing Store — Demo</div></div>
        </div>
      </div>
    </section>

    <section id="products">
      <div class="grid" id="product-grid">
        <!-- products injected by JS -->
      </div>
    </section>

    <footer>
      © <span id="year"></span> Reality Probe — Demo Store
    </footer>
  </main>

  <!-- cart button -->
  <div class="cart-btn" id="open-cart" title="Open cart">
    🛒 <span class="cart-count" id="cart-count">0</span>
  </div>

  <!-- cart panel (hidden initially) -->
  <div class="cart-panel" id="cart-panel" style="display:none">
    <h3>Your Cart</h3>
    <div id="cart-items"></div>
    <div style="margin-top:10px;font-weight:800">Total: ₹<span id="cart-total">0</span></div>

    <div class="checkout">
      <h4>Checkout</h4>
      <label>Naam</label>
      <input id="c-name" placeholder="Tumhara naam" />
      <label>Phone</label>
      <input id="c-phone" placeholder="+91 9XXXXXXXXX" />
      <label>Address</label>
      <textarea id="c-address" rows="3" placeholder="Delivery address"></textarea>
      <label>Email (optional)</label>
      <input id="c-email" placeholder="example@mail.com" />
      <button class="btn" id="place-order" style="margin-top:10px">Order Place Karo</button>
      <div id="order-msg" style="margin-top:8px;font-size:13px;color:#aef5c9"></div>
    </div>
  </div>

  <script>
    document.getElementById('year').textContent = new Date().getFullYear();

    // === EDIT PRODUCTS HERE ===
    // Replace or add products. For each product: id must be unique number, name, price (₹), desc, img (text or image URL)
    const products = [
      {id:1,name:'Oversized T-Shirt',price:399,desc:'Comfort fit, 100% cotton',img:'https://via.placeholder.com/400x300?text=Oversized+T-Shirt'},
      {id:2,name:'Cargo Pants',price:799,desc:'Durable cargo with pockets',img:'https://via.placeholder.com/400x300?text=Cargo+Pants'},
      {id:3,name:'Hoodie',price:999,desc:'Warm hoodie, unisex',img:'https://via.placeholder.com/400x300?text=Hoodie'},
      {id:4,name:'Casual Shirt',price:549,desc:'Smart casual shirt',img:'https://via.placeholder.com/400x300?text=Casual+Shirt'},
      {id:5,name:'Joggers',price:459,desc:'Comfort joggers',img:'https://via.placeholder.com/400x300?text=Joggers'},
      {id:6,name:'Denim Jacket',price:1299,desc:'Stylish denim jacket',img:'https://via.placeholder.com/400x300?text=Denim+Jacket'}
    ];

    // render products
    const grid = document.getElementById('product-grid');
    products.forEach(p=>{
      const card = document.createElement('div');card.className='card';
      card.innerHTML = `
        <div style="overflow:hidden;border-radius:8px;height:220px;display:flex;align-items:center;justify-content:center;background:#07130d"><img src="${p.img}" alt="${p.name}" style="max-width:100%;max-height:100%;object-fit:cover"/></div>
        <div class="title">${p.name}</div>
        <div class="small">${p.desc}</div>
        <div class="flex" style="margin-top:10px;justify-content:space-between;align-items:center">
          <div class="price">₹${p.price}</div>
          <div>
            <button data-id="${p.id}" class="btn add">Add</button>
          </div>
        </div>
      `;
      grid.appendChild(card);
    });

    // cart logic (local demo)
    const CART_KEY = 'rp_cart_v1';
    function loadCart(){ try{ return JSON.parse(localStorage.getItem(CART_KEY))||{} }catch(e){return{}} }
    function saveCart(c){ localStorage.setItem(CART_KEY,JSON.stringify(c)) }
    function addToCart(id){ const cart=loadCart(); cart[id]= (cart[id]||0)+1; saveCart(cart); refreshCartUI(); }
    function removeFromCart(id){ const cart=loadCart(); if(!cart[id]) return; cart[id]--; if(cart[id]<=0) delete cart[id]; saveCart(cart); refreshCartUI(); }
    function clearCart(){ localStorage.removeItem(CART_KEY); refreshCartUI(); }

    document.addEventListener('click',function(e){ if(e.target && e.target.matches('.add')) addToCart(e.target.dataset.id); });

    const cartPanel = document.getElementById('cart-panel');
    document.getElementById('open-cart').addEventListener('click',()=>{ cartPanel.style.display = cartPanel.style.display==='none'? 'block':'none'; refreshCartUI(); });

    function refreshCartUI(){ const cartItems = document.getElementById('cart-items'); cartItems.innerHTML=''; const cart=loadCart(); let total=0; let count=0;
      for(const id in cart){ const qty=cart[id]; const prod = products.find(p=>p.id==id); if(!prod) continue; count+=qty; total += prod.price*qty;
        const row = document.createElement('div'); row.className='cart-item'; row.innerHTML = `
          <div style='flex:1'>
            <div style='font-weight:700;color:#eaffef'>${prod.name}</div>
            <div class='small'>₹${prod.price} x ${qty} = ₹${prod.price*qty}</div>
          </div>
          <div style='text-align:right'>
            <div class='qty'>${qty}</div>
            <div style='margin-top:6px'>
              <button onclick="removeFromCart(${id})" style='margin-right:6px' class='btn'>-</button>
              <button onclick="addToCart(${id})" class='btn'>+</button>
            </div>
          </div>
        `;
        cartItems.appendChild(row);
      }
      document.getElementById('cart-total').textContent = total;
      document.getElementById('cart-count').textContent = count;
    }
    refreshCartUI();

    // checkout (demo)
    document.getElementById('place-order').addEventListener('click',()=>{
      const name=document.getElementById('c-name').value.trim();
      const phone=document.getElementById('c-phone').value.trim();
      const address=document.getElementById('c-address').value.trim();
      const email=document.getElementById('c-email').value.trim();
      const cart=loadCart(); if(Object.keys(cart).length===0){ alert('Cart khaali hai'); return; }
      if(!name||!phone||!address){ alert('Naam, phone aur address bhar do'); return; }

      let summary = `Order from ${name}
Phone: ${phone}
Address: ${address}
Email: ${email}

Items:
`;
      let total=0;
      for(const id in cart){ const qty=cart[id]; const prod = products.find(p=>p.id==id); summary += `${prod.name} x ${qty} = ₹${prod.price*qty}
`; total += prod.price*qty }
      summary += `
Total: ₹${total}`;

      document.getElementById('order-msg').textContent = 'Order placed! (Demo) — order summary shown in alert.';
      alert(summary + '

Note: Yeh demo store hai. Real payments / order saving server se integrate karna hoga.');
      clearCart();
      document.getElementById('c-name').value='';document.getElementById('c-phone').value='';document.getElementById('c-address').value='';document.getElementById('c-email').value='';
    });

    // handy: scroll to products
    document.getElementById('shop-now').addEventListener('click',()=>{ document.getElementById('products').scrollIntoView({behavior:'smooth'}); });
  </script>
