<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>PCP Digital - Wilian</title>
    <style>
        :root { --primary: #5d2da8; --success: #28a745; --danger: #dc3545; }
        body { font-family: sans-serif; margin: 0; background: #f0f2f5; }
        header { background: white; padding: 20px; border-bottom: 2px solid #ddd; display: flex; justify-content: space-between; position: sticky; top: 0; }
        .container { padding: 15px; max-width: 800px; margin: auto; }
        .op-card { background: white; border-radius: 10px; padding: 20px; margin-bottom: 12px; display: flex; justify-content: space-between; align-items: center; border-left: 8px solid var(--primary); box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
        #tela-detalhe { display: none; background: white; min-height: 100vh; position: fixed; top: 0; left: 0; width: 100%; z-index: 200; overflow-y: auto; }
        .header-detalhe { background: var(--primary); color: white; padding: 20px; display: flex; align-items: center; }
        .grid-tecnico { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; padding: 15px; background: #eee; }
        .box-tecnico { background: white; padding: 10px; border-radius: 5px; text-align: center; }
        .tabela-grade { width: 100%; border-collapse: collapse; margin-top: 20px; }
        .tabela-grade th, .tabela-grade td { border: 1px solid #ccc; padding: 12px; text-align: center; font-weight: bold; }
        .ef-bom { color: var(--success); font-size: 2rem; font-weight: bold; }
        .ef-ruim { color: var(--danger); font-size: 2rem; font-weight: bold; }
    </style>
</head>
<body>

<div id="tela-lista">
    <header>
        <div><strong>PCP Digital - Wilian</strong><br><small>Semana 12</small></div>
    </header>
    <div class="container" id="lista-corpo"></div>
</div>

<div id="tela-detalhe">
    <div class="header-detalhe">
        <button onclick="fecharDetalhe()" style="margin-right:20px; background:none; border:1px solid white; color:white; padding:10px;">VOLTAR</button>
        <div><div id="det-comando" style="font-weight:bold"></div><div id="det-produto" style="font-size:0.8rem"></div></div>
    </div>
    <div class="grid-tecnico">
        <div class="box-tecnico"><span>Tecido</span><br><strong id="det-tecido"></strong></div>
        <div class="box-tecnico"><span>Cor</span><br><strong id="det-cor"></strong></div>
    </div>
    <div class="container">
        <center><small>EFICIÊNCIA</small><div id="det-eficiencia"></div></center>
        <table class="tabela-grade">
            <thead><tr><th>34</th><th>36</th><th>38</th><th>40</th><th>42</th><th>44</th><th>46</th><th>48</th></tr></thead>
            <tbody><tr><td id="g34"></td><td id="g36"></td><td id="g38"></td><td id="g40"></td><td id="g42"></td><td id="g44"></td><td id="g46"></td><td id="g48"></td></tr></tbody>
        </table>
    </div>
</div>

<script>
    const dadosPCP = [
        { comando: "OPD002612.1", produto: "7696 - CALÇA FEM BOOTCUT PETIT", cor: "JEANS", qtd: 91, baixado: "100%", tecido: "JULIA PLUS", ef: 86, grade: { g34: 5, g36: 7, g38: 12, g40: 12, g42: 24, g44: 12, g46: 12, g48: 7 } },
        { comando: "OPD002598.1", produto: "6074 - CALÇA MAS RETA COMFORT", cor: "UNICA", qtd: 100, baixado: "100%", tecido: "DENIM STRETCH", ef: 81, grade: { g34: 0, g36: 10, g38: 20, g40: 20, g42: 30, g44: 10, g46: 10, g48: 0 } }
    ];

    function popular() {
        document.getElementById('lista-corpo').innerHTML = dadosPCP.map(op => `
            <div class="op-card" onclick="ver('${op.comando}')">
                <div><strong>${op.comando}</strong><br><small>${op.produto}</small></div>
                <div style="color:green; font-weight:bold">${op.baixado}</div>
            </div>`).join('');
    }

    function ver(id) {
        const op = dadosPCP.find(i => i.comando === id);
        document.getElementById('det-comando').innerText = op.comando;
        document.getElementById('det-produto').innerText = op.produto;
        document.getElementById('det-tecido').innerText = op.tecido;
        document.getElementById('det-cor').innerText = op.cor;
        document.getElementById('det-eficiencia').innerText = op.ef + "%";
        document.getElementById('det-eficiencia').className = op.ef >= 85 ? "ef-bom" : "ef-ruim";
        for(let g in op.grade) { document.getElementById(g).innerText = op.grade[g]; }
        document.getElementById('tela-detalhe').style.display = 'block';
    }

    function fecharDetalhe() { document.getElementById('tela-detalhe').style.display = 'none'; }
    popular();
</script>
</body>
</html>
