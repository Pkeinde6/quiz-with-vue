# 🎯 Quiz with Vue

Un quiz interactif développé avec **Vue.js 3** et **Vite**.  
Ce projet illustre comment créer une application Vue modulaire et réactive, avec un système de questions/réponses et un suivi de progression en temps réel.

---

## 🚀 Démo

👉 (Ajoute ici le lien si tu déploies le projet sur **GitHub Pages**, **Netlify** ou **Vercel**)

---

## ✨ Fonctionnalités

- 📚 Gestion des questions à partir d’un fichier JSON (`public/quiz.json`)  
- 🎨 Interface simple, moderne et responsive  
- ⚡ Hot Reload via **Vite** pour un développement rapide  
- 🔄 Suivi de la progression du joueur  
- ✅ Validation des réponses et affichage des résultats  

---

## 🛠️ Technologies utilisées

- [Vue.js 3](https://vuejs.org/) — Framework JavaScript progressif  
- [Vite](https://vitejs.dev/) — Outil de build rapide et moderne  
- [JavaScript ES6+](https://developer.mozilla.org/fr/docs/Web/JavaScript)  
- [HTML5](https://developer.mozilla.org/fr/docs/Web/Guide/HTML/HTML5) & [CSS3](https://developer.mozilla.org/fr/docs/Web/CSS)  

---

## 📂 Structure du projet

.
├── public/

│ ├── favicon.ico

│ └── quiz.json # Données du quiz

├── src/
│ ├── components/
│ │ ├── progress.vue # Barre de progression
│ │ ├── question.vue # Composant Question
│ │ └── quiz.vue # Composant principal Quiz
│ ├── App.vue # Application principale
│ └── main.js # Point d'entrée Vue
├── index.html
├── package.json
├── vite.config.js
└── README.md


---

## ⚙️ Installation & Utilisation

### 1️⃣ Cloner le dépôt
```bash
git clone https://github.com/Pkeinde6/quiz-with-vue.git
cd quiz-with-vue

2️⃣ Installer les dépendances

npm install

3️⃣ Lancer le projet en mode développement

npm run dev

👉 Ouvre ton navigateur sur http://localhost:5173/
4️⃣ Générer la version production

npm run build

🎨 Personnalisation

    ✏️ Modifier public/quiz.json pour changer les questions/réponses

    🎭 Adapter le style en modifiant le CSS ou en ajoutant Tailwind/Bootstrap

    ⚡ Étendre les composants Vue pour ajouter :

        Un système de score détaillé

        Un mode multi-quiz

        Des transitions animées

📌 Roadmap (idées futures)

    🔊 Ajout d’un feedback sonore pour les bonnes/mauvaises réponses

    🌍 Mode multi-langues

    👥 Mode multi-joueurs

🤝 Contribution

Les contributions sont les bienvenues !

    Fork le repo

    Crée une branche (git checkout -b feature/ma-fonctionnalite)

    Commit tes modifications (git commit -m 'Ajout nouvelle fonctionnalité')

    Push ta branche (git push origin feature/ma-fonctionnalite)

    Ouvre une Pull Request 🚀

📄 Licence

Ce projet est distribué sous licence MIT.
Tu es libre de l’utiliser, le modifier et le partager.

