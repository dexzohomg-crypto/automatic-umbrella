```html
<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="vieeport" content="width=device-width, initial-scale=1.0">
<title>For You ❤️</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html,body{
    width:100%;
    height:100%;
    overflow:hidden;
    background:#03030a;
    font-family:Arial,sans-serif;
}

canvas{
    position:fixed;
    inset:0;
}

/* COVER */
.cover{
    position:fixed;
    inset:0;
    z-index:20;

    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;

    background:
        radial-gradient(
            circle at center,
            #401333 0%,
            #17091e 35%,
            #070711 70%,
            #020207 100%
        );

    transition:
        opacity 1.5s ease,
        transform 1.5s ease;
}

.cover.hide{
    opacity:0;
    transform:scale(1.3);
    pointer-events:none;
}

/* รูป */
.profile{
    position:relative;
    z-index:3;

    width:clamp(120px,18vw,190px);
    height:clamp(120px,18vw,190px);

    border-radius:50%;
    object-fit:cover;

    border:3px solid #ff8fbd;

    box-shadow:
        0 0 15px #ff4f9a,
        0 0 40px #ff1d75,
        0 0 80px rgba(255,30,120,.5);

    margin-bottom:25px;

    animation:profileGlow 2s infinite alternate;
}

@keyframes profileGlow{
    from{transform:scale(1);}
    to{transform:scale(1.05);}
}

/* ชื่อ */
.cover h1{FIRST}h1
    position:relative;
    z-index:3;

    font-size:clamp(40px,7vw,80px);

    color:#ffb1d3;

    text-align:center;

    text-shadow:
        0 0 10px #ff4f9a,
        0 0 30px #ff4f9a,
        0 0 70px #ff1d75;
}

.cover p{
    position:relative;
    z-index:3;

    margin-top:12px;
    margin-bottom:30px;

    color:#ffd8e9;

    font-size:clamp(15px,2vw,20px);

    letter-spacing:2px;
}

/* ปุ่ม */
button{
    position:relative;
    z-index:5;

    padding:15px 50px;

    border-radius:100px;

    border:1px solid #ff7bb4;

    background:rgba(255,70,140,.08);

    color:white;

    font-size:18px;
    letter-spacing:3px;

    cursor:pointer;

    box-shadow:
        0 0 15px #ff4f9a,
        inset 0 0 15px rgba(255,80,150,.2);

    transition:.3s;
}

button:hover{
    transform:scale(1.12);

    background:rgba(255,70,140,.25);

    box-shadow:
        0 0 25px #ff4f9a,
        0 0 60px #ff1d75;
}

/* ปุ่มเพลง */
.musicButton{
    position:fixed;

    right:20px;
    top:20px;

    z-index:30;

    width:50px;
    height:50px;

    padding:0;

    border-radius:50%;

    font-size:20px;

    display:flex;
    align-items:center;
    justify-content:center;
}

/* ข้อความ */
.message{
    position:fixed;

    left:50%;
    bottom:30px;

    transform:
        translateX(-50%)
        translateY(30px);

    z-index:10;

    opacity:0;

    color:white;

    font-size:clamp(17px,3vw,26px);

    letter-spacing:2px;

    text-align:center;

    text-shadow:
        0 0 10px #ff4f9a,
        0 0 25px #ff1d75;

    transition:
        opacity 2s ease,
        transform 2s ease;
}

.message.show{
    opacity:1;

    transform:
        translateX(-50%)
        translateY(0);
}
</style>
</head>

<body>

<canvas id="canvas"></canvas>


<!-- =====================
     หน้าปก
===================== -->

<div class="cover" id="cover">

    <!-- เปลี่ยน photo.jpg เป็นชื่อไฟล์รูป -->
    <img
        class="profile"
        src="photo.jpg"
        alt="รูป"
    >

    <!-- เปลี่ยนชื่อคนตรงนี้ -->
    <h1> เฟิส ❤️</h1>

    <p>
        มีบางอย่างอยากให้เห็น...
    </p>

    <button onclick="openHeart()">
        OPEN
    </button>

</div>


<!-- =====================
     เพลง
===================== -->

<audio id="music" loop>
    <source
        src="file:///G:/PUN%20-%20%E0%B8%82%E0%B8%AD%E0%B9%81%E0%B8%84%E0%B9%88%E0%B8%99%E0%B8%B5%E0%B9%89%20(Forever%20n%20ever)%20_%20Official%20Lyric%20Video-converted.mp3"
        type="audio/mpeg"
    >
</audio>


<!-- ปุ่มเปิด/ปิดเพลง -->

<button
    class="musicButton"
    id="musicButton"
    onclick="toggleMusic()"
>
    🎵
</button>


<!-- =====================
     ข้อความ
===================== -->

<div class="message" id="message">
    🌸 Made with love ❤️
</div>


<script>

const canvas =
    document.getElementById("canvas");

const ctx =
    canvas.getContext("2d");

let width;
let height;


/* =====================
   ปรับขนาดจอ
===================== */

function resize(){

    width =
        window.innerWidth;

    height =
        window.innerHeight;

    canvas.width =
        width * devicePixelRatio;

    canvas.height =
        height * devicePixelRatio;

    canvas.style.width =
        width + "px";

    canvas.style.height =
        height + "px";

    ctx.setTransform(
        devicePixelRatio,
        0,
        0,
        devicePixelRatio,
        0,
        0
    );
}

resize();

window.addEventListener(
    "resize",
    resize
);


/* =====================
   รูปหัวใจ
===================== */

function heart(t){

    return{

        x:
            16 *
            Math.pow(
                Math.sin(t),
                3
            ),

        y:
            -(
                13*Math.cos(t)
                -
                5*Math.cos(2*t)
                -
                2*Math.cos(3*t)
                -
                Math.cos(4*t)
            )
    };
}


const points=[];

for(
    let i=0;
    i<720;
    i++
){

    const angle =
        i *
        Math.PI *
        2 /
        720;

    points.push(
        heart(angle)
    );
}


/* =====================
   ดอกไม้
===================== */

const flowers=[];

const flowerColors=[
    "#ff4f9a",
    "#ff82b7",
    "#ffc1dc",
    "#ffffff",
    "#ffd166",
    "#c77dff",
    "#ff8c42"
];


function createFlower(point){

    const scale =
        Math.min(
            width,
            height
        ) / 24;

    flowers.push({

        x:
            width/2 +
            point.x*scale,

        y:
            height/2 +
            point.y*scale,

        size:
            Math.min(
                width,
                height
            ) / 85 *
            (
                Math.random()*.8+.8
            ),

        color:
            flowerColors[
                Math.floor(
                    Math.random() *
                    flowerColors.length
                )
            ],

        rotation:
            Math.random() *
            Math.PI*2,

        growth:0,

        sway:
            Math.random() *
            Math.PI*2
    });
}


function drawFlower(flower){

    const size =
        flower.size *
        flower.growth;

    if(size<=0)return;

    ctx.save();

    ctx.translate(
        flower.x,
        flower.y
    );

    ctx.rotate(
        flower.rotation +
        Math.sin(
            performance.now()*.001 +
            flower.sway
        )*.05
    );

    ctx.shadowBlur =
        size*2;

    ctx.shadowColor =
        flower.color;


    for(
        let i=0;
        i<6;
        i++
    ){

        ctx.rotate(
            Math.PI/3
        );

        ctx.beginPath();

        ctx.ellipse(
            0,
            -size,
            size*.45,
            size,
            0,
            0,
            Math.PI*2
        );

        ctx.fillStyle =
            flower.color;

        ctx.fill();
    }


    ctx.shadowBlur=size;

    ctx.shadowColor="#ffd700";

    ctx.beginPath();

    ctx.arc(
        0,
        0,
        size*.35,
        0,
        Math.PI*2
    );

    ctx.fillStyle="#ffd700";

    ctx.fill();

    ctx.restore();
}


/* =====================
   ดาว
===================== */

const stars=[];

for(
    let i=0;
    i<220;
    i++
){

    stars.push({

        x:
            Math.random()*width,

        y:
            Math.random()*height,

        size:
            Math.random()*2.5+.3,

        alpha:
            Math.random(),

        speed:
            Math.random()*.015+.003
    });
}


function drawStars(){

    for(
        const star of stars
    ){

        star.alpha +=
            star.speed;

        if(
            star.alpha>1 ||
            star.alpha<0
        ){

            star.speed*=-1;
        }

        ctx.beginPath();

        ctx.arc(
            star.x,
            star.y,
            star.size,
            0,
            Math.PI*2
        );

        ctx.fillStyle =
            `rgba(255,190,220,${star.alpha})`;

        ctx.fill();
    }
}


/* =====================
   อนุภาค
===================== */

const particles=[];

for(
    let i=0;
    i<100;
    i++
){

    particles.push({

        x:
            Math.random()*width,

        y:
            height+
            Math.random()*height,

        size:
            Math.random()*3+1,

        speed:
            Math.random()*.5+.2,

        alpha:
            Math.random()
    });
}


function drawParticles(){

    for(
        const p of particles
    ){

        p.y-=p.speed;

        if(
            p.y<-20
        ){

            p.y=height+20;

            p.x=
                Math.random()*width;
        }

        ctx.beginPath();

        ctx.arc(
            p.x,
            p.y,
            p.size,
            0,
            Math.PI*2
        );

        ctx.fillStyle =
            `rgba(255,120,190,${p.alpha})`;

        ctx.shadowBlur=10;

        ctx.shadowColor="#ff4f9a";

        ctx.fill();
    }
}


/* =====================
   กลีบดอกไม้
===================== */

const petals=[];

for(
    let i=0;
    i<35;
    i++
){

    petals.push({

        x:
            Math.random()*width,

        y:
            Math.random()*height,

        size:
            Math.random()*5+3,

        speed:
            Math.random()*.8+.3,

        rotation:
            Math.random()*Math.PI,

        rotateSpeed:
            Math.random()*.03-.015
    });
}


function drawPetals(){

    for(
        const p of petals
    ){

        p.y+=p.speed;

        p.rotation+=
            p.rotateSpeed;

        p.x+=
            Math.sin(
                p.y*.01
            )*.5;


        if(
            p.y>height+20
        ){

            p.y=-20;

            p.x=
                Math.random()*width;
        }


        ctx.save();

        ctx.translate(
            p.x,
            p.y
        );

        ctx.rotate(
            p.rotation
        );

        ctx.beginPath();

        ctx.ellipse(
            0,
            0,
            p.size,
            p.size*.5,
            0,
            0,
            Math.PI*2
        );

        ctx.fillStyle =
            "rgba(255,120,180,.65)";

        ctx.shadowBlur=8;

        ctx.shadowColor="#ff4f9a";

        ctx.fill();

        ctx.restore();
    }
}


/* =====================
   วาดหัวใจ
===================== */

function drawHeart(){

    const scale =
        Math.min(
            width,
            height
        ) / 24;

    ctx.save();

    ctx.translate(
        width/2,
        height/2
    );


    for(
        let glow=0;
        glow<3;
        glow++
    ){

        ctx.beginPath();


        for(
            let i=0;
            i<points.length;
            i++
        ){

            const p =
                points[i];

            const x =
                p.x*scale;

            const y =
                p.y*scale;


            if(i===0)
                ctx.moveTo(x,y);
            else
                ctx.lineTo(x,y);
        }


        ctx.closePath();

        ctx.strokeStyle =
            glow===0
            ? "#ff3d86"
            : "rgba(255,70,150,.25)";

        ctx.lineWidth =
            glow===0
            ? 3
            : 12+glow*8;

        ctx.shadowBlur =
            25+glow*20;

        ctx.shadowColor =
            "#ff287b";

        ctx.stroke();
    }

    ctx.restore();
}


/* =====================
   ประกายรอบหัวใจ
===================== */

function drawSparks(){

    if(!started)return;

    const scale =
        Math.min(
            width,
            height
        ) / 24;

    const time =
        performance.now()*.001;


    for(
        let i=0;
        i<12;
        i++
    ){

        const index =
            Math.floor(
                (
                    time*100+
                    i*60
                ) %
                points.length
            );

        const p =
            points[index];


        const x =
            width/2+
            p.x*scale;

        const y =
            height/2+
            p.y*scale;


        ctx.beginPath();

        ctx.arc(
            x,
            y,
            2.5,
            0,
            Math.PI*2
        );

        ctx.fillStyle="#ffffff";

        ctx.shadowBlur=20;

        ctx.shadowColor="#ff6fae";

        ctx.fill();
    }
}


/* =====================
   ANIMATION
===================== */

let started=false;

let flowerIndex=0;


function animate(){

    ctx.clearRect(
        0,
        0,
        width,
        height
    );

    drawStars();

    drawParticles();

    drawPetals();


    if(started){

        drawHeart();

        drawSparks();


        if(
            flowerIndex<
            points.length
        ){

            for(
                let i=0;
                i<5;
                i++
            ){

                if(
                    flowerIndex<
                    points.length
                ){

                    createFlower(
                        points[
                            flowerIndex
                        ]
                    );

                    flowerIndex+=2;
                }
            }
        }


        for(
            const flower of flowers
        ){

            if(
                flower.growth<1
            ){

                flower.growth+=.035;
            }

            drawFlower(
                flower
            );
        }
    }


    requestAnimationFrame(
        animate
    );
}


/* =====================
   OPEN + MUSIC
===================== */

function openHeart(){

    started=true;


    document
        .getElementById("cover")
        .classList
        .add("hide");


    const music =
        document.getElementById("music");


    music.play()
        .catch(()=>{
            console.log(
                "กดปุ่ม 🎵 เพื่อเล่นเพลง"
            );
        });


    setTimeout(()=>{

        document
            .getElementById("message")
            .classList
            .add("show");

    },3500);
}


/* =====================
   ปุ่มเพลง
===================== */

function toggleMusic(){

    const music =
        document.getElementById("music");

    const button =
        document.getElementById(
            "musicButton"
        );


    if(music.paused){

        music.play();

        button.textContent="🔊";

    }else{

        music.pause();

        button.textContent="🎵";
    }
}


animate();

</script>

</body>
</html>
```
