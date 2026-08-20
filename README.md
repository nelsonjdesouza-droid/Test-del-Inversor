<!DOCTYPE html>
<html lang="es-AR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Test del inversor · de Souza Finanzas</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@500;600;700&family=Roboto:ital,wght@0,400;0,500;0,700;1,400&display=swap" rel="stylesheet">
<style>
:root{
  --verde:#0E7A4D; --verde-osc:#0A5C3A; --menta:#D8EFE3; --menta-suave:#F1F9F6;
  --tinta:#1A1A1A; --pill:#ECECEC; --pill-hover:#E2E2E2; --gris:#7C7C7C;
  --linea:#E6E6E6; --blanco:#fff;
  --display:'Oswald','Arial Narrow','Helvetica Neue Condensed',Impact,sans-serif;
  --texto:'Roboto',-apple-system,BlinkMacSystemFont,'Segoe UI',Arial,sans-serif;
}
*{box-sizing:border-box}
html,body{margin:0;padding:0}
body{background:var(--blanco);color:var(--tinta);font-family:var(--texto);
  -webkit-font-smoothing:antialiased;min-height:100vh}
.wrap{max-width:860px;margin:0 auto;padding:0 24px 64px;min-height:100vh;display:flex;flex-direction:column}

.top{position:sticky;top:0;background:var(--blanco);padding:20px 0 14px;z-index:20}
.barra{height:3px;background:var(--linea);border-radius:2px;overflow:hidden}
.barra span{display:block;height:100%;width:0;background:var(--verde);transition:width .35s cubic-bezier(.4,0,.2,1)}
.contador{margin-top:8px;font-family:var(--display);font-size:11px;font-weight:600;
  letter-spacing:.16em;text-transform:uppercase;color:var(--gris)}

.eyebrow{display:flex;align-items:center;gap:12px;margin-bottom:14px;font-family:var(--display);
  font-size:12px;font-weight:600;letter-spacing:.18em;text-transform:uppercase;color:var(--verde)}
.eyebrow::before{content:"";width:26px;height:2px;background:var(--verde);flex:none}
h1.pregunta{font-family:var(--display);font-weight:700;text-transform:uppercase;
  font-size:clamp(26px,4.6vw,40px);line-height:1.06;margin:0 0 12px;color:var(--tinta)}
.ayuda{font-style:italic;color:var(--gris);font-size:15px;line-height:1.45;margin:0 0 26px}
.multi-badge{display:inline-block;background:var(--menta);color:var(--verde-osc);
  font-family:var(--display);font-size:11px;font-weight:600;letter-spacing:.14em;
  text-transform:uppercase;padding:7px 14px;border-radius:999px;margin:0 0 18px}

.opciones{display:flex;flex-direction:column;gap:10px;margin:0;padding:0;list-style:none}
.op{display:flex;align-items:center;gap:16px;width:100%;text-align:left;cursor:pointer;
  background:var(--pill);border:2px solid transparent;border-radius:12px;padding:18px 22px;
  font-family:var(--texto);font-size:15.5px;font-weight:500;color:#2B2B2B;line-height:1.35;
  transition:background .16s,border-color .16s,transform .16s}
.op:hover{background:var(--pill-hover)}
.op:active{transform:scale(.995)}
.op:focus-visible{outline:3px solid var(--verde);outline-offset:3px}
.marca{flex:none;width:21px;height:21px;border:2px solid #B4B4B4;background:var(--blanco);
  display:grid;place-items:center;transition:border-color .16s}
.marca.radio{border-radius:50%} .marca.check{border-radius:6px}
.marca i{display:block;width:11px;height:11px;background:var(--verde);transform:scale(0);
  transition:transform .16s cubic-bezier(.34,1.56,.64,1)}
.marca.radio i{border-radius:50%} .marca.check i{border-radius:3px}
.op.on{background:var(--blanco);border-color:var(--verde);font-weight:700}
.op.on .marca{border-color:var(--verde)} .op.on .marca i{transform:scale(1)}

.nav{display:flex;align-items:center;justify-content:space-between;gap:16px;margin-top:34px;
  padding-top:24px;border-top:1px solid var(--linea);flex-wrap:wrap}
.btn-atras{font-family:var(--display);font-size:13px;font-weight:600;letter-spacing:.14em;
  text-transform:uppercase;color:var(--tinta);background:transparent;border:1.5px solid var(--tinta);
  border-radius:999px;padding:13px 26px;cursor:pointer;transition:background .16s,color .16s}
.btn-atras:hover{background:var(--tinta);color:var(--blanco)}
.btn-atras:disabled{opacity:.28;cursor:not-allowed}
.btn-atras:disabled:hover{background:transparent;color:var(--tinta)}
.btn-sig{font-family:var(--display);font-size:14px;font-weight:600;letter-spacing:.14em;
  text-transform:uppercase;color:var(--verde);background:transparent;border:0;padding:13px 4px;
  cursor:pointer;transition:opacity .16s,transform .16s}
.btn-sig:hover{transform:translateX(3px)}
.btn-sig[data-listo="no"]{color:var(--gris);cursor:default;pointer-events:none}
.btn-atras:focus-visible,.btn-sig:focus-visible{outline:3px solid var(--verde);outline-offset:3px}

