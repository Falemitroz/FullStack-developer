# Chiamate API reali 

### 🎯 Obiettivi

- Fare richieste reali (es. a https://jsonplaceholder.typicode.com)
- Gestire correttamente loading e errori
- Separare lo stile di ogni componente con i CSS Modules
- Apprendere i concetti fondamentali del CSS moderno

## Le chiamate API con axios

### 📦 Cos'è axios?
È una libreria per effettuare richieste HTTP. È più semplice e leggibile di fetch, ed è usatissima nel mondo JavaScript.

**📥 Installazione**

```bash
npm install axios
```

**🧠 Come funziona?**

```jsx
import axios from "axios";
import { useEffect, useState } from "react";

const Utenti = () => {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [errore, setErrore] = useState(null);

  useEffect(() => {
      try{
        const request_URL = "https://jsonplaceholder.typicode.com/users";
        const response = axios.get(request_URL);
        setUsers(response.data);
        setLoading(false);
    } catch(error) {
        console.error("Errore:", error);
        setErrore("Errore nel caricamento!");
        setLoading(false);
    }
  }, []);

  if (loading) return <p>Caricamento...</p>;
  if (errore) return <p>{errore}</p>;

  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}
```

**🔍 Altri metodi di `axios`**

Metodo       | Uso
axios.get    | Ottiene dati da un'API
axios.post   | Invia dati (es. un form)
axios.put    | Aggiorna tutti i campi di una risorsa
axios.patch  | Aggiorna uno o piu' campi di una risorsa
axios.delete | Cancella una risorsa

**⚠️ Best practice**
- Mostrare sempre un messaggio di caricamento
- Gestire gli errori con `try/catch`
- Frontend: Le chiamate vengono centrallizzate in file chiamati api.js, contenuti nella directory `services`
- Backend: Le richieste del frontend arrivano ai file che gestiscono le rotte, che a loro volta invocano le funzioni dei relativi controller.

**Esempio di comunicazione FE -> BE**

client/services/api.js

```jsx
import axios from 'axios';

const API_URL = "http://localhost:5000";

export const createUser = async(userData) => {
    try{
        const response = await axios.POST(
                                    `${API_URL}/create-user`,
                                    /*eventuale header di autorizzazione*/,
                                    userData);
                                
        return response.data;
    } catch(error) {
        console.error("Errore durante la creazione dell'utente.", error);
        throw error;
    }
}

export const getUserById = async(userId) => {
    try{
        const response = await axios.GET(
                                    `${API_URL}/get-user/${userId}`,
                                    /*eventuale header di autorizzazione*/,
                                    );
                                
        return response.data;
    } catch(error) {
        console.error("Errore durante la ricerca dell'utente.", error);
        throw error;
    }
}
```

server/userRoutes.js

```jsx
const express = require('express');
const router = express.Router();

// Eventuale middleware per la protezione delle rotte
// const { authMiddleware } = require("../middleware/authMiddleware");

const userController = require("../controllers/userController");

router.post("/create-user", /* authMiddleware, */ userController.createUser);
router.get("/get-user/:userId", /* authMiddleware, */ userController.getUser);



module.exports = router;
```

server/controllers/userController.js

```jsx
const User = require("../models/user");

exports.createUser = async( req, res ) => {
    try{
        // codice per creare un utente
    } catch(error){
        // gestione dell'errore
    }
}

exports.getUser = async( req, res ) => {
    try{
        const { userId } = req.params;
        // codice per ottenere un utente
    } catch(error){
        // gestione dell'errore
    }
}
```

