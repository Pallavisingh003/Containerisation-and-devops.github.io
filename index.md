# Containerisation and DevOps Lab
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Containerisation & DevOps Lab</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Poppins', sans-serif;
    background: #f4f6f9;
    color: #333;
}

/* HERO SECTION */
.hero {
    background: linear-gradient(135deg, #1e3c72, #2a5298);
    color: white;
    text-align: center;
    padding: 60px 20px;
}

.hero h1 {
    font-size: 2.8rem;
    font-weight: 700;
}

.hero p {
    margin-top: 10px;
    font-size: 1.1rem;
    opacity: 0.9;
}

/* CONTAINER */
.container {
    max-width: 1000px;
    margin: 50px auto;
    padding: 0 20px;
}

/* SECTION TITLES */
.section-title {
    font-size: 1.8rem;
    margin-bottom: 20px;
    position: relative;
    padding-left: 15px;
}

.section-title::before {
    content: "";
    position: absolute;
    left: 0;
    top: 8px;
    width: 6px;
    height: 25px;
    background: #2a5298;
    border-radius: 3px;
}

/* CARD STYLE */
.card {
    background: white;
    border-radius: 15px;
    padding: 30px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.08);
    transition: 0.3s ease;
}

.card:hover {
    transform: translateY(-5px);
}

/* TABLE */
table {
    width: 100%;
    border-collapse: collapse;
}

table td {
    padding: 12px;
    border-bottom: 1px solid #eee;
}

table td:first-child {
    font-weight: 600;
    color: #2a5298;
}

/* EXPERIMENT BUTTONS */
.exp-list {
    margin-top: 30px;
}

.exp-item {
    display: block;
    background: white;
    margin-bottom: 15px;
    padding: 18px 20px;
    border-radius: 12px;
    text-decoration: none;
    color: #2a5298;
    font-weight: 600;
    box-shadow: 0 5px 15px rgba(0,0,0,0.08);
    transition: 0.3s;
}

.exp-item:hover {
    background: #2a5298;
    color: white;
    transform: translateX(10px);
}

/* FOOTER */
footer {
    text-align: center;
    margin-top: 60px;
    padding: 20px;
    background: #1e3c72;
    color: white;
    font-size: 0.9rem;
}

/* RESPONSIVE */
@media(max-width: 600px){
    .hero h1 {
        font-size: 2rem;
    }
}
</style>
</head>

<body>

<div class="hero">
    <h1>Containerisation & DevOps Lab</h1>
    <p>Pallavi Singh | Semester 6 | SAP ID: 500119176</p>
</div>

<div class="container">

    <h2 class="section-title">🎓 Student Information</h2>

    <div class="card">
        <table>
            <tr>
                <td>Name</td>
                <td>Pallavi Singh</td>
            </tr>
            <tr>
                <td>SAP ID</td>
                <td>500119176</td>
            </tr>
            <tr>
                <td>Semester</td>
                <td>6</td>
            </tr>
            <tr>
                <td>Course</td>
                <td>Containerisation & DevOps</td>
            </tr>
        </table>
    </div>

    <h2 class="section-title">🧪 Experiments</h2>

    <div class="exp-list">
        <a href="#" class="exp-item">
            🚀 Experiment 1 – VM vs Container Setup
        </a>

        <a href="#" class="exp-item">
            🐳 Experiment 2 – Docker Installation, Configuration & Running Images
        </a>

        <a href="#" class="exp-item">
            🔥 Experiment 3 – Deploy NGINX Using Different Base Images & Compare Layers
        </a>

        <a href="#" class="exp-item">
            ⚙️ Experiment 4 – Docker Essentials (Dockerfile, Tagging, Publishing)
        </a>
    </div>

</div>

<footer>
    © 2026 Pallavi Singh | DevOps Lab Portfolio
</footer>

</body>
</html>
## 👩‍🎓 Student Information

| Field | Details |
|------|---------|
| **Name** | Pallavi Singh |
| **SAP ID** | 500119176 |
| **Semester** | 6 |
| **Course** | Containerisation & DevOps |


## Experiments

- [Experiment 1 – VM vs Container Setup](lab/exp1/README.md)
- [Experiment 2 – Docker Installation, Configuration, and Running Images](lab/exp2/README.md)
- [Experiment 3 – Docker Deploy NGINX Using Different Base Images and Comparing Image Layers](lab/exp3/README.md)
