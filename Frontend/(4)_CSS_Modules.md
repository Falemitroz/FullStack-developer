#  Styling con CSS Modules

**🎨 Cosa sono?**
Un CSS Module è un file `.module.css` i cui stili sono scoperti solo dal componente in cui vengono importati.

Questo evita **conflitti tra classi CSS** con lo stesso nome, specialmente in app grandi.

**🔧 Come si usa?**
✅ Struttura file

```swift
/src/components/Card/Card.js
/src/components/Card/Card.module.css
```

oppure

```swift
/src/components/Card.js
/src/styles/Card.module.css
```

✅ Card.module.css (esempio)

```css
.container {
  background-color: white;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.2);
}
```

✅ Card.js 

```jsx
import styles from "./Card.module.css"; // Prima struttura file

function Card({ children }) {
  return <div className={styles.container}>{children}</div>;
}
```

**Nota:** React genera nomi di classi unici come `Card_container__x81fd`
Quindi puoi usare `container` in più moduli senza conflitti!

**💡 Vantaggi dei CSS Modules**
- Scope limitato per ogni componente
- Meno rischio di errori
- Più chiaro dove nasce e vive ogni stile

### Fondamenti CSS utili da ripassare

Concetto                    | Descrizione veloce
`display: flex`             | Allineamento flessibile di elementi in riga o colonna
`gap`, `padding`, `margin`  | Spaziatura interna, esterna e tra gli elementi
`font-size`                 | Controllo della dimensione del testo
`color`, `background-color` | Gestione dei colori di testo e sfondo
`border`, `border-radius`   | Per creare angoli arrotondati e cornici visive