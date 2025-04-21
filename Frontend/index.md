# Modulo 1: React frontend #

## Fondamenta di React + JSX ##

### 🎯 Obiettivi ###

Comprendere la struttura base di un'app React
Usare JSX per creare componenti
Gestire stato e props
Gestire eventi (click, change, submit)

### 🧠 Lezioni teoriche ###

Cos’è React? Com’è strutturata un’app (componenti, props, state)
JSX e differenze con HTML
useState: gestione dello stato nei componenti
Eventi in React: onClick, onChange, onSubmit

### 🧪 Esercizi pratici ###

Contatore (+, -, reset)
Form con input che aggiorna lo stato in tempo reale
Lista dinamica di elementi (es. to-do locali)

## Hook + Routing ##

### 🎯 Obiettivi

Usare useEffect per eseguire codice al montaggio del componente
Creare navigazione tra pagine con react-router-dom
Simulare fetch di dati con useEffect

### 🧠 Lezioni teoriche

useEffect: comportamento e dipendenze
Libreria react-router-dom: setup, <Routes>, <Route>, <Link>
Navigazione dinamica con useParams

### 🧪 Esercizi pratici

App con 3 pagine: Home, About, Contatti
Simulazione fetch (setTimeout) e loading UI
Pagina di dettaglio: clic su elemento → mostra dettagli in altra route

## Chiamate API reali + Styling con CSS Modules

### 🎯 Obiettivi

Fare richieste HTTP reali con axios
Gestire loading e errori
Usare CSS Modules per scrivere stili “modulari” e ordinati
Applicare uno stile semplice ma coerente all’intera app

### 🧠 Lezioni teoriche

Come usare axios (GET, POST)
Come gestire errori (try/catch, .catch)
Cosa sono i CSS Modules e perché sono utili
Struttura dei file .module.css
Concetti CSS fondamentali: flexbox, padding, margini, font-size

### 🧪 Esercizi pratici

Chiamare https://jsonplaceholder.typicode.com/posts
Mostrare lista post
Dettaglio post con route dinamica
Aggiunta post fittizia con un form (dati salvati solo in locale)
Applicare uno stile semplice usando .module.css

### 📌 Obiettivo della settimana:

Un’app completa con:

Routing
Fetch reale con axios
Stile modulare con CSS Modules

### 💼 Mini Progetto 

Blog Viewer (o ToDo avanzata)
Pagina Home → lista post da API
Pagina Dettaglio → mostra il contenuto di un singolo post
Pagina "Nuovo Post" → form che simula l’inserimento di un nuovo contenuto
Stile con CSS Modules (layout base, colori coerenti, mobile responsive)

### 🧰 Strumenti da installare

react
react-dom
react-router-dom
axios
✅ Tutto può essere gestito con Create React App

### 🚀 Setup del progetto (con CRA)

Apri il terminale e digita:

```bash
npx create-react-app blog-app
cd blog-app
npm install axios react-router-dom
```

