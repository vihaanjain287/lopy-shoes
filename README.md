<!DOCTYPE html><html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Lopy Shoes</title>
<style>
body{font-family:Arial;margin:0;background:#0f0f0f;color:white}
header{background:#000;padding:20px;text-align:center;border-bottom:2px solid gold}
.logo{font-size:28px;font-weight:bold;color:gold}
nav{background:#111;display:flex;justify-content:center;gap:25px;padding:10px;border-bottom:1px solid #333}
nav a{text-decoration:none;color:gold;font-weight:bold}
.hero{padding:50px 20px;text-align:center;background:linear-gradient(black,#1a1a1a)}
.hero h1{color:gold}
section{padding:40px 20px;text-align:center}/* search bar */ .search-box{margin:20px auto;max-width:400px} .search-box input{width:100%;padding:10px;border-radius:6px;border:none}

.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:25px;margin-top:30px} .card{background:#1a1a1a;border-radius:12px;padding:15px;box-shadow:0 3px 10px rgba(0,0,0,0.5)} .card img{width:100%;border-radius:10px} .price{color:gold;font-weight:bold}

select{padding:8px;border-radius:6px;margin-top:8px;border:none}

button{background:gold;color:black;border:none;padding:10px 16px;border-radius:6px;margin-top:10px;font-weight:bold;cursor:pointer} button:hover{opacity:0.9}

/* cart */ .cart{position:fixed;right:10px;bottom:10px;background:#1a1a1a;border:1px solid gold;padding:15px;border-radius:10px;width:260px;max-height:350px;overflow:auto} .cart h3{color:gold;margin-top:0} .cart-item{display:flex;justify-content:space-between;font-size:14px;margin:5px 0} .checkout{background:gold;color:black;width:100%;margin-top:10px}

/* order form */ .order-form{background:#1a1a1a;padding:20px;border-radius:10px;max-width:400px;margin:20px auto} .order-form input,.order-form textarea{width:100%;padding:10px;margin:5px 0;border:none;border-radius:6px}

/* reviews */ .reviews{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:20px;margin-top:20px} .review-card{background:#1a1a1a;padding:15px;border-radius:10px} .stars{color:gold}

footer{background:black;color:gold;text-align:center;padding:15px;margin-top:30px;border-top:2px solid gold} </style>

</head>
<body><header>
<div class="logo">Lopy Shoes</div>
<p>Premium Style • Premium Comfort</p>
</header><nav>
<a href="#home">Home</a>
<a href="#products">Products</a>
<a href="#reviews">Reviews</a>
<a href="#order">Order</a>
</nav><div class="hero" id="home">
<h1>Welcome to Lopy Shoes</h1>
<p>Discover premium stylish footwear</p>
</div><section id="products">
<h2 style="color:gold">Our Products</h2><div class="search-box">
<input type="text" id="search" placeholder="Search shoes..." onkeyup="searchProducts()">
</div><div class="products" id="product-list"><div class="card" data-name="sport sneakers">
<img src="https://images.unsplash.com/photo-1542291026-7eec264c27ff">
<h3>Sport Sneakers</h3>
<p class="price">₹1999</p>
<select id="size1">
<option value="7">Size 7</option>
<option value="8">Size 8</option>
<option value="9">Size 9</option>
<option value="10">Size 10</option>
</select>
<button onclick="addToCart('Sport Sneakers',1999,'size1')">Add to Cart</button>
</div><div class="card" data-name="running shoes">
<img src="https://images.unsplash.com/photo-1600185365483-26d7a4cc7519">
<h3>Running Shoes</h3>
<p class="price">₹2499</p>
<select id="size2">
<option value="7">Size 7</option>
<option value="8">Size 8</option>
<option value="9">Size 9</option>
<option value="10">Size 10</option>
</select>
<button onclick="addToCart('Running Shoes',2499,'size2')">Add to Cart</button>
</div><div class="card" data-name="casual shoes">
<img src="https://images.unsplash.com/photo-1525966222134-fcfa99b8ae77">
<h3>Casual Shoes</h3>
<p class="price">₹1799</p>
<select id="size3">
<option value="7">Size 7</option>
<option value="8">Size 8</option>
<option value="9">Size 9</option>
<option value="10">Size 10</option>
</select>
<button onclick="addToCart('Casual Shoes',1799,'size3')">Add to Cart</button>
</div></div>
</section><div class="cart">
<h3>🛒 Cart</h3>
<div id="cart-items"></div>
<p>Total: ₹<span id="total">0</span></p>
<button class="checkout" onclick="showOrderForm()">Checkout</button>
</div><section id="order">
<h2 style="color:gold">Order Details</h2><div class="order-form" id="orderForm" style="display:none">
<input type="text" id="name" placeholder="Your Name">
<input type="text" id="phone" placeholder="Phone Number">
<textarea id="address" placeholder="Delivery Address"></textarea><h3>UPI Payment</h3>
<p>Send payment to UPI ID: <b>lopyshoes@upi</b></p><button onclick="placeOrder()">Place Order on WhatsApp</button>

</div>
</section><section id="reviews">
<h2 style="color:gold">Customer Reviews</h2><div class="reviews"><div class="review-card">
<p>"Amazing quality shoes!"</p>
<div class="stars">★★★★★</div>
<p>- Rahul</p>
</div><div class="review-card">
<p>"Very comfortable and stylish."</p>
<div class="stars">★★★★★</div>
<p>- Aman</p>
</div><div class="review-card">
<p>"Fast delivery and great price."</p>
<div class="stars">★★★★☆</div>
<p>- Neha</p>
</div></div>
</section><footer>
<p>© 2026 Lopy Shoes</p>
</footer><script>
let cart=[]

function addToCart(name,price,sizeId){
let size=document.getElementById(sizeId).value
cart.push({name,price,size})
renderCart()
}

function renderCart(){
let cartItems=document.getElementById('cart-items')
cartItems.innerHTML=''
let total=0

cart.forEach(item=>{
let div=document.createElement('div')
div.className='cart-item'
div.innerHTML=`<span>${item.name} (${item.size})</span><span>₹${item.price}</span>`
cartItems.appendChild(div)
 total+=item.price
})

document.getElementById('total').innerText=total
}

function showOrderForm(){
if(cart.length===0){alert('Cart is empty');return}

document.getElementById('orderForm').style.display='block'
}

function placeOrder(){
let name=document.getElementById('name').value
let phone=document.getElementById('phone').value
let address=document.getElementById('address').value

let message=`Order from Lopy Shoes:%0AName: ${name}%0APhone: ${phone}%0AAddress: ${address}%0A`
let total=0

cart.forEach(item=>{
message+=`- ${item.name} Size ${item.size} ₹${item.price}%0A`
 total+=item.price
})

message+=`Total: ₹${total}`

window.open(`https://wa.me/919909986441?text=${message}`)
}

function searchProducts(){
let input=document.getElementById('search').value.toLowerCase()
let products=document.querySelectorAll('#product-list .card')

products.forEach(p=>{
let name=p.getAttribute('data-name')
if(name.includes(input)){
 p.style.display='block'
}else{
 p.style.display='none'
}
})
}
</script></body>
</html>