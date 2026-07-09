# Resturant-website
import React, { useState } from "react";
import "./App.css";

const menu = [
  {
    id: 1,
    name: "french fries",
    desc: "Crispy, golden fries served hot.
",
    price: 30,
    badge: "Chef's Pick",
    image: "https://www.citypng.com/photo/21a7de17/fluffy-french-fries-with-herbs-on-a-bowl-hd-transparent-png",
  },
  {
    id: 2,
    name: "Crispy Calamari",
    desc: "Lightly fried calamari served with aioli.",
    price: 14,
    badge: "",
    image: "https://picsum.photos/200?2",
  },
  {
    id: 3,
    name: "Roasted Beetroot Salad",
    desc: "Goat cheese, walnuts and balsamic.",
    price: 13,
    badge: "Vegetarian",
    image: "https://picsum.photos/200?3",
  },
  {
    id: 4,
    name: "Seared Scallops",
    desc: "Scallops with pancetta.",
    price: 19,
    badge: "Chef's Pick",
    image: "https://picsum.photos/200?4",
  },
  {
    id: 5,
    name: "Chicken Liver Parfait",
    desc: "Served with toasted brioche.",
    price: 14,
    badge: "",
    image: "https://picsum.photos/200?5",
  },
  {
    id: 6,
    name: "'Nduja Arancini",
    desc: "Crispy risotto balls.",
    price: 12,
    badge: "Spicy",
    image: "https://picsum.photos/200?6",
  },
];

function App() {
  const [cart, setCart] = useState([]);
  const [showCart, setShowCart] = useState(false);

  const addToCart = (item) => {
    setCart([...cart, item]);
  };

  const total = cart.reduce((sum, item) => sum + item.price, 0);

  const checkout = () => {
    if (cart.length === 0) {
      alert("Cart is empty!");
      return;
    }

    alert(`Order placed successfully!\nTotal: £${total}`);
    setCart([]);
  };

  return (
    <div>
      <header className="header">
        <h1>Osteria Locale</h1>

        <button
          className="order-btn"
          onClick={() => setShowCart(!showCart)}
        >
          🛒 Order ({cart.length})
        </button>
      </header>

      <div className="tabs">
        <button>Starters</button>
        <button>Mains</button>
        <button>Desserts</button>
        <button>Drinks</button>
      </div>

      <div className="container">
        {menu.map((item) => (
          <div className="card" key={item.id}>
            <img src={item.image} alt={item.name} />

            <div className="info">
              {item.badge && (
                <span className="badge">{item.badge}</span>
              )}

              <h2>{item.name}</h2>

              <p>{item.desc}</p>

              <button
                className="add-btn"
                onClick={() => addToCart(item)}
              >
                + Add
              </button>
            </div>

            <h3 className="price">£{item.price}</h3>
          </div>
        ))}
      </div>

      {showCart && (
        <div className="cart">
          <h2>Your Order</h2>

          {cart.map((item, index) => (
            <p key={index}>
              {item.name} - £{item.price}
            </p>
          ))}

          <h3>Total : £{total}</h3>

          <button className="checkout" onClick={checkout}>
            Checkout
          </button>
        </div>
      )}
    </div>
  );
}

export default App;
