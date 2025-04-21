# Fondamenta di React

### 🔷 Cos’è React?

React è una libreria JavaScript open-source sviluppata da Facebook per costruire interfacce utente. È oggi uno degli strumenti più usati per creare applicazioni web moderne, perché permette di organizzare la UI (quindi l'interfaccia grafica) in piccoli **blocchi riutilizzabili chiamati componenti**.

**Perché usare React?**

- **Riutilizzabilità:** ogni componente può essere usato più volte, anche con dati diversi.
- **Reattività:** cambia solo ciò che serve, grazie al DOM virtuale (migliori performance).
- **Modularità:** l'app si costruisce come un puzzle.
- **Tooling:** Create React App, DevTools, librerie di supporto (es. React Router, Axios).

### 📐 Com’è strutturata un'app React?

Un’app React è una composizione di componenti, ognuno dei quali rappresenta una parte dell’interfaccia utente.

- **Componenti:** funzioni che restituiscono markup (JSX)
- **Props:** "parametri" passati ai componenti (immutabili)
- **Stato (state):** dati che cambiano nel tempo (mutabili solo internamente)
- **Hooks:** funzioni speciali (come useState) per lavorare con stato ed effetti

### 🔷 JSX: Scrivere HTML dentro JavaScript

JSX (JavaScript XML) è una sintassi che permette di scrivere codice simile all’HTML all’interno di JavaScript, ma con regole specifiche. Non è obbligatorio in React, ma è fortemente consigliato, perché rende il codice molto più leggibile e naturale.
Esempio:

```jsx
function Component() {
  return <h1>Hello Wolrd!</h1>;
}
```

Scrittura equivalente:

```jsx
const Component = () => {
  return <h1>Hello World!</h1>;
}
```

### 📌 Differenze tra JSX e HTML

HTML             | JSX
<div class="x">  | <div className="x">
<label for="x">  | <label htmlFor="x">
Tutto è permesso | Un solo elemento padre, es. un <div> o <>
Attributi liberi | Solo attributi validi in JS

⚠️ **Attenzione:** JSX non è HTML, è JavaScript!

### 🔷 Stato (useState) nei componenti
React utilizza uno stato interno per gestire dati che possono cambiare nel tempo. Lo stato è **locale al componente** e si modifica tramite una funzione apposita, mai direttamente.

Sintassi base:

```jsx
const [valore, setValore] = useState(valoreIniziale);
```

Cosa succede:

**valore:** contiene il valore corrente
**setValore:** aggiorna il valore e re-renderizza il componente

### 🔷 Eventi in React

Gli eventi in React sono associati a funzioni, che sono definite come **handler**. Ogni evento che si verifica nell'interfaccia utente (come un click su un pulsante o il cambiamento di un valore in un campo di input) può essere gestito da una funzione che viene invocata quando l'evento si verifica.

Ad esempio, se vuoi gestire il clic su un pulsante, crei una funzione per gestire quell'evento e la associ all’elemento tramite la prop onClick:

```jsx
const App = () => {
  // Funzione che gestisce l'evento click
  const handleClick = () => {
    console.log("Pulsante cliccato!");
  };

  return (
    <button onClick={handleClick}>Cliccami!</button>
  );
}
```

Nell’esempio sopra, la funzione handleClick è l'event handler che verrà chiamata quando l'utente fa clic sul pulsante.

React usa un oggetto chiamato SyntheticEvent per gestire gli eventi. Questo oggetto è un wrapper per l'evento nativo, che fornisce una comportamento uniforme su tutti i browser.
Se vogliamo passare argomenti personalizzati alla funzione, dobbiamo utilizzare una funzione di freccia per incapsulare l'event handler. Tuttavia, il primo argomento che viene passato ad ogni gestore di eventi è sempre l'oggetto evento (un’istanza di SyntheticEvent).

Esempio:

```jsx
function App() {
  const handleClick = (id, event) => {
    console.log(`Pulsante con ID ${id} è stato cliccato.`);
  };

  return (
    <button onClick={(e) => handleClick(1, e)}>Clicca me</button>
  );
}
```

### Tipi di eventi più comuni in React

**onClick**: evento di clic

```jsx
<button onClick={handleClick}>Clicca qui</button>
```

**onChange**: evento quando un valore di un campo di input cambia

```jsx
<input type="text" onChange={handleChange} />
```

**onSubmit**: evento quando un form viene inviato

```jsx
<form onSubmit={handleSubmit}>
  <button type="submit">Invia</button>
</form>
```

**onFocus / onBlur**: eventi di focus e perdita del focus (utile nei campi di input)

```jsx
<input onFocus={handleFocus} onBlur={handleBlur} />
```

**onMouseOver / onMouseOut**: eventi quando il mouse passa sopra o lascia un elemento

```jsx
<div onMouseOver={handleMouseOver} onMouseOut={handleMouseOut}>Passa sopra</div>
```

### Debouncing degli eventi (esempio pratico)

Un concetto utile da conoscere è il **debouncing**, che limita la frequenza con cui un evento viene eseguito. È particolarmente utile con eventi come onChange su campi di ricerca, in modo da non inviare una richiesta a ogni lettera digitata, ma solo dopo che l'utente ha finito di scrivere.

Esempio di debouncing con onChange:

```jsx
import { useState } from "react";

function Ricerca() {
  const [termine, setTermine] = useState("");

  const handleChange = (e) => {
    const nuovoTermine = e.target.value;
    setTermine(nuovoTermine);
    // Esegui la logica di debouncing qui
  };

  return (
    <div>
      <input type="text" onChange={handleChange} placeholder="Cerca..." />
    </div>
  );
}
```

### ✋ e.preventDefault() e e.stopPropagation()

Quando gestiamo eventi in React (come onClick, onSubmit, onChange), spesso abbiamo bisogno di controllare il comportamento dell’evento. Queste due funzioni ti permettono di farlo:

**🛑 e.preventDefault() – Impedisce il comportamento predefinito dell’evento**

**Cosa fa?**
Blocca l’azione automatica associata a un elemento HTML.

**Esempi di comportamenti predefiniti**:
**Quando invii un <form>**: il browser ricarica la pagina
**Quando clicchi su un link <a>**: il browser naviga verso un altro URL
**Quando selezioni un’opzione in una dropdown**: la pagina può scorrere

Esempio pratico con un form:

```jsx
function Form() {
  const handleSubmit = (e) => {
    e.preventDefault(); // Impedisce il refresh automatico del form
    alert("Form inviato, ma la pagina NON si è ricaricata!");
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" placeholder="Scrivi qualcosa" />
      <button type="submit">Invia</button>
    </form>
  );
}
```

Quando usarlo?
Ogni volta che vuoi gestire un’azione tu stesso, senza lasciare che il browser faccia tutto da solo.

Esempio con un link:

```jsx
function LinkFinto() {
  const handleClick = (e) => {
    e.preventDefault(); // Impedisce la navigazione
    alert("Hai cliccato, ma non sei andato da nessuna parte.");
  };

  return (
    <a href="https://google.com" onClick={handleClick}>Non andare su Google</a>
  );
}
```

**⛔ e.stopPropagation() – Blocca la "propagazione" dell’evento verso l’alto**

**Cosa fa?**
Ferma l’evento nel suo percorso verso l’alto nel DOM.
In pratica, impedisce che l’evento venga “ereditato” dai genitori dell’elemento su cui è stato generato.

**Immagina una matrioska:**
Se clicchi sul pupazzetto più interno, anche quelli esterni ricevono il clic... a meno che tu non dica: "STOP, basta così!"