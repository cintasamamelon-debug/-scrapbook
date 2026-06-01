# -scrapbook
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Scrapbook Kenangan ✨</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&family=Pacifico&display=swap" rel="stylesheet">

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html{
    scroll-behavior:smooth;
}

body{
    font-family:'Poppins',sans-serif;
    background:linear-gradient(135deg,#ffeaf3,#fff8e7);
    overflow-x:hidden;
    color:#444;
}

/* COVER */
.cover{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    text-align:center;
    padding:20px;
}

.cover-box{
    background:white;
    padding:40px;
    border-radius:30px;
    max-width:700px;
    box-shadow:0 15px 40px rgba(0,0,0,.1);
}

.cover h1{
    font-family:'Pacifico',cursive;
    font-size:3rem;
    color:#ff5f9e;
}

.cover p{
    margin:15px 0 25px;
}

.btn{
    border:none;
    cursor:pointer;
    background:#ff5f9e;
    color:white;
    padding:14px 28px;
    border-radius:50px;
    font-size:1rem;
    transition:.3s;
}

.btn:hover{
    transform:translateY(-3px);
}

/* SECTION */
section{
    padding:80px 20px;
    max-width:1100px;
    margin:auto;
}

.title{
    text-align:center;
    color:#ff5f9e;
    margin-bottom:40px;
}

/* POLAROID */
.gallery{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
    gap:25px;
}

.polaroid{
    background:white;
    padding:10px 10px 25px;
    border-radius:8px;
    box-shadow:0 10px 25px rgba(0,0,0,.12);
    transform:rotate(-2deg);
    transition:.3s;
}

.polaroid:nth-child(even){
    transform:rotate(2deg);
}

.polaroid:hover{
    transform:scale(1.05);
}

.polaroid img{
    width:100%;
    height:250px;
    object-fit:cover;
    border-radius:5px;
}

.polaroid p{
    text-align:center;
    margin-top:10px;
}

/* TIMELINE */
.timeline{
    position:relative;
}

.timeline::before{
    content:'';
    position:absolute;
    left:20px;
    top:0;
    width:4px;
    height:100%;
    background:#ff5f9e;
}

.event{
    margin-left:60px;
    margin-bottom:30px;
    background:white;
    padding:20px;
    border-radius:15px;
    box-shadow:0 8px 20px rgba(0,0,0,.08);
}

.event h3{
    color:#ff5f9e;
}

/* MESSAGE */
.message{
    background:white;
    padding:35px;
    border-radius:20px;
    text-align:center;
    box-shadow:0 8px 20px rgba(0,0,0,.08);
}

/* HEARTS */
.heart{
    position:fixed;
    font-size:20px;
    pointer-events:none;
    animation:float 5s linear forwards;
}

@keyframes float{
    from{
        transform:translateY(0);
        opacity:1;
    }
    to{
        transform:translateY(-100vh);
        opacity:0;
    }
}

/* HIDDEN */
.hidden{
    display:none;
}

footer{
    text-align:center;
    padding:30px;
    color:#777;
}
</style>
</head>
<body>

<!-- MUSIK -->
<audio id="music" loop>
    <!-- Ganti music.mp3 dengan lagu kamu -->
    <source src="music.mp3" type="audio/mpeg">
</audio>

<!-- COVER -->
<div class="cover" id="cover">
    <div class="cover-box">
        <h1>Scrapbook Kenangan ✨</h1>
        <p>
            Sebuah kumpulan momen yang akan selalu dikenang.
        </p>

        <button class="btn" onclick="startBook()">
            💖 Buka Scrapbook
        </button>
    </div>
</div>

<!-- KONTEN -->
<div id="content" class="hidden">

<section>
    <h2 class="title">📸 Galeri Kenangan</h2>

    <div class="gallery">

        <div class="polaroid">
            <img src="https://picsum.photos/500/500?1">
            <p>Momen pertama</p>
        </div>

        <div class="polaroid">
            <img src="https://picsum.photos/500/500?2">
            <p>Hari yang menyenangkan</p>
        </div>

        <div class="polaroid">
            <img src="https://picsum.photos/500/500?3">
            <p>Kenangan favorit</p>
        </div>

        <div class="polaroid">
            <img src="https://picsum.photos/500/500?4">
            <p>Tidak terlupakan</p>
        </div>

    </div>
</section>

<section>
    <h2 class="title">🗓️ Timeline Cerita</h2>

    <div class="timeline">

        <div class="event">
            <h3>Awal Cerita</h3>
            <p>Hari pertama semuanya dimulai.</p>
        </div>

        <div class="event">
            <h3>Petualangan</h3>
            <p>Banyak momen lucu dan berharga.</p>
        </div>

        <div class="event">
            <h3>Hari Spesial</h3>
            <p>Salah satu hari terbaik yang pernah ada.</p>
        </div>

    </div>
</section>

<section>
    <h2 class="title">💌 Pesan</h2>

    <div class="message">
        <p id="typing"></p>
    </div>
</section>

<footer>
    Dibuat dengan ❤️ untuk mengabadikan kenangan
</footer>

</div>

<script>

function startBook(){

    document.getElementById('cover').style.display='none';
    document.getElementById('content').classList.remove('hidden');

    document.getElementById('music').play();

    typingEffect();

    setInterval(createHeart,400);
}

const text =
"Terima kasih sudah menjadi bagian dari cerita ini. Semoga setiap foto dan kenangan di scrapbook ini selalu membawa senyum ketika suatu hari nanti dikenang kembali.";

let i = 0;

function typingEffect(){

    const target = document.getElementById('typing');

    const interval = setInterval(()=>{

        target.innerHTML += text.charAt(i);
        i++;

        if(i >= text.length){
            clearInterval(interval);
        }

    },40);
}

function createHeart(){

    const heart = document.createElement('div');

    heart.classList.add('heart');
    heart.innerHTML = '💖';

    heart.style.left = Math.random()*100 + 'vw';
    heart.style.bottom = '-20px';

    document.body.appendChild(heart);

    setTimeout(()=>{
        heart.remove();
    },5000);
}

</script>

</body>
</html>