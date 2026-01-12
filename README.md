<html lang="id">
<head>
<meta charset="UTF-8">
<title>Sebuah Undangan</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=Inter:wght@300;400&display=swap');

*{margin:0;padding:0;box-sizing:border-box;}

body{
    height:100vh;
    background:radial-gradient(circle at top,#f7f6f4,#e6e3de);
    display:flex;
    justify-content:center;
    align-items:center;
    font-family:'Inter', sans-serif;
    color:#2b2b2b;
}

/* === KERTAS UNDANGAN === */
.wrapper{position:relative;}

.shadow{
    position:absolute;
    inset:12px;
    background:#fff;
    border-radius:26px;
    filter:blur(25px);
    opacity:0.35;
}

.invitation{
    width:650px;
    min-height:460px;
    background:linear-gradient(180deg,#ffffff,#f9f8f6);
    border-radius:26px;
    padding:70px 80px;
    box-shadow:0 40px 80px rgba(0,0,0,0.12);
    position:relative;
    overflow:hidden;
}

.invitation::before{
    content:"";
    position:absolute;
    top:0;
    left:50%;
    width:120px;
    height:3px;
    background:linear-gradient(90deg,transparent,#c9bfae,transparent);
    transform:translateX(-50%);
}

/* === PAGE === */
.page{display:none; animation:pageIn 1.1s ease;}
.page.active{display:block;}

@keyframes pageIn{
    from{opacity:0; transform:translateY(30px);}
    to{opacity:1; transform:translateY(0);}
}

/* === TEXT === */
.title{
    font-family:'Playfair Display', serif;
    font-size:42px;
    font-style:italic;
    text-align:center;
    margin-bottom:35px;
    letter-spacing:0.04em;
}

.text{
    font-size:17px;
    line-height:1.95;
    text-align:center;
    color:#4a4a4a;
}

.footer{text-align:center;margin-top:55px;}

button{
    padding:12px 36px;
    border-radius:40px;
    border:1px solid #2b2b2b;
    background:transparent;
    font-size:14px;
    letter-spacing:0.18em;
    cursor:pointer;
    transition:0.4s;
}

button:hover{
    background:#2b2b2b;
    color:#fff;
}

/* === PAGE 3 === */
.question{
    font-family:'Playfair Display', serif;
    font-size:22px;
    font-style:italic;
    text-align:center;
    margin:45px 0;
}

.buttons{
    position:relative;
    height:90px;
}

.yes{
    position:absolute;
    left:50%;
    transform:translateX(-120%);
}

.no{
    position:absolute;
    left:50%;
    transform:translateX(20%);
    border-color:#c3bdb3;
    color:#7a756d;
}

.no:hover{
    background:#ebe8e3;
}

.result{
    margin-top:45px;
    text-align:center;
    font-family:'Playfair Display', serif;
    font-size:21px;
    font-style:italic;
    display:none;
}
</style>
</head>

<body>

<div class="wrapper">
<div class="shadow"></div>

<div class="invitation">

<!-- PAGE 1 -->
<div class="page active" id="page1">
    <div class="title">Undangan</div>
    <div class="text">For you</div>
    <div class="footer">
        <button onclick="nextPage(2)">BUKA UNDANGAN</button>
    </div>
</div>

<!-- PAGE 2 -->
<div class="page" id="page2">
    <div class="title">Isi Surat</div>
    <div class="text">
        Dengan penuh kesadaran dan ketulusan,<br>
        izinkan aku menyampaikan kejujuran ini.<br><br>
        Perasaan ini hadir perlahan,<br>
        memberi ruang, memberi makna.<br><br>
        Bersamamu, aku belajar bahwa<br>
        ketenangan adalah bentuk rasa paling tulus.
    </div>
    <div class="footer">
        <button onclick="nextPage(3)">LANJUTKAN</button>
    </div>
</div>

<!-- PAGE 3 -->
<div class="page" id="page3">
    <div class="title">Pertanyaan</div>
    <div class="question">
        Maukah kamu menerima undangan ini,<br>
        untuk berjalan bersamaku ke depan?
    </div>

    <div class="buttons">
        <button class="yes" onclick="jawabIya()">IYA</button>
        <button class="no" id="noBtn">TIDAK</button>
    </div>

    <div class="result" id="result"></div>
</div>

</div>
</div>

<script>
/* === NAVIGASI PAGE === */
function nextPage(n){
    document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
    document.getElementById('page'+n).classList.add('active');
}

/* === KONFIGURASI === */
const nomorWA = "6285716758155"; // GANTI NOMOR
const noBtn = document.getElementById("noBtn");
let klikTidak = 0;

/* === JAWABAN IYA === */
function jawabIya(){
    const pesan = encodeURIComponent(
        "Aku telah membaca undanganmu.\n" +
        "Jawabanku adalah: Iya.\n\n" +
        "Mari kita jalani dengan tenang dan penuh makna 🤍"
    );
    window.open(`https://wa.me/${nomorWA}?text=${pesan}`, "_blank");

    tampilkanHasil("Terima kasih telah menerima undangan ini.<br>Semoga langkah kita selalu diberi ketenangan.");
}

/* === JAWABAN TIDAK === */
noBtn.addEventListener("click", ()=>{
    klikTidak++;

    if(klikTidak < 3){
        const parent = noBtn.parentElement;
        noBtn.style.left = Math.random() * (parent.offsetWidth - noBtn.offsetWidth) + "px";
        noBtn.style.top  = Math.random() * 40 + "px";

        if(klikTidak === 2) noBtn.innerText = "Yakin?";
    } else {
        jawabTidak();
    }
});

function jawabTidak(){
    const pesan = encodeURIComponent(
        "Aku sudah membaca undanganmu dengan penuh hormat.\n" +
        "Jawabanku saat ini adalah: Tidak.\n\n" +
        "Terima kasih atas keberanian dan kejujuranmu.\n" +
        "Semoga hatimu tetap kuat dan tenang 🤍"
    );
    window.open(`https://wa.me/${nomorWA}?text=${pesan}`, "_blank");

    tampilkanHasil("Terima kasih atas jawabannya.<br>Semoga kebaikan selalu menemukanmu.");
}

/* === HASIL === */
function tampilkanHasil(teks){
    const result = document.getElementById("result");
    result.style.display = "block";
    result.innerHTML = teks;
}
</script>

</body>
</html>
