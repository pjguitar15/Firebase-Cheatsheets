### Install Firebase
```
npm install --save firebase
```

### Configuration
> separate its file (firebase-config.js)
```javascript
import { initializeApp } from "firebase/app";
import { getFirestore } from "@firebase/firestore";

const firebaseConfig = {
  apiKey: "AIzaSyBG_9s2JJDUeBLtMenyPtIBsVLupa8vRB8",
  authDomain: "fir-tutorial-ad573.firebaseapp.com",
  projectId: "fir-tutorial-ad573",
  storageBucket: "fir-tutorial-ad573.appspot.com",
  messagingSenderId: "459866772432",
  appId: "1:459866772432:web:b029523d67a8c9f1981fd5",
  measurementId: "G-2R62T7YE0E",
};

const app = initializeApp(firebaseConfig);

export const db = getFirestore(app);
```

### Import to App
```javascript
import { db } from "./firebase-config";
import {
  collection,
  getDocs,
  addDoc,
  updateDoc,
  deleteDoc,
  doc,
  serverTimestamp,
  query, 
  orderBy
} from "firebase/firestore";
```

### Connect to its collections
```javascript
const collectionRef = collection(db, "collectionName");
```

### Create
```javascript
const addItem = async () => {
    await addDoc(collectionRef, { item: itemName, timestamp: serverTimestamp() });
};
```


### Update
```javascript
const updateItem = async (id, item) => {
    const userDoc = doc(db, "items", id);
    const newFields = { item: item + 1 };
    await updateDoc(userDoc, newFields);
};
```

### Delete
```javascript
 const deleteItem = async (id) => {
    const userDoc = doc(db, "collectionName", id);
    await deleteDoc(userDoc);
};
```

### Read
```javascript
useEffect(() => {
    const q = query(collectionRef, orderBy('timestamp', 'desc'))
    const getData = async () => {
      const data = await getDocs(q);
      setUsers(data.docs.map((doc) => ({ ...doc.data(), id: doc.id })));
    };

    getData();
}, []);
```
