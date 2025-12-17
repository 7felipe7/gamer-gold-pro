<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gamer Gold Pro - Elite Edition</title>
    <style>
        :root { --primary: #ff5722; --bg: #0f0f0f; --card: #1a1a1a; }
        body { background-color: var(--bg); color: white; font-family: 'Segoe UI', sans-serif; padding: 15px; margin: 0; }
        
        .container { max-width: 500px; margin: 0 auto; }
        
        .card-pro {
            background-color: var(--card); border-radius: 20px; padding: 20px;
            margin-bottom: 20px; border: 1px solid #333;
            box-shadow: 0 10px 30px rgba(0,0,0,0.7);
        }

        .title { color: var(--primary); font-size: 1.4rem; font-weight: bold; margin-bottom: 20px; text-align: center; text-transform: uppercase; letter-spacing: 2px; }

        input[type="text"] { width: 100%; padding: 15px; border-radius: 10px; border: none; font-size: 1.1rem; background: #252525; color: white; margin-bottom: 10px; box-sizing: border-box; }

        /* Selector de Colores */
        .color-section { background: #252525; padding: 15px; border-radius: 12px; margin-bottom: 15px; }
        .color-row { display: flex; justify-content: space-around; align-items: center; }
        input[type="color"] { width: 45px; height: 45px; border: none; border-radius: 50%; cursor: pointer; background: none; }

        /* Símbolos */
        .symbol-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 10px; margin-bottom: 15px; }
        .sym-btn { background: #333; border: 1px solid #444; color: white; padding: 10px; border-radius: 8px; cursor: pointer; font-size: 1.2rem; }

        /* Botones */
        .btn-main { width: 100%; padding: 15px; border-radius: 10px; border: none; font-weight: bold; cursor: pointer; margin-bottom: 10px; font-size: 1rem; text-transform: uppercase; }
        .btn-gen { background: linear-gradient(45deg, #ff5722, #ff9800); color: white; }
        .btn-space { background: transparent; color: #ff5722; border: 1px dashed #ff5722; }

        /* Resultados */
        .nick-item { background: #222; padding: 15px; border-radius: 12px; margin-bottom: 10px; border-left: 4px solid var(--primary); }
        .nick-preview { font-size: 1.3rem; font-weight: bold; margin-bottom: 8px; }
        .nick-footer { display: flex; justify-content: space-between; align-items: center; }
        .color-code { font-family: monospace; font-size: 0.7rem; color: #777; }
        .btn-copy { background: #333; border: 1px solid var(--primary); color: var(--primary); padding: 6px 12px; border-radius: 6px; cursor: pointer; }

        /* Logo Preview */
        .logo-display { background: #000; padding: 30px; border-radius: 15px; text-align: center; font-size: 2.5rem; font-weight: bold; min-height: 60px; margin-top: 10px; }
    </style>
</head>
<body>

<div class="container">
    
    <div class="card-pro">
        <div class="title">🏆 Nicks & Degradados</div>
        <input type="text" id="nickInput" placeholder="Tu Nombre..." maxlength="15">
        
        <div class="color-section">
            <div class="color-row">
                <input type="color" id="color1" value="#ff5722">
                <span>➡</span>
                <input type="color" id="color2" value="#ffff00">
            </div>
        </div>

        <div class="symbol-grid">
            <button class="sym-btn" onclick="addSym('亗')">亗</button>
            <button class="sym-btn" onclick="addSym('⚡')">⚡</button>
            <button class="sym-btn" onclick="addSym('꧁')">꧁</button>
            <button class="sym-btn" onclick="addSym('꧂')">꧂</button>
            <button class="sym-btn" onclick="addSym('〆')">〆</button>
        </div>

        <button class="btn-main btn-space" onclick="addSym('ㅤ')">+ Espacio Invisible</button>
        <button class="btn-main btn-gen" onclick="generar()">GENERAR ESTILOS</button>

        <div id="resultados"></div>
    </div>

    <div class="card-pro">
        <div class="title">✨ Logo Gamer</div>
        <input type="text" id="logoInput" placeholder="Nombre del Clan..." oninput="updateLogo()">
        <div id="logoPreview" class="logo-display">LOGO</div>
    </div>

</div>

<script>
    const input = document.getElementById('nickInput');
    const logoIn = document.getElementById('logoInput');

    function addSym(s) {
        input.value += s;
        input.focus();
    }

    function updateLogo() {
        const logoPreview = document.getElementById('logoPreview');
        const c1 = document.getElementById('color1').value;
        const c2 = document.getElementById('color2').value;
        logoPreview.innerText = logoIn.value || "LOGO";
        logoPreview.style.background = `linear-gradient(to right, ${c1}, ${c2})`;
        logoPreview.style.webkitBackgroundClip = "text";
        logoPreview.style.webkitTextFillColor = "transparent";
    }

    function generar() {
        const val = input.value.trim();
        const c1 = document.getElementById('color1').value.toUpperCase();
        const c2 = document.getElementById('color2').value.toUpperCase();
        const res = document.getElementById('resultados');
        if(!val) return alert("Escribe algo");

        const estilos = [`꧁ঔৣ☬${val}☬ঔৣ꧂`, `亗 ${val} 亗`, `⚡${val}⚡`, `『VLT』${val}`];
        res.innerHTML = "";

        estilos.forEach(e => {
            const mitad = Math.floor(e.length / 2);
            const fullCode = `[${c1.replace('#','')}]${e.substring(0,mitad)}[${c2.replace('#','')}]${e.substring(mitad)}`;
            
            res.innerHTML += `
                <div class="nick-item">
                    <div class="nick-preview" style="background:linear-gradient(to right, ${c1}, ${c2}); -webkit-background-clip:text; -webkit-text-fill-color:transparent;">${e}</div>
                    <div class="nick-footer">
                        <span class="color-code">${fullCode}</span>
                        <button class="btn-copy" onclick="copy('${fullCode}')">Copiar</button>
                    </div>
                </div>`;
        });
    }

    function copy(t) {
        navigator.clipboard.writeText(t);
        alert("¡Copiado con éxito!");
    }
</script>

</body>
</html>
