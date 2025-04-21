# Hook + Routing

## 🎯 Obiettivi

- Comprendere come React gestisce effetti collaterali tramite useEffect
- Implementare navigazione a più pagine con react-router-dom
- Simulare fetch di dati da un'API (es. con setTimeout)
- Usare parametri dinamici nell’URL per pagine di dettaglio

## Cos’è un Hook in React?
Un Hook è una funzione speciale introdotta in React 16.8 che ti permette di "agganciarti" alle funzionalità di React (come lo stato, il ciclo di vita, il contesto, ecc.) all'interno di un componente funzionale.
È un modo per "infilarsi" nei meccanismi interni dei componenti, senza dover scrivere codice complicato o ripetitivo.

**⚠️ Regole dei React Hook**
1. Si chiamano solo nel corpo principale del componente (non dentro `if`, `for`, o funzioni annidate)
2. Devono iniziare con `use` (React li riconosce così)

**Esempio in parole semplici:**

"Ho un componente che mostra il nome dell’utente. Quando clicco un bottone, voglio cambiare quel nome. Con useState, posso tenermi il nome in memoria (lo stato), e cambiarlo ogni volta che serve, senza ricaricare tutta la pagina."

### useEffect – Eseguire codice al montaggio del componente

**Cos'è?**
`useEffect` è un Hook fornito da React per gestire effetti collaterali: operazioni che coinvolgono il mondo esterno al componente, come:

richieste API
log su console
interazioni con il DOM
setTimeout, setInterval
listener di eventi

Sintassi base:

```jsx
import { useEffect } from 'react';

useEffect(() => {
  // Codice che vuoi eseguire dopo il "render"
}, []);
```

Il secondo argomento (`[]`) è l’array delle dipendenze:

- `[] vuoto`: effetto eseguito una sola volta, al montaggio
- `[variabile]`: effetto rieseguito ogni volta che quella variabile cambia
- **omesso**: effetto rieseguito ad ogni render

**Esempio – Simulazione fetch**

```jsx
import { useState, useEffect } from 'react';

const Lista = () => {
  const [items, setItems] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    setTimeout(() => {
      setItems(["Elemento 1", "Elemento 2", "Elemento 3"]);
      setLoading(false);
    }, 2000);
  }, []);

  return loading
    ? <p>Caricamento in corso...</p>
    : <ul>{items.map((item, i) => <li key={i}>{item}</li>)}</ul>;
}
```


## react-router-dom – Navigazione tra pagine in React
**Cos’è?**
Una libreria per navigazione client-side: permette di creare SPA (Single Page Applications) dove l’URL cambia senza ricaricare la pagina.

**Installazione (con Create React App)**

```bash
npm install react-router-dom
```

**Setup base**

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./Home";
import About from "./About";

const App = () => {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

**Navigazione con `<Link />`**

```jsx
import { Link } from 'react-router-dom';

function NavBar() {
  return (
    <nav>
      <Link to="/">Home</Link> | <Link to="/about">About</Link>
    </nav>
  );
}
```

**Navigazione dinamica con `useParams`**

**Quando serve?**
Quando hai una pagina che mostra dettagli di un elemento, in base a un parametro nell’URL (es: /post/3).

**Setup con route dinamica**

```jsx
<Route path="/post/:id" element={<PostDettaglio />} />
```

**Uso di `useParams`**

```jsx
import { useParams } from "react-router-dom";

function PostDettaglio() {
  const { id } = useParams();

  return <h2>Stai vedendo il post con ID: {id}</h2>;
}
```