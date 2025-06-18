# Twubric - Twitter Follower Rubric Viewer

A responsive Vue.js web app that allows users to review and manage their Twitter followers based on a scoring rubric. Users can sort, filter, visualize scores, and remove followers efficiently.

---

## 🚀 Features

* 🎯 Display followers in a responsive grid
* 📅 Filter followers by Twitter join date using a date picker
* 🔃 Sort by: Twubric Score, Friends, Influence, Chirpy (asc/desc toggle)
* ❌ Remove followers from the listing
* 📊 Chart view for visualizing Twubric scores using Chart.js
* ⌨️ Keyboard shortcuts for quick actions
* 🎨 Bootstrap-based modern UI with responsive layout

---

## 🗂️ File Structure

```
src/
├── App.vue                       # Main app layout and logic
├── main.js                       # Vue entry point
├── assets/                       # Icons, styles
├── components/
│   ├── FollowerCard.vue         # Individual follower card UI
│   ├── SortToolbar.vue          # Sort buttons toolbar
│   ├── DateFilter.vue           # Date picker filter component
│   └── TwubricChartView.vue     # Chart.js score visualization
├── views/
│   ├── TwubricChartView.vue     # Route-level view components
```

---

## 🧩 Keyboard Shortcuts

| Key | Action                 |
| --- | ---------------------- |
| `F` | Sort by Friends        |
| `I` | Sort by Influence      |
| `C` | Sort by Chirpy         |
| `S` | Sort by Twubric Score  |
| `R` | Remove top listed user |

---

## ⚙️ Installation & Running

```bash
# 1. Clone the repository
https://github.com/your-username/twubric-app.git

# 2. Navigate into project folder
cd twubric-app

# 3. Install dependencies
npm install

# 4. Start the development server
npm run dev
```

---

## 🔗 External API

* **Follower data:** [twubric.json](https://gist.githubusercontent.com/pandemonia/21703a6a303e0487a73b2610c8db41ab/raw/82e3ef99cde5b6e313922a5ccce7f38e17f790ac/twubric.json)

---

## 🛠 Built With

* [Vue.js 3](https://vuejs.org/)
* [Vite](https://vitejs.dev/)
* [Bootstrap 5](https://getbootstrap.com/)
* [Chart.js](https://www.chartjs.org/)

---

## 📚 Notes

* Fully ES6+ compliant (no jQuery)
* Responsive grid layout with adaptive controls
* Can be extended with export/download and additional visualizations

---

## 📜 License

This project is licensed under the MIT License.

---

## 👨‍💻 Author

Ayush Kumar
GitHub: [your-username](https://github.com/your-username)