.aviso{background:var(--menta-suave);border-left:4px solid #4BB89A;border-radius:8px;
  padding:18px 22px;margin:0 0 30px;font-size:14.5px;line-height:1.55;color:#33413D}
.aviso b{color:var(--verde)}

.intro{padding:56px 0 20px}
.marca-dss{font-family:var(--display);font-size:12px;font-weight:600;letter-spacing:.22em;
  text-transform:uppercase;color:var(--verde);margin:0 0 26px}
.intro h1{font-family:var(--display);font-weight:700;text-transform:uppercase;
  font-size:clamp(38px,8vw,68px);line-height:.95;margin:0 0 20px}
.intro p{font-size:17px;line-height:1.6;color:#4A4A4A;max-width:52ch;margin:0 0 14px}
.metajson{font-family:var(--display);font-size:12px;letter-spacing:.16em;text-transform:uppercase;
  color:var(--gris);font-weight:600;margin:26px 0 34px}
.cta{font-family:var(--display);font-size:15px;font-weight:600;letter-spacing:.14em;
  text-transform:uppercase;background:var(--verde);color:var(--blanco);border:0;border-radius:999px;
  padding:17px 40px;cursor:pointer;transition:background .16s,transform .16s}
.cta:hover{background:var(--verde-osc);transform:translateY(-1px)}
.cta:focus-visible{outline:3px solid var(--tinta);outline-offset:3px}

/* formulario de contacto */
.campos{display:flex;flex-direction:column;gap:18px;max-width:520px}
.campo label{display:block;font-family:var(--display);font-size:12px;font-weight:600;
  letter-spacing:.13em;text-transform:uppercase;color:#3A3A3A;margin-bottom:8px}
.campo label .opt{color:var(--gris);font-weight:500}
.campo input[type=text],.campo input[type=email],.campo input[type=tel]{
  width:100%;background:var(--pill);border:2px solid transparent;border-radius:12px;
  padding:16px 18px;font-family:var(--texto);font-size:15.5px;color:var(--tinta);transition:.16s}
.campo input:focus{outline:0;background:var(--blanco);border-color:var(--verde)}
.campo input:focus-visible{outline:3px solid var(--verde);outline-offset:3px}
.campo .err{display:none;color:#C0392B;font-size:13px;margin-top:7px}
.campo.mal input{border-color:#C0392B}
.campo.mal .err{display:block}
.consent{display:flex;gap:14px;align-items:flex-start;background:var(--pill);border:2px solid transparent;
  border-radius:12px;padding:17px 20px;cursor:pointer;font-size:14.5px;line-height:1.5;color:#3A3A3A;
  transition:.16s;max-width:520px}
.consent:hover{background:var(--pill-hover)}
.consent.on{background:var(--blanco);border-color:var(--verde)}
.consent .marca{margin-top:1px}

.res-eyebrow{margin-bottom:10px}
.perfil-nombre{font-family:var(--display);font-weight:700;text-transform:uppercase;
  font-size:clamp(34px,7.2vw,62px);line-height:.98;margin:0 0 6px}
.perfil-score{font-family:var(--display);font-size:14px;font-weight:600;letter-spacing:.16em;
  text-transform:uppercase;color:var(--gris);margin:0 0 32px}
.perfil-score b{color:var(--verde);font-size:18px}

.escala{display:flex;gap:3px}
.tramo{flex:1;height:52px;background:var(--pill);border-radius:4px;transition:background .3s}
.tramo.activo{background:var(--verde)} .tramo.previo{background:var(--menta)}
.escala-lab{display:flex;gap:3px;margin-top:9px}
.escala-lab span{flex:1;font-family:var(--display);font-size:9.5px;font-weight:600;letter-spacing:.08em;
  text-transform:uppercase;color:var(--gris);line-height:1.25;text-align:center}
.escala-lab span.activo{color:var(--verde)}
.escala-wrap{position:relative;padding:12px 0}
.aguja{position:absolute;top:2px;bottom:2px;width:2px;background:var(--tinta);border-radius:2px;
  transition:left .5s cubic-bezier(.4,0,.2,1)}

/* tarjeta de cartera: la firma del resultado */
.cartera{margin:38px 0 0;border:2px solid var(--tinta);border-radius:16px;overflow:hidden}
.cartera-top{background:var(--tinta);color:var(--blanco);padding:16px 24px;font-family:var(--display);
  font-size:12px;font-weight:600;letter-spacing:.18em;text-transform:uppercase}
.cartera-cuerpo{padding:26px 24px 24px}
.cartera-nombre{font-family:var(--display);font-weight:700;text-transform:uppercase;
  font-size:clamp(26px,5vw,38px);line-height:1;margin:0 0 6px}
.cartera-sat{font-size:14.5px;color:#4A4A4A;margin:0 0 20px}
.cartera-sat b{color:var(--verde-osc)}
table.mix{width:100%;border-collapse:collapse;font-size:15px}
table.mix td{padding:12px 0;border-bottom:1px solid var(--linea)}
table.mix tr:last-child td{border-bottom:0}
table.mix td:first-child{color:#4A4A4A}
table.mix td:last-child{text-align:right;font-family:var(--display);font-weight:600;font-size:16px;
  color:var(--tinta);white-space:nowrap}

.tope{background:#FFF7E8;border-left:4px solid #E0A32E;border-radius:8px;padding:16px 20px;
  margin:26px 0 0;font-size:14.5px;line-height:1.55;color:#4A3A18}
h2.sub{font-family:var(--display);font-weight:600;text-transform:uppercase;font-size:14px;
  letter-spacing:.16em;color:var(--verde);margin:46px 0 16px;display:flex;align-items:center;gap:12px}
h2.sub::before{content:"";width:26px;height:2px;background:var(--verde);flex:none}
.dims{display:flex;flex-direction:column;gap:16px}
.dim{display:grid;grid-template-columns:132px 1fr 52px;gap:14px;align-items:center}
.dim-lab{font-family:var(--display);font-size:12.5px;font-weight:600;letter-spacing:.1em;
  text-transform:uppercase;color:#3A3A3A}
.dim-bar{height:9px;background:var(--pill);border-radius:5px;overflow:hidden}
.dim-bar span{display:block;height:100%;background:var(--verde);width:0;border-radius:5px;
  transition:width .7s cubic-bezier(.4,0,.2,1)}
.dim-val{font-family:var(--display);font-size:13px;font-weight:600;color:var(--gris);text-align:right}
.lectura{font-size:16px;line-height:1.65;color:#333;max-width:62ch}
.chips{display:flex;flex-wrap:wrap;gap:8px}
.chip{background:var(--menta);color:var(--verde-osc);border-radius:999px;padding:8px 15px;font-size:13.5px;font-weight:500}
.chip.gris{background:var(--pill);color:#4A4A4A}
.dato{display:flex;justify-content:space-between;gap:20px;padding:13px 0;border-bottom:1px solid var(--linea);
  font-size:15px;flex-wrap:wrap}
.dato span:first-child{color:var(--gris)}
.dato span:last-child{font-weight:500;text-align:right}
.acciones{display:flex;gap:12px;flex-wrap:wrap;margin-top:44px}
.btn-sec{font-family:var(--display);font-size:13px;font-weight:600;letter-spacing:.13em;text-transform:uppercase;
  background:transparent;border:1.5px solid var(--tinta);color:var(--tinta);border-radius:999px;
  padding:14px 26px;cursor:pointer;transition:background .16s,color .16s}
.btn-sec:hover{background:var(--tinta);color:var(--blanco)}
.btn-sec:focus-visible{outline:3px solid var(--verde);outline-offset:3px}
#copia{width:100%;margin-top:16px;min-height:190px;font-family:ui-monospace,Menlo,Consolas,monospace;
  font-size:12.5px;padding:14px;border:1px solid var(--linea);border-radius:8px;display:none;resize:vertical}
.legal{margin-top:52px;padding-top:22px;border-top:1px solid var(--linea);font-size:12.5px;
  line-height:1.6;color:#9A9A9A;max-width:70ch}
.escena{animation:entra .3s ease both}
@keyframes entra{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
@media (prefers-reduced-motion:reduce){*{animation-duration:.01ms !important;transition-duration:.01ms !important}}
@media (max-width:560px){
  .wrap{padding:0 18px 48px}
  .op{padding:16px 17px;font-size:14.5px;gap:13px}
  .dim{grid-template-columns:1fr;gap:6px} .dim-val{text-align:left}
  .escala-lab span{font-size:8px} .tramo{height:44px}
  .cartera-cuerpo{padding:22px 18px}
}
</style>
</head>
<body>
<div class="wrap">
  <div class="top" id="top" hidden>
    <div class="barra"><span id="barra"></span></div>
    <div class="contador" id="contador"></div>
  </div>
  <main id="escena" class="escena"></main>
</div>

<script>
/* =========================================================================
   CONFIGURACIÓN
   ========================================================================= */
const MARCA = "de Souza Finanzas";
const CANAL_TG = "dSs · Información de Mercado";
const CONTACTO_AL_INICIO = false;   // true = pide datos antes de las preguntas

/* =========================================================================
   PUNTAJES — editá los `p` para recalibrar. tope = techo de perfil (0..4)
   ========================================================================= */
const PERFILES = ["Conservador","Moderadamente conservador","Moderado","Moderadamente agresivo","Agresivo"];

const PREGUNTAS = [
  { bloque:"Bloque A · Perfil de riesgo", dim:"riesgo", peso:1, tipo:"single",
    titulo:"¿En qué etapa de tu vida estás?",
    ayuda:"Esto nos ayuda a entender tu horizonte natural de inversión.",
    ops:[
      {t:"Menos de 30 años, recién empiezo a invertir", p:5},
      {t:"Entre 30 y 45 años, en pleno crecimiento patrimonial", p:4},
      {t:"Entre 45 y 55 años, consolidando patrimonio", p:3},
      {t:"Entre 55 y 65 años, pensando en la transición al retiro", p:2},
      {t:"Más de 65 años, priorizo preservar lo construido", p:1}]},

  { bloque:"Bloque A · Perfil de riesgo", dim:"riesgo", peso:1, tipo:"single",
    titulo:"¿Cuál es tu horizonte de inversión?",
    ayuda:"El plazo durante el cual no necesitarías tocar este dinero.",
    ops:[
      {t:"Más de 10 años", p:5},
      {t:"Entre 5 y 10 años", p:4},
      {t:"Entre 3 y 5 años", p:3},
      {t:"Entre 1 y 3 años", p:2, tope:2},
      {t:"Menos de 1 año", p:1, tope:0}]},

  { bloque:"Bloque A · Perfil de riesgo", dim:"riesgo", peso:2, tipo:"single",
    titulo:"Si tu cartera cae 25% en 6 meses ¿qué hacés en los siguientes 60 días?",
    ayuda:"La tolerancia real al riesgo se ve en las caídas, no en las subas.",
    ops:[
      {t:"Doblo apuesta: aporto más del 20% adicional", p:6},
      {t:"Aporto un 10% extra a precios bajos", p:5},
      {t:"Rebalanceo hacia sectores menos volátiles", p:3},
      {t:"Mantengo sin tocar nada", p:4},
      {t:"Reduzco entre 30% y 50% para limitar el daño", p:2},
      {t:"Salgo casi todo, no me lo banco", p:1, tope:1}]},

  { bloque:"Bloque A · Perfil de riesgo", dim:"riesgo", peso:1, tipo:"single",
    titulo:"¿Qué % de tu patrimonio total (incluyendo inmueble familiar, auto y ahorros en USD físicos) tenés en activos de riesgo?",
    ayuda:"Activos de riesgo = acciones, CEDEARs, cripto, ETFs equity. NO incluye plazo fijo, bonos en USD ni FCI money market.",
    ops:[
      {t:"Más del 70%", p:6},{t:"Entre 50% y 70%", p:5},{t:"Entre 30% y 50%", p:4},
      {t:"Entre 15% y 30%", p:3},{t:"Entre 5% y 15%", p:2},{t:"Menos del 5%", p:1}]},

  { bloque:"Bloque B · Conocimiento y experiencia", dim:"conoc", peso:2, tipo:"single",
    titulo:"¿Cómo describirías tu nivel de conocimiento financiero?",
    ayuda:"Sé honesto. Los criterios son específicos a propósito.",
    ops:[
      {t:"Experto: armo cartera diversificada, leo balances, uso PER/EV/EBITDA, entiendo opciones y derivados", p:5},
      {t:"Avanzado: conozco bonos, ONs, CEDEARs, ETFs y armé estrategias propias con tesis", p:4},
      {t:"Intermedio: opero hace tiempo en lo básico (acciones, FCI, plazo fijo) pero me falta profundidad", p:3},
      {t:"Básico: invierto algo pero sigo recomendaciones de otros, no analizo los activos yo", p:2, tope:2},
      {t:"Inicial: estoy empezando a aprender", p:1, tope:1}]},

  { bloque:"Bloque B · Conocimiento y experiencia", dim:"conoc", peso:1, tipo:"multi", tope_score:10,
    titulo:"¿Con qué instrumentos ya operaste o invertiste?",
    ayuda:"Sumá los que correspondan. El score se topea en 10.",
    ops:[
      {t:"Plazo Fijo / Fondos Comunes", p:1},
      {t:"Bonos / Obligaciones Negociables", p:2},
      {t:"CEDEARs / Acciones argentinas", p:3},
      {t:"Cripto / Opciones y derivados", p:4},
      {t:"Ninguno todavía", p:0, excluyente:true, tope:1}]},

  { bloque:"Bloque C · Objetivos y preferencias", dim:"objet", peso:1, tipo:"single",
    titulo:"¿Cuál es tu principal objetivo al invertir?",
    ops:[
      {t:"Maximizar crecimiento, aunque implique más volatilidad", p:5},
      {t:"Hacer crecer mi patrimonio con riesgo controlado", p:4},
      {t:"Generar una renta periódica", p:3},
      {t:"Proteger mi capital de la inflación", p:2},
      {t:"Preservar lo que ya tengo, prioridad cero riesgo", p:1, tope:1}]},

  { bloque:"Bloque C · Objetivos y preferencias", dim:"objet", peso:1, tipo:"single",
    titulo:"¿En qué moneda preferís invertir?",
    ayuda:"En Argentina, dolarizar todo es preservar; tomar pesos por tasa real es apetito de riesgo.",
    ops:[
      {t:"100% dólares o activos dolarizados", p:1},
      {t:"Mayormente dólares, algo en pesos", p:2},
      {t:"Mix equilibrado pesos/dólares", p:3},
      {t:"Mayormente pesos, buscando tasa local", p:5},
      {t:"No tengo preferencia, busco el mejor rendimiento donde sea", p:4}]},

  { bloque:"Bloque D · Segmentación", dim:null, tipo:"multi", opcional:true,
    titulo:"¿Qué temáticas te interesan más para recibir análisis?",
    ayuda:"Sin puntaje. Nos ayuda a segmentar el contenido que te enviamos.",
    ops:[
      {t:"Renta fija en dólares: ONs y soberanos"},
      {t:"CEDEARs y acciones de EEUU"},
      {t:"Renta variable argentina"},
      {t:"Crypto y activos digitales"},
      {t:"Inteligencia artificial y tecnología"},
      {t:"Energía y commodities"},
      {t:"Planificación patrimonial y fiscal"},
      {t:"Educación financiera en general"}]},

  { bloque:"Bloque D · Segmentación", dim:null, tipo:"single",
    titulo:"¿Operás actualmente con algún broker?",
    ayuda:"Sin puntaje. Nos ayuda a entender desde dónde partís.",
    ops:[
      {t:"Sí, opero por mi cuenta y busco una segunda opinión"},
      {t:"Sí, pero quiero acompañamiento para ordenar la cartera"},
      {t:"No tengo cuenta comitente todavía"},
      {t:"NS / NC"}]},

  { bloque:"Bloque E · Contenido dSs", dim:null, tipo:"single",
    aviso:'🔔 Si ya sos cliente de <b>de Souza Finanzas</b>, podés responder estas preguntas para recibir el <b>Radar Semanal y las alertas del Update de Estrategia</b> filtradas por tu perfil y por los activos que más te interesan. Si todavía no sos cliente, podés saltearlas y conocer tu perfil igual.',
    titulo:"¿Estás en el canal de Telegram dSs?",
    ops:[{t:"Sí"},{t:"No"},{t:"No, pero me gustaría sumarme"}]},

  { bloque:"Bloque E · Contenido dSs", dim:null, tipo:"multi", opcional:true,
    titulo:"Marcá las secciones del Update de Estrategia que querés recibir",
    ayuda:"Solo recibirás avisos de las secciones que marques acá.",
    ops:[
      {t:"Estrategia en pesos: tasa y cobertura"},
      {t:"Hard dollar y soberanos"},
      {t:"Obligaciones Negociables"},
      {t:"Renta variable local"},
      {t:"Renta variable internacional y CEDEARs"},
      {t:"Posicionamiento táctico y oportunidades coyunturales"}]}
];

/* Mapeo perfil → cartera modelo dSs.
   Los rangos son placeholders: reemplazalos por los pesos reales de cada cartera. */
const CARTERAS = [
  { nombre:"Cartera Conservadora", genesis:null,
    txt:"Priorizás no perder por encima de ganar. El portafolio debería estar dominado por instrumentos de baja volatilidad y liquidez alta, con la renta variable como pincelada y no como cuerpo de la cartera.",
    mix:[["Liquidez y money market","20 – 35%"],["Renta fija corta: ONs y soberanos cortos","55 – 70%"],["CEDEARs y renta variable","0 – 10%"]] },
  { nombre:"Cartera Conservadora", genesis:null, nota:"con rampa gradual hacia Moderada",
    txt:"Tolerás algo de volatilidad si el piso está protegido. El grueso sigue en renta fija, pero ya hay lugar para un componente de equity que sostenga el rendimiento real en el largo plazo.",
    mix:[["Liquidez y money market","10 – 20%"],["Renta fija: ONs y soberanos","55 – 70%"],["CEDEARs y renta variable","15 – 25%"]] },
  { nombre:"Cartera Moderada", genesis:null,
    txt:"Buscás crecimiento real sin exponerte a caídas que te saquen del plan. El equilibrio entre renta fija y variable es tu terreno natural: acá la diversificación hace más trabajo que la selección de activos.",
    mix:[["Liquidez y money market","5 – 15%"],["Renta fija: ONs y soberanos","35 – 50%"],["CEDEARs y renta variable","35 – 50%"]] },
  { nombre:"Cartera Arriesgada", genesis:"hasta 5%",
    txt:"Tu foco es la apreciación del capital y aguantás caídas fuertes sin desarmar posiciones. La renta fija pasa a ser amortiguador y reserva para comprar en las bajas, no el motor del retorno.",
    mix:[["Liquidez y money market","5 – 10%"],["Renta fija: ONs y soberanos","15 – 30%"],["CEDEARs y renta variable","55 – 70%"]] },
  { nombre:"Cartera Muy Arriesgada", genesis:"hasta 10%",
    txt:"Maximizás retorno esperado y convivís con volatilidad alta y períodos largos en rojo. Acá el riesgo principal deja de ser el mercado y pasa a ser el dimensionamiento: sin reglas de sizing, el perfil se vuelve inmanejable.",
    mix:[["Liquidez y money market","0 – 5%"],["Renta fija: ONs y soberanos","5 – 15%"],["CEDEARs y renta variable","65 – 80%"]] }
];

const RANGOS = { riesgo:[5,28], conoc:[2,20], objet:[2,10] };
const BANDAS = [25,45,63,80];

/* ========================= estado ========================= */
const PASOS = [];
if (CONTACTO_AL_INICIO) PASOS.push({tipo:"contacto"});
PREGUNTAS.forEach((q,n)=>PASOS.push({tipo:"pregunta",n}));
if (!CONTACTO_AL_INICIO) PASOS.push({tipo:"contacto"});

let p = 0;
const R = PREGUNTAS.map(q => q.tipo === "multi" ? [] : null);
const C = { nombre:"", email:"", tel:"", consent:false };
const $ = s => document.querySelector(s);
const esc = s => String(s??"").replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));
const emailOk = v => /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/.test(v.trim());

function calcular(){
  const bruto = {riesgo:0,conoc:0,objet:0};
  let topeMax = 4, motivos = [];
  PREGUNTAS.forEach((q,n)=>{
    if(!q.dim) return;
    if(q.tipo==="single"){
      const o=q.ops[R[n]]; if(!o) return;
      bruto[q.dim]+=(o.p||0)*(q.peso||1);
      if(o.tope!==undefined&&o.tope<topeMax){topeMax=o.tope;motivos.push(o.t)}
    }else{
      let s=0;
      R[n].forEach(k=>{const o=q.ops[k];s+=(o.p||0);
        if(o.tope!==undefined&&o.tope<topeMax){topeMax=o.tope;motivos.push(o.t)}});
      if(q.tope_score) s=Math.min(s,q.tope_score);
      bruto[q.dim]+=s*(q.peso||1);
    }
  });
  const pct=d=>{const[lo,hi]=RANGOS[d];return Math.round(((bruto[d]-lo)/(hi-lo))*100)};
  const tMin=RANGOS.riesgo[0]+RANGOS.conoc[0]+RANGOS.objet[0];
  const tMax=RANGOS.riesgo[1]+RANGOS.conoc[1]+RANGOS.objet[1];
  const total=bruto.riesgo+bruto.conoc+bruto.objet;
  const score=Math.round(((total-tMin)/(tMax-tMin))*100);
  let nivel=0; BANDAS.forEach(b=>{if(score>=b)nivel++});
  const nf=Math.min(nivel,topeMax);
  return {score,nivel:nf,nivelBruto:nivel,limitado:nf<nivel,motivos,
          dims:{riesgo:pct("riesgo"),conoc:pct("conoc"),objet:pct("objet")}};
}

/* ========================= vistas ========================= */
function inicio(){
  $("#top").hidden = true;
  $("#escena").dataset.vista = "inicio";
  $("#escena").innerHTML = `
    <div class="intro">
      <div class="marca-dss">${esc(MARCA)}</div>
      <h1>Test del<br>inversor</h1>
      <p>Doce preguntas para ubicar tu tolerancia al riesgo, tu conocimiento real de los instrumentos y el objetivo que perseguís con tu capital.</p>
      <p>Al final vas a ver tu perfil y cuál de las carteras modelo de ${esc(MARCA)} le corresponde. No hay respuestas buenas ni malas: la única forma de que el resultado sirva es contestar lo que realmente harías, no lo que te gustaría hacer.</p>
      <div class="metajson">12 preguntas · 3 minutos · resultado inmediato</div>
      <button class="cta" id="empezar">Empezar el test →</button>
    </div>`;
  $("#empezar").onclick = () => { p = 0; pintar(); };
}

function pintar(){
  $("#top").hidden = false;
  $("#barra").style.width = (p / PASOS.length * 100) + "%";
  const paso = PASOS[p];
  $("#escena").dataset.vista = paso.tipo;
  if (paso.tipo === "contacto"){ $("#contador").textContent = "Datos de contacto"; pintarContacto(); }
  else { $("#contador").textContent = `Pregunta ${paso.n + 1} de ${PREGUNTAS.length}`; pintarPregunta(paso.n); }
  window.scrollTo({top:0,behavior:"instant"});
}

function pintarPregunta(n){
  const q = PREGUNTAS[n], multi = q.tipo === "multi";
  const marcado = k => multi ? R[n].includes(k) : R[n] === k;
  $("#escena").innerHTML = `
    ${q.aviso ? `<div class="aviso">${q.aviso}</div>` : ""}
    <div class="eyebrow">${esc(q.bloque)}</div>
    <h1 class="pregunta">${esc(q.titulo)}</h1>
    ${q.ayuda ? `<p class="ayuda">${esc(q.ayuda)}</p>` : ""}
    ${multi ? `<div class="multi-badge">Podés marcar varias opciones</div>` : ""}
    <div class="opciones" role="${multi?"group":"radiogroup"}" aria-label="${esc(q.titulo)}">
      ${q.ops.map((o,k)=>`
        <button type="button" class="op ${marcado(k)?"on":""}" data-k="${k}"
          role="${multi?"checkbox":"radio"}" aria-checked="${marcado(k)}">
          <span class="marca ${multi?"check":"radio"}"><i></i></span>
          <span>${esc(o.t)}</span></button>`).join("")}
    </div>
    ${navHTML()}`;
  document.querySelectorAll(".op").forEach(b => b.onclick = () => elegir(n, +b.dataset.k));
  enganchaNav();
}

function pintarContacto(){
  const ultimo = p === PASOS.length - 1;
  $("#escena").innerHTML = `
    <div class="eyebrow">Casi listo</div>
    <h1 class="pregunta">${ultimo ? "¿A dónde te mandamos el resultado?" : "Empecemos por tus datos"}</h1>
    <p class="ayuda">Usamos tus datos para enviarte el informe de perfil y el contenido de mercado. No los compartimos con terceros.</p>
    <div class="campos">
      <div class="campo" id="c-nombre">
        <label for="f-nombre">Nombre y apellido</label>
        <input type="text" id="f-nombre" autocomplete="name" value="${esc(C.nombre)}" placeholder="Cómo te llamás">
        <div class="err">Escribí tu nombre para poder identificar el informe.</div>
      </div>
      <div class="campo" id="c-email">
        <label for="f-email">Email</label>
        <input type="email" id="f-email" autocomplete="email" value="${esc(C.email)}" placeholder="tunombre@correo.com">
        <div class="err">Revisá el email: falta el @ o el dominio.</div>
      </div>
      <div class="campo" id="c-tel">
        <label for="f-tel">WhatsApp <span class="opt">— opcional</span></label>
        <input type="tel" id="f-tel" autocomplete="tel" value="${esc(C.tel)}" placeholder="11 5555 5555">
      </div>
      <button type="button" class="consent ${C.consent?"on":""}" id="f-consent" role="checkbox" aria-checked="${C.consent}">
        <span class="marca check"><i></i></span>
        <span>Acepto que ${esc(MARCA)} me contacte y me envíe contenido de mercado. Puedo darme de baja cuando quiera.</span>
      </button>
    </div>
    ${navHTML()}`;

  const sync = () => {
    C.nombre = $("#f-nombre").value;
    C.email  = $("#f-email").value;
    C.tel    = $("#f-tel").value;
    $("#c-nombre").classList.toggle("mal", C.nombre.trim() !== "" && C.nombre.trim().length < 2);
    $("#c-email").classList.toggle("mal", C.email.trim() !== "" && !emailOk(C.email));
    estadoSig();
  };
  ["f-nombre","f-email","f-tel"].forEach(id => $("#"+id).addEventListener("input", sync));
  $("#f-consent").onclick = () => {
    C.consent = !C.consent;
    $("#f-consent").classList.toggle("on", C.consent);
    $("#f-consent").setAttribute("aria-checked", C.consent);
    estadoSig();
  };
  enganchaNav();
}

function navHTML(){
  return `<div class="nav">
    <button class="btn-atras" id="atras" ${p===0?"disabled":""}>← Anterior</button>
    <button class="btn-sig" id="sig"></button></div>`;
}
function enganchaNav(){
  $("#atras").onclick = () => { if (p > 0){ p--; pintar(); } };
  $("#sig").onclick = avanzar;
  estadoSig();
}

function elegir(n, k){
  const q = PREGUNTAS[n];
  if (q.tipo === "multi"){
    if (q.ops[k].excluyente){ R[n] = R[n].includes(k) ? [] : [k]; }
    else {
      R[n] = R[n].filter(x => !q.ops[x].excluyente);
      R[n] = R[n].includes(k) ? R[n].filter(x => x !== k) : [...R[n], k];
    }
    document.querySelectorAll(".op").forEach(b=>{
      const on = R[n].includes(+b.dataset.k);
      b.classList.toggle("on", on); b.setAttribute("aria-checked", on);
    });
    estadoSig();
  } else {
    R[n] = k;
    document.querySelectorAll(".op").forEach(b=>{
      const on = +b.dataset.k === k;
      b.classList.toggle("on", on); b.setAttribute("aria-checked", on);
    });
    estadoSig();
    setTimeout(avanzar, 260);
  }
}

function listo(){
  const paso = PASOS[p];
  if (paso.tipo === "contacto")
    return C.nombre.trim().length >= 2 && emailOk(C.email) && C.consent;
  const q = PREGUNTAS[paso.n];
  if (q.opcional) return true;
  return q.tipo === "multi" ? R[paso.n].length > 0 : R[paso.n] !== null;
}

function estadoSig(){
  const b = $("#sig"); if (!b) return;
  const paso = PASOS[p], ok = listo(), ultimo = p === PASOS.length - 1;
  b.dataset.listo = ok ? "si" : "no";
  if (paso.tipo === "contacto"){
    b.textContent = ok ? (ultimo ? "Ver mi perfil →" : "Empezar →")
      : (!C.nombre.trim() || !C.email.trim() ? "Completá tus datos →" : "Falta confirmar el consentimiento →");
    return;
  }
  const q = PREGUNTAS[paso.n];
  b.textContent = !ok
    ? (q.tipo === "multi" ? "Elegí al menos una →" : "Elegí una opción →")
    : (ultimo ? "Ver mi perfil →"
      : (q.opcional && R[paso.n].length === 0 ? "Saltear →" : "Siguiente →"));
}

function avanzar(){
  if (!listo()) return;
  if (p < PASOS.length - 1){ p++; pintar(); } else resultado();
}

document.addEventListener("keydown", e => {
  const v = $("#escena").dataset.vista;
  if (v !== "pregunta") return;
  const ops = document.querySelectorAll(".op"); if (!ops.length) return;
  if (/^[1-9]$/.test(e.key) && +e.key <= ops.length){ e.preventDefault(); elegir(PASOS[p].n, +e.key - 1); }
  if (e.key === "Enter"){ e.preventDefault(); avanzar(); }
  if (e.key === "Backspace" && p > 0){ e.preventDefault(); p--; pintar(); }
});

/* ========================= resultado ========================= */
function resultado(){
  const r = calcular(), K = CARTERAS[r.nivel];
  const marcar = n => PREGUNTAS[n].tipo === "multi"
    ? R[n].map(k => PREGUNTAS[n].ops[k].t)
    : (R[n] === null ? [] : [PREGUNTAS[n].ops[R[n]].t]);
  const temas = marcar(8), broker = marcar(9), tg = marcar(10), alertas = marcar(11);

  $("#top").hidden = true;
  const e = $("#escena");
  e.dataset.vista = "resultado";
  e.innerHTML = `
    <div style="padding-top:44px">
      <div class="eyebrow res-eyebrow">${esc(C.nombre.trim().split(" ")[0] || "Tu")} · resultado</div>
      <h1 class="perfil-nombre">${esc(PERFILES[r.nivel])}</h1>
      <p class="perfil-score">Score de riesgo <b>${r.score}</b> / 100</p>

      <div class="escala-wrap">
        <div class="escala">
          ${PERFILES.map((_,k)=>`<div class="tramo ${k===r.nivel?"activo":(k<r.nivel?"previo":"")}"></div>`).join("")}
        </div>
        <div class="aguja" style="left:calc(${r.score}% - 1px)"></div>
      </div>
      <div class="escala-lab">
        ${PERFILES.map((x,k)=>`<span class="${k===r.nivel?"activo":""}">${esc(x.replace("Moderadamente ","Mod. "))}</span>`).join("")}
      </div>

      ${r.limitado?`<div class="tope"><b>Perfil acotado.</b> Por puntaje te ubicabas en <b>${esc(PERFILES[r.nivelBruto])}</b>,
        pero una o más respuestas ponen un techo de idoneidad: ${r.motivos.map(m=>`“${esc(m)}”`).join(", ")}.
        El apetito de riesgo no alcanza si el horizonte o la experiencia no lo acompañan.</div>`:""}

      <div class="cartera">
        <div class="cartera-top">Cartera modelo que te corresponde</div>
        <div class="cartera-cuerpo">
          <h3 class="cartera-nombre">${esc(K.nombre)}</h3>
          <p class="cartera-sat">${K.nota?esc(K.nota)+" · ":""}${K.genesis
            ? `Satélite <b>Génesis</b> habilitado, ${esc(K.genesis)} de la cartera`
            : `Satélite <b>Génesis</b> no habilitado para este perfil`}</p>
          <table class="mix">${K.mix.map(([a,b])=>`<tr><td>${esc(a)}</td><td>${esc(b)}</td></tr>`).join("")}
            ${K.genesis?`<tr><td>Génesis · apuestas temáticas</td><td>${esc(K.genesis)}</td></tr>`:""}</table>
        </div>
      </div>

      <h2 class="sub">Cómo se compone</h2>
      <div class="dims">
        ${[["Tolerancia al riesgo",r.dims.riesgo],["Conocimiento",r.dims.conoc],["Objetivo",r.dims.objet]]
          .map(([lab,v])=>{const w=Math.max(0,Math.min(100,v));return `<div class="dim">
            <div class="dim-lab">${lab}</div>
            <div class="dim-bar"><span data-w="${w}"></span></div>
            <div class="dim-val">${w}%</div></div>`}).join("")}
      </div>

      <h2 class="sub">Qué significa</h2>
      <p class="lectura">${esc(K.txt)}</p>

      <h2 class="sub">Tus datos</h2>
      <div class="dato"><span>Nombre</span><span>${esc(C.nombre)}</span></div>
      <div class="dato"><span>Email</span><span>${esc(C.email)}</span></div>
      ${C.tel.trim()?`<div class="dato"><span>WhatsApp</span><span>${esc(C.tel)}</span></div>`:""}
      <div class="dato"><span>Broker</span><span>${esc(broker[0]||"—")}</span></div>
      <div class="dato"><span>Canal ${esc(CANAL_TG)}</span><span>${esc(tg[0]||"—")}</span></div>

      ${temas.length?`<h2 class="sub">Temáticas de interés</h2>
        <div class="chips">${temas.map(t=>`<span class="chip">${esc(t)}</span>`).join("")}</div>`:""}
      ${alertas.length?`<h2 class="sub">Alertas del Update de Estrategia</h2>
        <div class="chips">${alertas.map(t=>`<span class="chip gris">${esc(t)}</span>`).join("")}</div>`:""}

      <div class="acciones">
        <button class="btn-sec" id="copiar">Copiar ficha</button>
        <button class="btn-sec" id="bajar">Descargar ficha</button>
        <button class="btn-sec" id="reiniciar">Volver a empezar</button>
      </div>
      <textarea id="copia" readonly aria-label="Ficha para copiar"></textarea>

      <p class="legal">Este test es una herramienta orientativa de autodiagnóstico de ${esc(MARCA)}. No constituye
      asesoramiento de inversión personalizado ni una recomendación de compra o venta, y no reemplaza al test de
      perfil del inversor que la normativa CNV exige completar al abrir una cuenta comitente ante un ALyC. Los
      rangos de asignación son referencias generales por banda de perfil, no una cartera cerrada.</p>
    </div>`;

  requestAnimationFrame(()=>document.querySelectorAll(".dim-bar span").forEach(s=>s.style.width=s.dataset.w+"%"));

  const texto = ficha(r, K, temas, broker, tg, alertas);
  $("#copiar").onclick = () => {
    const ta = $("#copia");
    const fallback = () => { ta.value = texto; ta.style.display = "block"; ta.select(); $("#copiar").textContent = "Copialo de acá ↓"; };
    if (navigator.clipboard?.writeText){
      navigator.clipboard.writeText(texto).then(()=>{
        $("#copiar").textContent = "Copiada ✓";
        setTimeout(()=>$("#copiar").textContent="Copiar ficha",1800);
      }, fallback);
    } else fallback();
  };
  $("#bajar").onclick = () => {
    const data = { fecha:new Date().toISOString(), contacto:{...C}, perfil:PERFILES[r.nivel],
      cartera:CARTERAS[r.nivel].nombre, genesis:CARTERAS[r.nivel].genesis, score:r.score,
      dimensiones:r.dims, acotado:r.limitado, motivos_tope:r.motivos,
      respuestas:PREGUNTAS.map((q,n)=>({pregunta:q.titulo,respuesta:marcar(n)})) };
    const slug = (C.nombre.trim().toLowerCase().replace(/[^a-z0-9]+/g,"-").replace(/^-|-$/g,"")) || "cliente";
    const url = URL.createObjectURL(new Blob([JSON.stringify(data,null,2)],{type:"application/json"}));
    const a = document.createElement("a");
    a.href = url; a.download = `perfil-${slug}.json`; a.click();
    setTimeout(()=>URL.revokeObjectURL(url),1500);
  };
  $("#reiniciar").onclick = () => {
    R.forEach((_,n)=>R[n] = PREGUNTAS[n].tipo === "multi" ? [] : null);
    C.nombre = C.email = C.tel = ""; C.consent = false;
    p = 0; inicio();
  };
  window.scrollTo({top:0,behavior:"instant"});
}

function ficha(r, K, temas, broker, tg, alertas){
  return [
    `FICHA DE PERFIL — ${MARCA} — ${new Date().toLocaleDateString("es-AR")}`,
    ``,
    `${C.nombre}  |  ${C.email}${C.tel.trim() ? "  |  " + C.tel : ""}`,
    ``,
    `Perfil: ${PERFILES[r.nivel]}   |   Score: ${r.score}/100`,
    `Cartera modelo: ${K.nombre}${K.nota ? " (" + K.nota + ")" : ""}`,
    `Génesis: ${K.genesis || "no habilitado"}`,
    r.limitado ? `Acotado desde ${PERFILES[r.nivelBruto]} por: ${r.motivos.join("; ")}` : ``,
    `Tolerancia al riesgo ${r.dims.riesgo}% · Conocimiento ${r.dims.conoc}% · Objetivo ${r.dims.objet}%`,
    ``,
    `ENCUADRE ORIENTATIVO`,
    ...K.mix.map(([a,b])=>`  ${a}: ${b}`),
    K.genesis ? `  Génesis: ${K.genesis}` : ``,
    ``,
    `SEGMENTACIÓN`,
    `  Broker: ${broker[0] || "—"}`,
    `  Telegram dSs: ${tg[0] || "—"}`,
    `  Temáticas: ${temas.length ? temas.join(" / ") : "—"}`,
    `  Alertas: ${alertas.length ? alertas.join(" / ") : "no solicitadas"}`,
    ``,
    `RESPUESTAS`,
    ...PREGUNTAS.map((q,n)=>{
      const v = q.tipo === "multi"
        ? (R[n].length ? R[n].map(k=>q.ops[k].t).join(" / ") : "—")
        : (R[n] === null ? "—" : q.ops[R[n]].t);
      return `  ${n+1}. ${q.titulo}\n     → ${v}`;
    })
  ].filter(x => x !== ``).join("\n");
}

inicio();
</script>
</body>
</html>
